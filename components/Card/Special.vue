<template>
  <div class="p-4">
    <div class="rounded-xl w-full p-4">
      <div class="flex flex-col items-left space-y-4">
        <div class="text-3xl font-bold">{{ title }}</div>
        <div :class="`flex flex-col items-left space-y-2 text-justify overflow-y-hidden transition-all duration-500 ease-in-out ${collapse ? 'max-h-[20rem]' : 'max-h-[100rem]'}`">
          <p
            v-for="(desc, i) in description"
            :key="`desc${i}`"
            class="text-base dark:text-zinc-100 text-zinc-900"
          >
            {{ desc }}
          </p>
        </div>
        <button class = "text-lg text-blue-400" @click="() => collapse = !collapse">Read {{collapse ? 'more' : 'less' }}</button>
      </div>
    </div>
  </div>
</template>
<script setup>
const { title, description } = defineProps(["title", "description"]);

const collapse = ref(true)
</script>
