<template>
  <div class="app">
    <Navbar />
    <div class="container">
      <div class="row">
        <router-view />
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: {
    Navbar,
  },
};
</script>