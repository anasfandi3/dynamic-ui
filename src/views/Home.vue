<template>
  <div class="home">
    <Navbar />
    <b-container style="background: red"> ssss </b-container>
    <Workspaces />
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Workspaces from "@/components/Workspaces.vue";
// @ is an alias to /src
export default {
  name: "Home",
  components: { Navbar, Workspaces },
};
</script>
