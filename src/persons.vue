<script setup>
import { ref } from 'vue'

const persons = ref([])
const error = ref(null)

async function fetchAllPersons() {
  try {
    const res = await fetch('/persons')
    let data = await res.json()
    if (!res.ok) {
      error.value = `Impossible d'obtenir la liste des personnes`
    } else {
      persons.value = data
    }
  } catch(err) {
    error.value = "Impossible d'accéder à la source de données. " + err
  }
}

fetchAllPersons()
</script>

<template>
  <div>
      <h2 class="mybg">All registered persons:</h2>
      <div v-if="persons.length">
          <div v-for="person in persons" :key="person.lastname" class="row col-lg-6">
              <p>{{ person.firstname }} {{ person.lastname}}</p>
          </div>
      </div>
      <div v-if="error" class="alert alert-danger alert-dismissible fade show">
          <p><strong>Error!</strong> {{ error }}</p>
      </div>
  </div>
</template>

