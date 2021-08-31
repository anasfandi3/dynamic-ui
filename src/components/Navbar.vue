<template>
  <div class="nav-menu nav-menu-x nav-menu-top nav-menu-left">
    <b-navbar type="dark" variant="dark">
      <div class="mx-1">
        <a draggable="true" @dragend="dock($event)" class="light"
          ><i class="fas fa-th fa-lg"></i
        ></a>
      </div>
      <div class="logo">
        <b style="font-size: 20px; color: white">AVL</b>
      </div>
      <b-navbar-nav class="nav-list ml-auto">
        <!-- Navbar dropdowns -->

        <b-nav-item right class="avatar">
          <span>Username</span>
          <img
            class="rounded-circle shadow-4"
            width="40"
            src="https://placekitten.com/300/300"
          />
        </b-nav-item>

        <b-nav-item right>
          <i class="fas fa-bell fa-2x"></i>
        </b-nav-item>

        <b-nav-item right disabled>
          <i class="fas fa-envelope fa-2x"></i>
        </b-nav-item>
        <b-nav-item-dropdown right no-caret>
          <template #button-content>
            <i class="fas fa-plus-circle fa-2x"></i>
          </template>
          <b-dropdown-header>Add items</b-dropdown-header>
          <b-dropdown-item href="#">User</b-dropdown-item>
          <b-dropdown-item href="#">Device</b-dropdown-item>
          <b-dropdown-item href="#">Driver</b-dropdown-item>
          <b-dropdown-item href="#">Gepfence</b-dropdown-item>
          <b-dropdown-item href="#">Alert</b-dropdown-item>
          <b-dropdown-item href="#">Event</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
import JQuery from "jquery";
let $ = JQuery;
export default {
  name: "Navbar",
  methods: {
    dock($event) {
      // let screen_width = screen.width;
      let screen_height = screen.height;
      // let sX = event.screenX;
      let sY = $event.screenY;
      console.log(sY);
      let el = $(".nav-menu")[0];
      let workspace = $(".ws-panel")[0];
      console.log(workspace.offsetHeight);
      if (sY < screen_height * 0.35) {
        el.classList.remove("nav-menu-bottom");
        el.style.removeProperty("bottom");
        workspace.style.removeProperty("bottom");
        el.classList.add("nav-menu-top");
        if (workspace.classList.contains("ws-panel-top"))
          workspace.style.setProperty("top", el.offsetHeight + "px");
      } else if (sY > screen_height * 0.65) {
        el.classList.remove("nav-menu-top");
        el.style.removeProperty("top");
        workspace.style.removeProperty("top");
        el.classList.add("nav-menu-bottom");
        if (workspace.classList.contains("ws-panel-bottom"))
          workspace.style.setProperty("bottom", el.offsetHeight + "px");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav-menu-top {
  top: 0px;
}
.nav-menu-bottom {
  bottom: 0px;
}
.nav-menu-right {
  right: 0px;
}
.nav-menu-left {
  left: 0px;
}

.nav-menu {
  position: fixed;
}

.nav-menu-x {
  width: 100%;
}
.nav-menu-x > nav > .nav-list {
  flex-direction: row-reverse !important;
}
.nav-menu-x > nav > .logo {
  margin-left: 15px;
  margin-right: 15px;
  text-align: start;
  width: 100%;
}

.nav-menu-y {
  height: 100%;
}
.nav-menu-y > nav {
  height: 100%;
  display: block;
}
.nav-menu-y > nav > .nav-list {
  flex-direction: column;
}
.nav-menu-y > nav > .nav-list > .d-table {
  display: block;
}
.nav-menu-y > nav > .nav-list > .avatar > a > span {
  display: none;
}

.avatar > a {
  display: flex;
  align-items: center;
}
.avatar > a > span {
  padding-left: 5px;
  padding-right: 5px;
}

.light {
  color: var(--bs-light);
}
.navbar {
  padding: 0.5rem
}
</style>
