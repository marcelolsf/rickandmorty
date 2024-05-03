<script setup>

  import { onMounted, reactive, ref} from 'vue';
  import ListRickandMorty from '../components/ListRickandMorty.vue'

  let RickandMorty = reactive(ref());

  onMounted(() => {
    fetch("https://rickandmortyapi.com/api/character?limit=20")
    .then(response => response.json())
    .then(response => {
      RickandMorty.value = response.results
      console.log(RickandMorty)
    })
  })
</script>


<template>
  <main>
    <div class="container-fluid">
      <div class="row mt-8">   
        <div class="col-sm-12 col-md-6">
          <div class="card" style="width: 100%;">
            <div class="card-body row">
                <ListRickandMorty
              v-for="rickandmorty in RickandMorty"
              :key="rickandmorty.name"
              :name="rickandmorty.name"
              :url="rickandmorty.url"
              />
            </div>
          </div>
        </div>  
      </div>
    </div>
  </main>
</template>




