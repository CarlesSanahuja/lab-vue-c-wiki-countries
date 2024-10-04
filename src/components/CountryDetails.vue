<template>
  <div v-if="country">
    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="country flag" style="width: 300px" />
    <h1>{{ country.name.common }}</h1>
    <table class="table">
      <tbody>
        <tr>
          <td>Official Name</td>
          <td>{{ country.name.official }}</td>
        </tr>
        <tr>
          <td>Capital</td>
          <td>{{ country.capital[0] }}</td>
        </tr>
        <tr>
          <td>Region</td>
          <td>{{ country.region }}</td>
        </tr>
        <tr>
          <td>Subregion</td>
          <td>{{ country.subregion }}</td>
        </tr>
        <tr>
          <td>Area</td>
          <td>{{ country.area }} km<sup>2</sup></td>
        </tr>
        <tr v-if="country.borders && country.borders.length">
          <td>Borders</td>
          <td>
            <ul>
              <li v-for="border in country.borders" :key="border">
                <router-link :to="'/list/' + border">{{ border }}</router-link>
              </li>
            </ul>
          </td>
        </tr>
        <tr>
          <td>Currency</td>
          <td>{{ currencyName }} ({{ currencySymbol }})</td>
        </tr>
        <tr>
          <td>Languages</td>
          <td>{{ countryLanguages }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'CountryDetails',
  data() {
    return {
      country: null,
    };
  },
  computed: {
    currencyName() {
      const currencyKey = Object.keys(this.country?.currencies || {})[0];
      return currencyKey ? this.country.currencies[currencyKey].name : '';
    },
    currencySymbol() {
      const currencyKey = Object.keys(this.country?.currencies || {})[0];
      return currencyKey ? this.country.currencies[currencyKey].symbol : '';
    },
    countryLanguages() {
      return this.country?.languages
        ? Object.values(this.country.languages).join(", ")
        : '';
    },
  },
  watch: {
    '$route.params.alpha3Code': {
      immediate: true,
      async handler(newVal) {
        try {
          const response = await fetch('/src/assets/countries.json');
          if (!response.ok) {
            throw new Error('Error al cargar los datos');
          }
          const data = await response.json();
          this.country = data.find(country => country.alpha3Code === newVal) || null;
        } catch (error) {
          console.error('Error al cargar los detalles del país:', error);
        }
      },
    },
  },
};
</script>