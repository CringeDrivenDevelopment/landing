<template>
  <div class="grid grid-rows-[20px_1fr_20px] items-center justify-items-center min-h-screen p-8 pb-20 gap-16 sm:p-20 font-[family-name:var(--font-geist-sans)]">
    <main class="flex flex-col gap-[32px] row-start-2 items-center sm:items-start">
      <div class="flex flex-col space-y-2">
        <SplitText
            text="nword"
            class-name="text-6xl font-semibold text-center"
            :delay="400"
            :duration="0.6"
            ease="power3.out"
            split-type="chars"
            :threshold="0.1"
            root-margin="-100px"
        />

        <SplitText
            text="driven"
            class-name="text-6xl font-semibold text-center"
            :delay="400"
            :duration="0.6"
            ease="power3.out"
            split-type="chars"
            :threshold="0.1"
            root-margin="-100px"
        />

        <SplitText
            text="design"
            class-name="text-6xl font-semibold text-center"
            :delay="400"
            :duration="0.6"
            ease="power3.out"
            split-type="chars"
            :threshold="0.1"
            root-margin="-100px"
        />
      </div>
    </main>
    <footer class="row-start-3 flex gap-[24px] flex-wrap items-center justify-center">
      <a
          class="flex items-center gap-2 hover:underline hover:underline-offset-4"
          href="https://t.me/cringe_driven_dev"
          target="_blank"
          rel="noopener noreferrer"
      >
        <NuxtImg
            aria-hidden="true"
            src="/telegram.svg"
            alt="Telegram icon"
            width={16}
            height={16}
        />
        tg
      </a>

      <a
          class="flex items-center gap-2 hover:underline hover:underline-offset-4"
          href="https://github.com/Cringe-driven-development"
          target="_blank"
          rel="noopener noreferrer"
      >
        <NuxtImg
            aria-hidden="true"
            src="/github.svg"
            alt="GitHub icon"
            width={16}
            height={16}
        />
        gh
      </a>
    </footer>
  </div>
</template>

<script setup lang="ts">
</script>
