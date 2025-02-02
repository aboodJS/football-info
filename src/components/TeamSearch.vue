<script setup>
import InfoBox from "./InfoBox.vue";

import { ref, computed } from "vue";
const show = ref(false);
const query = ref("");
const formatedQuery = computed(function () {
  return query.value.split(" ").join("+");
});
const key = ref("");
let teamInfo = ref([]);

function getTeam() {
  const url = `https://v3.football.api-sports.io/teams?search=${formatedQuery.value}`;
  fetch(url, {
    method: "GET",
    headers: {
      "x-rapidapi-host": "v3.football.api-sports.io",
      "x-rapidapi-key": key.value,
    },
  })
    .then((res) => res.json())
    .then((result) => {
      teamInfo.value = result.response;
    })
    .catch((err) => console.log(err));
}

const teamName = ref("");
const teamIcon = ref("");
const teamDate = ref("");
const teamCountry = ref("");
</script>

<template>
  <main class="bg-slate-900">
    <section class="grid w-96 h-36 justify-center text-center mx-auto mb-5">
      <h3
        class="text-center text-white justify-self-center text-2xl font-bold mx-0"
      >
        team search
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
        @click="getTeam"
      >
        search
      </button>
    </section>
    <info-box
      :visible="show"
      :name="teamName"
      :foundingDate="teamDate"
      :image="teamIcon"
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
        v-for="team in teamInfo"
        @click="
          () => {
            show = true;
            teamName = team.team.name;
            teamIcon = team.team.logo;
            teamDate = team.team.founded;
            teamCountry = team.team.country;
          }
        "
      >
        <ul>
          <li>
            <h3>team name: {{ team.team.name || "N/A" }}</h3>
          </li>
          <li>
            <h3>team code: {{ team.team.code || "N/A" }}</h3>
          </li>
          <li>
            <h3>founded: {{ team.team.founded || "N/A" }}</h3>
          </li>
          <li>
            <h3>country: {{ team.team.country || "N/A" }}</h3>
          </li>
          <img
            class="justify-self-center"
            :src="team.team.logo"
            :alt="team.team.name || 'N/A'"
          />
        </ul>
      </div>
    </section>
  </main>
</template>
