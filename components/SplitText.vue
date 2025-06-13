<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
import { SplitText as GSAPSplitText } from 'gsap/SplitText';

gsap.registerPlugin(ScrollTrigger, GSAPSplitText);

interface SplitTextProps {
  text: string;
  className?: string;
  delay?: number;
  duration?: number;
  ease?: string | gsap.EaseFunction;
  splitType?: 'chars' | 'words' | 'lines' | 'words, chars';
  from?: gsap.TweenVars;
  to?: gsap.TweenVars;
  threshold?: number;
  rootMargin?: string;
  onLetterAnimationComplete?: () => void;
}

const props = withDefaults(defineProps<SplitTextProps>(), {
  className: '',
  delay: 100,
  duration: 0.6,
  ease: 'power3.out',
  splitType: 'chars',
  from: () => ({ opacity: 0, y: 40 }),
  to: () => ({ opacity: 1, y: 0 }),
  threshold: 0.1,
  rootMargin: '-100px',
});

const root = ref<HTMLElement | null>(null);
let splitter: GSAPSplitText | null = null;
let animationTimeline: gsap.core.Timeline | null = null;

function setupAnimation() {
  if (!root.value) return;

  // Clean up previous animations
  if (animationTimeline) {
    animationTimeline.kill();
    animationTimeline = null;
  }
  if (splitter) {
    splitter.revert();
    splitter = null;
  }

  // Setup position for line splitting
  const absoluteLines = props.splitType === 'lines';
  if (absoluteLines) {
    root.value.style.position = 'relative';
  }

  // Create split text
  splitter = new GSAPSplitText(root.value, {
    type: props.splitType,
    absolute: absoluteLines,
    linesClass: 'split-line',
  });

  // Determine targets based on split type
  let targets: Element[];
  switch (props.splitType) {
    case 'lines':
      targets = splitter.lines;
      break;
    case 'words':
      targets = splitter.words;
      break;
    case 'words, chars':
      targets = [...splitter.words, ...splitter.chars];
      break;
    default:
      targets = splitter.chars;
  }

  // Optimize rendering
  targets.forEach((t) => ((t as HTMLElement).style.willChange = 'transform, opacity'));

  // Calculate scroll trigger position
  const startPct = (1 - props.threshold) * 100;
  const m = /^(-?\d+)px$/.exec(props.rootMargin);
  const raw = m ? parseInt(m[1], 10) : 0;
  const sign = raw < 0 ? `-=${Math.abs(raw)}px` : `+=${raw}px`;
  const start = `top ${startPct}%${sign}`;

  // Create animation timeline
  animationTimeline = gsap.timeline({
    scrollTrigger: {
      trigger: root.value,
      start,
      toggleActions: 'play none none none',
      once: true,
    },
    smoothChildTiming: true,
    onComplete: props.onLetterAnimationComplete,
  });

  animationTimeline.set(targets, {
    ...props.from,
    immediateRender: false,
    force3D: true
  });

  animationTimeline.to(targets, {
    ...props.to,
    duration: props.duration,
    ease: props.ease,
    stagger: props.delay / 1000,
    force3D: true,
  });
}

function cleanUp() {
  if (animationTimeline) {
    animationTimeline.kill();
    animationTimeline = null;
  }
  ScrollTrigger.getAll().forEach(trigger => trigger.kill());
  if (splitter) {
    splitter.revert();
    splitter = null;
  }
}

// Initial setup
onMounted(setupAnimation);

// Clean up on unmount
onUnmounted(cleanUp);

// Re-run animation when reactive props change
watch(
    () => [
      props.text,
      props.delay,
      props.duration,
      props.ease,
      props.splitType,
      props.from,
      props.to,
      props.threshold,
      props.rootMargin,
    ],
    () => {
      cleanUp();
      setupAnimation();
    }
);
</script>

<template>
  <p
      ref="root"
      class="split-parent overflow-hidden inline-block whitespace-normal"
      :class="className"
      style="word-wrap: break-word"
  >
    {{ text }}
  </p>
</template>