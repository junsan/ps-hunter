<template>
    <div class="q-pa-md">
      <q-card class="my-card" style="margin-bottom: 20px;" v-for="game in games" :key="game.npCommunicationId">
        <img :src="game.trophyTitleIconUrl">
  
        <q-card-section>
          <div style="float: left; width: 167px;">
            <div class="text-h6">{{ game.trophyTitleName }}</div>
            <q-badge v-if="game.trophyTitlePlatform === 'PS5'" style="padding: 5px 10px;" color="black" text-color="white" label="PS5" />
            <q-badge  v-if="game.trophyTitlePlatform === 'PS4'" style="padding: 5px 10px;" color="black" text-color="white" label="PS4" />
          </div>
          <div class="float-right">
            <div class="trophy">
                <img src="~assets/plat.png" style="height: 30px;">
                <img src="~assets/gold.png" style="height: 30px;">
                <img src="~assets/silver.png" style="height: 30px;">
                <img src="~assets/bronze.png" style="height: 30px;">
            </div>
            <div class="earntrophy">
                <span>{{ game.earnedTrophies.platinum }}</span>
                <span>{{ game.earnedTrophies.gold }}</span>
                <span>{{ game.earnedTrophies.silver }}</span>
                <span style="margin-right: 0;">{{ game.earnedTrophies.bronze }}</span>
            </div>
            <div>
              <q-btn size="sm" :to="{ name: 'index', params: { game: game.npCommunicationId } }" outline rounded color="primary" label="See all Trophies" />
            </div>
          </div>
        <div style="clear: both"></div>
        </q-card-section>
      </q-card>
    </div>
  </template>
  
  <script setup>
  import { api } from 'boot/axios'
  import { ref } from 'vue'
  
  const games = ref()
  
  const getLists = async () => {
    await api.get('/june').then((response) => {
      games.value = response.data
      console.log(response.data)
    })
  }
  
  getLists()
  
  
  </script>
<style>
.trophy img {
    margin-right: 5px;
}
.earntrophy {
    margin-left: 12px;
}
.earntrophy span {
    margin-right: 23px;
}
</style>