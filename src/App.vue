<script setup>
import { computed, ref } from "vue";
import Players from "./components/PlayerSearch.vue";
import Teams from "./components/TeamSearch.vue";

const currentTab = ref("Teams");

function update(e) {
  currentTab.value = e.innerText;
  console.log(e.innerText);
}

const tabs = { Players, Teams };
</script>

<template>
  <nav
    class="flex justify-center items-center text-white h-16 w-screen border-b-2 mb-5"
  >
    <div class="w-1/3 flex justify-evenly">
      <h2
        @click="update($event.target)"
        class="text-2xl w-1/2 h-16 text-center hover:bg-white hover:text-black cursor-pointer items-center flex justify-center transition-all"
      >
        Teams
      </h2>
      <h2
        class="justify-center text-2xl w-1/2 h-16 flex items-center text-center hover:bg-white hover:text-black cursor-pointer transition-all"
        @click="update($event.target)"
      >
        Players
      </h2>
    </div>
  </nav>

  <main class="bg-slate-900 grid">
    <component :is="tabs[currentTab]"></component>
  </main>
</template>
