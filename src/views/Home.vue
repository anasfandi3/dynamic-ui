<template>
  <div class="home">
    <Navbar />
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
<style>
@navheight: 72px;
</style>
