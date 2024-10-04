<template>
  <header class="navbar navbar-expand-lg navbar-light bg-primary">
    <nav class="container">
      <a class="navbar-brand text-white" href="#">WikiCountries</a>
      <button
        class="navbar-toggler"
        type="button"
        @click="isCollapsed = !isCollapsed"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div
        class="collapse navbar-collapse"
        :class="{ show: !isCollapsed }"
        id="navbarNav"
      >
        <ul class="navbar-nav ml-auto">
          <!-- Add navbar items here -->
        </ul>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      isCollapsed: true,
    };
  },
};
</script>