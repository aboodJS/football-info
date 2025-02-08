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
    class="grid bg-slate-800 w-3/6 h-80 fixed rounded top-1/4 left-0 right-0 mx-auto con"
    v-if="visible"
  >
    <slot></slot>
    <main
      class="flex text-white justify-evenly text-center items-center self-center w-11/12 justify-self-center"
    >
      <img class="justify-self-center" :src="image" :alt="name" />
      <div>
        <p class="hover:underline transition-all">Name: {{ name }}</p>
        <p class="hover:underline transition-all">Country: {{ country }}</p>
        <p class="hover:underline transition-all">
          Birth day: {{ foundingDate }}
        </p>
        <p class="hover:underline transition-all">
          team venue: {{ venue || "" }}
        </p>
        <p class="hover:underline transition-all">goals: {{ goals || 0 }}</p>
        <p class="hover:underline transition-all">assits: {{ assits || 0 }}</p>
        <p class="hover:underline transition-all">id: {{ id || "" }}</p>
      </div>
    </main>
  </div>
</template>
