<script setup>
const props = defineProps([
  "image",
  "name",
  "foundingDate",
  "visible",
  "country",
]);
function closeBox(e) {
  props.visible = false;
  console.log(e);
}
</script>

<template>
  <div
    class="grid bg-slate-800 w-72 h-80 fixed rounded top-1/4 right-[38%]"
    v-if="visible"
  >
    <slot></slot>
    <main class="grid text-white justify-center text-center">
      <img :src="image" :alt="name" />
      <h1>{{ name }}</h1>
      <p>{{ country }}</p>
      <p>{{ foundingDate }}</p>
    </main>
  </div>
</template>
