<script setup>
import { computed, ref } from "vue";

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
    .then((result) => (teamInfo.value = result.response))
    .catch((err) => console.log(err));
}
</script>

<template>
  <section class="grid w-96 h-28 justify-center mx-auto">
    <p>
      api key:
      <input
        class="border-2 rounded border-black focus:border-blue-500"
        v-model="key"
      />
    </p>
    <p class="justify-self-center">
      team search:
      <input
        class="border-2 rounded border-black focus:border-blue-500"
        type="text"
        name=""
        id=""
        v-model="query"
      />
    </p>

    <button
      class="bg-blue-500 w-20 h-9 text-white justify-self-center"
      @click="getTeam"
    >
      search
    </button>
  </section>

  <section class="grid grid-rows-4 grid-cols-4 justify-center gap-5">
    <div
      class="justify-self-center border-2 grid rounded-md border-blue-500 w-72"
      v-for="team in teamInfo"
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
</template>
