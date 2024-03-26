<script setup>
import { ref } from 'vue'

const persons = ref([])
const error = ref(null)

async function fetchAllPersons() {
  try {
    const res = await fetch('/persons')
    let data = await res.json()
    if (!res.ok) {
      error.value = "Impossible d'obtenir la liste des personnes"
    } else {
      persons.value = data
    }
  } catch(err) {
    error.value = "Impossible d'accéder à la source de données"
  }
}

fetchAllPersons()
</script>

<template>
  <div>
      <div v-if="persons.length" class="row">
          <div v-for="person in persons" :key="person.lastname" class="col-lg-6">
              <p>{{ person.firstname }} {{ person.lastname}}</p>
          </div>
      </div>
      <div v-if="error" class="alert alert-danger alert-dismissible fade show">
          <p><strong>Error!</strong> {{ error }}</p>
      </div>
  </div>
</template>

