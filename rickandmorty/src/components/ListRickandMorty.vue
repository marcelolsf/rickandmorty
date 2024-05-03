<script setup>
import { defineProps, ref } from 'vue';

const { name, url } = defineProps({
  name: String,
  url: String
});

const id = url.split('/').slice(-1)[0];
const imageUrl = `https://rickandmortyapi.com/api/character/avatar/${id}.jpeg`;

const status = ref('');
const species = ref('');
const gender = ref('');
const location = ref('');
const episodeCount = ref(0);

fetch(url)
  .then(response => response.json())
  .then(character => {
    status.value = character.status;
    species.value = character.species;
    gender.value = character.gender;
    location.value = character.location.name;
    episodeCount.value = character.episode.length;
  })
  .catch(error => {
    console.error('Erro ao buscar informações do personagem:', error);
  });
</script>

<template>
        <div class="col-md-4">
          <div class="card mb-3">
            <img :src="imageUrl" height="80" class="card-img-top mt-3">
            <div class="card-body">
              <h5 class="card-title">{{ name }}</h5>
              <p class="card-text">Status: {{ status }}</p>
              <p class="card-text">Espécie: {{ species }}</p>
              <p class="card-text">Gênero: {{ gender }}</p>
              <p class="card-text">Localização Atual: {{ location }}</p>
              <p class="card-text">Episódios Aparecidos: {{ episodeCount }}</p>
            </div>
        </div>
    </div>
  </template>
  
  <style>
  .card-img-top {
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    height: 200px;

  }
  </style>
  

<style>
.card-img-top {
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  height: 200px;
  object-fit: cover;
}
</style>


