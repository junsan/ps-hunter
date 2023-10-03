<template>
  <div class="q-pa-md">
    <q-card class="my-card" style="margin-bottom: 20px;" v-for="trophy in trophies" :key="trophy.trophyId">
      <img :src="trophy.trophyIconUrl">

      <q-card-section>
        <div style="float: left; width: 230px;">
          <div class="text-h6">{{ trophy.trophyName }}</div>
          <div class="text-subtitle2" style="font-weight: normal;">{{ trophy.trophyDetail }}</div>
        </div>
        <div class="float-right">
          <img v-if="trophy.trophyType === 'platinum'" src="~assets/plat.png" style="height: 80px;">
          <img v-if="trophy.trophyType === 'gold'" src="~assets/gold.png" style="height: 80px;">
          <img v-if="trophy.trophyType === 'silver'" src="~assets/silver.png" style="height: 80px;">
          <img v-if="trophy.trophyType === 'bronze'" src="~assets/bronze.png" style="height: 80px;">
        </div>
        <div style="clear: both"></div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script setup>
import { api } from 'boot/axios'
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
const route = useRoute()
const router = useRouter()
const game = ref(null)
const trophies = ref()

onMounted(async () => {
  await router.isReady()
  game.value = route.params.game
  console.log(game)

  await api.get('/game?game='+game.value).then((response) => {
    trophies.value = response.data.trophies
    console.log(response.data)
  })
})

</script>
