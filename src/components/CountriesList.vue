<template>
  <div class="row">
    <div class="col-5" style="max-height: 90vh; overflow-y: scroll">
      <div class="list-group">
        <router-link
          v-for="country in countries"
          :key="country.alpha3Code"
          class="list-group-item list-group-item-action"
          :to="'/list/' + country.alpha3Code"
        >
          <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" />
          <p>{{ country.name.common }}</p>
        </router-link>
      </div>
    </div>

    <div class="col-7">
      <router-view />  <!-- Este es el lugar donde se mostrarán los detalles del país -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Crear una referencia reactiva para almacenar los países
const countries = ref([]);

// Función para obtener los datos de la API
const fetchCountries = async () => {
  try {
    const response = await fetch('https://ih-countries-api.herokuapp.com/countries');
    if (!response.ok) throw new Error('Error al obtener los datos de los países');
    const data = await response.json();
    countries.value = data;  // Asignar los datos de la API a la lista reactiva de países
  } catch (error) {
    console.error('Error al obtener los datos:', error);
  }
};
onMounted(() => {
  fetchCountries();  // Llamar a la función cuando el componente se monte
});
</script>

<style scoped>
.list-group-item {
  display: flex;
  align-items: center;
}

.list-group-item img {
  width: 50px;
  margin-right: 15px;
}
</style>
