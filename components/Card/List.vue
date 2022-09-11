<template>
  <div class="p-4">
    <div class="rounded-xl w-full p-4">
      <div class="flex flex-col items-left space-y-4">
        <div class="text-2xl font-semibold text-blue-400 text-left uppercase">{{ title }}</div>
        <ul class="flex flex-col max-w-full list-outside lg:list-outside items-left space-y-2 text-justify list-disc">
          <li
            v-for="(desc, i) in description"
            :key="`desc${i}`"
            class="text-base break-words"
          >
          <i class="fi fi-rr-check text-cyan-400"> </i> {{ desc }}
        </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script setup>
const { title, description } = defineProps(["title", "description"]);
</script>
