<template>
  <div class="home">
  
    <CSP msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import CSP from "@/components/CSP.vue";

export default {
  name: "Home",
  components: {
    CSP,
  },
};
</script>
