<script setup>
const emits = defineEmits(["getStats"]);
const props = defineProps([
  "image",
  "name",
  "foundingDate",
  "visible",
  "country",
  "venue",
  "goals",
  "assits",
  "id",
]);
function closeBox(e) {
  props.visible = false;
  console.log(e);
}
</script>

<template>
  <div
    class="grid bg-slate-800 w-fit h-80 fixed rounded top-1/4 right-auto left-auto"
    v-if="visible"
  >
    <slot></slot>
    <main
      class="flex text-white justify-center text-center items-center self-center"
    >
      <img class="justify-self-center" :src="image" :alt="name" />
      <div>
        <h1>Name: {{ name }}</h1>
        <p>Country: {{ country }}</p>
        <p>Birth day: {{ foundingDate }}</p>
        <p>team venue: {{ venue || "" }}</p>
        <p>goals: {{ goals || 0 }}</p>
        <p>assits: {{ assits || 0 }}</p>
        <p>id: {{ id || "" }}</p>
      </div>
    </main>
  </div>
</template>
