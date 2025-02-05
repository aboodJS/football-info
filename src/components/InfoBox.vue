<script setup>
const props = defineProps([
  "image",
  "name",
  "foundingDate",
  "visible",
  "country",
  "venue",
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
      <img class="justify-self-center" :src="image" :alt="name" />
      <h1>Name: {{ name }}</h1>
      <p>Country: {{ country }}</p>
      <p>Birth day: {{ foundingDate }}</p>
      <p>team venue: {{ venue }}</p>
    </main>
  </div>
</template>
