<script setup lang="ts">
import {ArrowDown} from "lucide-vue-next";

</script>

<template>
  <section class="h-screen flex flex-col relative">
    <div  class="relative scale-70 md:scale-100 w-full h-full flex items-center justify-center">
      <h1 class="absolute text-8xl blur-[464.3px] text-center z-0">
        CRINGE <br/>
        DRIVEN <br/>
        DEVELO <br/>
        PMENT
      </h1>

      <h1 class="text-8xl text-center z-0">
        CRINGE <br/>
        DRIVEN <br/>
        DEVELO <br/>
        PMENT
      </h1>
      <div  class="absolute scale-110 top-1/8 z-10 pointer-events-none">
        <svg  width="701" height="491" viewBox="0 0 701 491" fill="none" xmlns="http://www.w3.org/2000/svg">
          <foreignObject x="-40.5" y="-40.5" width="782" height="572"><div xmlns="http://www.w3.org/1999/xhtml" style="backdrop-filter:blur(11.9px);clip-path:url(#bgblur_0_25_58_clip_path);height:100%;width:100%"></div></foreignObject><path data-figma-bg-blur-radius="23.8" d="M210.237 0L300.608 201.549L701 0L481.349 239.221L701 491H210.237L395.999 350.983L0 239.221L210.237 0Z" fill="black/10"/>
          <defs>
            <clipPath id="bgblur_0_25_58_clip_path" transform="translate(40.5 40.5)"><path d="M210.237 0L300.608 201.549L701 0L481.349 239.221L701 491H210.237L395.999 350.983L0 239.221L210.237 0Z"/>
            </clipPath></defs>
        </svg>

      </div>
    </div>
    <div class="w-full md:-mt-40 flex items-center justify-center">
      <button class="md:mb-40 flex items-center overflow-hidden whitespace-nowrap gap-1 text-xl px-40 py-10 bg-(--foreground) text-black rounded-full">
        learn more <ArrowDown/>
      </button>
    </div>
  </section>
</template>

