<script setup>
import { ref, computed } from "vue";
import InfoBox from "./InfoBox.vue";
const show = ref(false);
const query = ref("");
const formatedQuery = computed(function () {
  return query.value.split(" ").join("+");
});
const key = ref("");
let playerInfo = ref([]);

function getPlayers() {
  const url = `https://v3.football.api-sports.io/players/profiles?search=${formatedQuery.value}`;
  fetch(url, {
    method: "GET",
    headers: {
      "x-rapidapi-host": "v3.football.api-sports.io",
      "x-rapidapi-key": key.value,
    },
  })
    .then((res) => res.json())
    .then((result) => (playerInfo.value = result.response))
    .catch((err) => console.log(err));
}

const playerName = ref("");
const playerIcon = ref("");
const playerCountry = ref("");
const playerBirth = ref("");
</script>

<template>
  <main class="bg-slate-900">
    <section class="grid w-96 h-36 justify-center text-center mx-auto mb-5">
      <h3
        class="text-center text-white justify-self-center text-2xl font-bold mx-0"
      >
        player search
      </h3>
      <p class="text-white">
        api key:
        <input
          class="border-2 rounded border-blue-400 focus:border-blue-600 outline-none text-black"
          v-model="key"
        />
      </p>
      <p class="justify-self-center text-white">
        search:
        <input
          class="border-2 rounded border-blue-400 focus:border-blue-600 outline-none text-black"
          type="text"
          name=""
          id=""
          v-model="query"
        />
      </p>

      <button
        class="bg-blue-500 w-20 h-9 text-white justify-self-center rounded hover:bg-blue-600 transition-all"
        @click="getPlayers"
      >
        search
      </button>
    </section>
    <info-box
      :visible="show"
      :name="playerName"
      :image="playerIcon"
      :country="playerCountry"
      :foundingDate="playerBirth"
    >
      <box-icon
        name="x"
        color="#ffffff"
        @click="() => (show = false)"
        class="justify-self-end"
      ></box-icon>
    </info-box>
    <section class="grid grid-rows-4 grid-cols-4 justify-center gap-5">
      <div
        class="justify-self-center border-2 grid rounded-md border-blue-500 w-72 hover:bg-blue-500 text-white hover:shadow-md hover:shadow-slate-300 transition-all"
        v-for="player in playerInfo"
        @click="
          () => {
            show = true;
            playerName = player.player.name || 'N/A';
            playerIcon = player.player.photo;
            playerCountry = player.player.birth.country || 'N/A';
            playerBirth = player.player.birth.date || 'N/A';
          }
        "
      >
        <ul>
          <h3>
            <li>name: {{ player.player.name }}</li>
          </h3>
          <h3>
            <li>first name: {{ player.player.firstname || "N/A" }}</li>
          </h3>
          <h3>
            <li>last name: {{ player.player.lastname || "N/A" }}</li>
          </h3>
          <img
            class="justify-self-center"
            :src="player.player.photo"
            :alt="player.player.name"
          />
        </ul>
      </div>
    </section>
  </main>
</template>
