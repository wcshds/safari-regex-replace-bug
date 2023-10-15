<script setup lang="ts">
import { ref } from "vue";

let text = ref("abcるde😂éàö𣎴ùçてëêîcÏ💕😒測し試");
</script>

<template>
  <div class="m-4 max-w-[500px] mx-auto">
    <p>filter basic characters in range U+0000..U+FFFF</p>
    <input type="text" v-model="text" placeholder="input some characters" />

    <p class="mt-5">output:</p>
    <p class="mx-5">with normal replace method</p>
    <p class="mx-5 border h-20 rounded">
      {{ text.replace(/[^\u{10000}-\u{10FFFF}]/gu, "") }}
    </p>
    <p class="mx-5 mt-3">call matchAll first, then turn the iterator into an array, finally join characters together </p>
    <p class="mx-5 border h-20 rounded">
      <!-- It works, but it doesn't look intuitive. -->
      {{ Array.from(text.matchAll(/[\u{10000}-\u{10FFFF}]/ug)).join("") }}
    </p>
    <p class="mt-16">Note:</p>
    <p class="ml-5">
      This basic character replacement (implemented using regular expression in
      unicode mode) works fine in Chrome, Edge, and Firefox, but in Safari the
      surrogate pairs are broken.
    </p>
  </div>
</template>
