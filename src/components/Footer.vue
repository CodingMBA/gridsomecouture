<template>
  <footer>
    Copyright {{ getCurrentYear }} by <a :href="href">Bodhi Code</a>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      href: "https://www.asmith.dev"
    };
  },
  computed: {
    getCurrentYear() {
      return new Date().getFullYear();
    }
  }
};
</script>

<style>
footer {
  text-align: center;
  color: #00a672;
  letter-spacing: 0.5px;
  padding: 20px;
}
</style>
