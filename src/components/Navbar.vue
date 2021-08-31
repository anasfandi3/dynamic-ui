<template>
  <div class="nav-menu nav-menu-x nav-menu-top">
    <nav
      class="navbar navbar-dark bg-dark navbar-expand"
      type="dark"
      variant="dark"
    >
      <div class="mx-1">
        <a draggable="true" @dragend="dock($event)" class="light"
          ><i class="fas fa-th fa-lg"></i
        ></a>
      </div>
      <div class="tools">
        <b style="font-size: 20px; color: white; margin-right: 10px">AVL</b>
        <!-- language -->
        <div class="btn-group drop-direction">
          <button
            type="button"
            class="btn btn-none x-none text-white"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            <i class="fas fa-language fa-lg"></i>
          </button>
          <ul class="dropdown-menu">
            <li>
              <a class="dropdown-item" @click="changeLang('en')" href="#"
                >English</a
              >
            </li>
            <li>
              <a class="dropdown-item" @click="changeLang('ar')" href="#"
                >Arabic</a
              >
            </li>
          </ul>
        </div>

        <!-- theme -->
        <div class="btn-group drop-direction">
          <button
            type="button"
            class="btn btn-none x-none text-white"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            <i class="fas fa-palette fa-lg"></i>
          </button>
          <ul class="dropdown-menu">
            <li>
              <a class="dropdown-item" @click="changeTheme('Cerulean')" href="#"
                >Cerulean</a
              >
            </li>
            <li>
              <a class="dropdown-item" @click="changeTheme('Darkly')" href="#"
                >Darkly</a
              >
            </li>
            <li>
              <a class="dropdown-item" @click="changeTheme('Journal')" href="#"
                >Journal</a
              >
            </li>
            <li>
              <a class="dropdown-item" @click="changeTheme('Litera')" href="#"
                >Litera</a
              >
            </li>
            <li>
              <a class="dropdown-item" @click="changeTheme('Morph')" href="#"
                >Morph</a
              >
            </li>
          </ul>
        </div>

        <div class="form-check form-switch">
          <input
            class="form-check-input focus-none"
            type="checkbox"
            id="flexSwitchCheckDefault"
            v-model="isDark"
          />
          <label class="form-check-label" for="flexSwitchCheckDefault"
            ><i
              v-if="!isDark"
              style="color: yellow"
              class="fas fa-sun fa-lg"
            ></i
            ><i v-else style="color: darkblue" class="fas fa-moon fa-lg"></i
          ></label>
        </div>
      </div>

      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav nav-list">
          <li class="nav-item avatar">
            <a class="nav-link active" aria-current="page" href="#">
              <span>Username</span>
              <img
                class="rounded-circle shadow-4"
                width="40"
                src="https://placekitten.com/300/300"
              />
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#"><i class="fas fa-bell fa-2x"></i></a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#"
              ><i class="fas fa-envelope fa-2x"></i
            ></a>
          </li>
          <li class="nav-item drop-direction dropdown">
            <a
              class="nav-link"
              href="#"
              id="navbarDropdownMenuLink"
              role="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              <i class="fas fa-plus-circle fa-2x"></i>
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
              <li role="presentation">
                <header class="dropdown-header">Add items</header>
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >User</a
                >
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >Device</a
                >
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >Driver</a
                >
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >Geofence</a
                >
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >Alert</a
                >
              </li>
              <li role="presentation">
                <a role="menuitem" href="#" target="_self" class="dropdown-item"
                  >Event</a
                >
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      isDark: true,
    };
  },
  methods: {
    dock($event) {
      //screen width and height
      let browserWidth = window.innerWidth;
      let browserHeight = window.innerHeight;

      //mouse coords
      let sX = event.screenX;
      let sY = $event.screenY;

      //elements to dock
      // eslint-disable-next-line no-undef
      let nav = $(".nav-menu")[0];
      // eslint-disable-next-line no-undef
      let workspace = $(".ws-panel")[0];

      let dFromRight = browserWidth - sX;
      let dFromLeft = sX;
      let dFromBottom = browserHeight - sY;
      let dFromTop = sY;

      if (
        dFromRight < dFromLeft &&
        dFromRight < dFromTop &&
        dFromRight < dFromBottom
      ) {
        nav.className = "nav-menu nav-menu-right nav-menu-top nav-menu-y";
      } else if (
        dFromLeft < dFromRight &&
        dFromLeft < dFromTop &&
        dFromLeft < dFromBottom
      ) {
        nav.className = "nav-menu nav-menu-left nav-menu-top nav-menu-y";
      } else if (
        dFromTop < dFromRight &&
        dFromTop < dFromLeft &&
        dFromTop < dFromBottom
      ) {
        nav.className = "nav-menu nav-menu-top nav-menu-x";
      } else if (
        dFromBottom < dFromRight &&
        dFromBottom < dFromLeft &&
        dFromBottom < dFromTop
      ) {
        nav.className = "nav-menu nav-menu-bottom nav-menu-x";
      }
      this.checkPositions(nav, workspace);
    },
    changeLang(lang) {
      // eslint-disable-next-line no-undef
      let html = $("html");
      let prev = html.attr("dir");
      console.log(prev);
      if (lang === "en") {
        html.attr("dir", "ltr");
        html.attr("lang", "en");
      } else if (lang === "ar") {
        html.attr("dir", "rtl");
        html.attr("lang", "ar");
      }
      if (prev !== html.attr("dir")) {
        // eslint-disable-next-line no-undef
        let nav = $(".nav-menu")[0];
        // eslint-disable-next-line no-undef
        let workspace = $(".ws-panel")[0];
        if (nav.classList.contains("nav-menu-right")) {
          nav.classList.remove("nav-menu-right");
          nav.classList.add("nav-menu-left");
        } else if (nav.classList.contains("nav-menu-left")) {
          nav.classList.remove("nav-menu-left");
          nav.classList.add("nav-menu-right");
        }
        if (workspace.classList.contains("ws-panel-right")) {
          workspace.classList.remove("ws-panel-right");
          workspace.classList.add("ws-panel-left");
        } else if (workspace.classList.contains("ws-panel-left")) {
          workspace.classList.remove("ws-panel-left");
          workspace.classList.add("ws-panel-right");
        }

        this.checkPositions(nav, workspace);
      }
    },
    checkPositions(nav, workspace) {
      // eslint-disable-next-line no-undef
      let dDown = $(".drop-direction");
      workspace.classList.remove(
        "ws-panel-right-menu",
        "ws-panel-left-menu",
        "ws-panel-top-menu",
        "ws-panel-bottom-menu"
      );
      for (let i = 0; i < dDown.length; i++) {
        dDown[i].classList.remove("dropup", "dropdown", "dropstart", "dropend");
      }

      let { navPosition: navPosition, wsPosition: wsPosition } =
        this.getPositions(nav, workspace);

      if (navPosition === "top") {
        for (let i = 0; i < dDown.length; i++) {
          dDown[i].classList.add("dropdown");
        }
        if (wsPosition !== "bottom") {
          workspace.classList.add("ws-panel-top-menu");
        }
      } else if (navPosition === "bottom") {
        for (let i = 0; i < dDown.length; i++) {
          dDown[i].classList.add("dropup");
        }
        if (wsPosition !== "top") {
          workspace.classList.remove("ws-panel-top", "ws-panel-top-menu");
          workspace.classList.add("ws-panel-bottom-menu", "ws-panel-bottom");
        }
      } else if (navPosition === "right") {
        for (let i = 0; i < dDown.length; i++) {
          dDown[i].classList.add("dropstart");
        }
        if (wsPosition !== "left") {
          workspace.classList.add("ws-panel-right-menu");
        }
      } else if (navPosition === "left") {
        for (let i = 0; i < dDown.length; i++) {
          dDown[i].classList.add("dropend");
        }
        if (wsPosition !== "right") {
          workspace.classList.add("ws-panel-left-menu");
        }
      }
    },
    getPositions(nav, workspace) {
      let navPosition, wsPosition;
      if (
        nav.classList.contains("nav-menu-top") &&
        nav.classList.contains("nav-menu-x")
      ) {
        navPosition = "top";
      } else if (
        nav.classList.contains("nav-menu-bottom") &&
        nav.classList.contains("nav-menu-x")
      ) {
        navPosition = "bottom";
      } else if (nav.classList.contains("nav-menu-right")) {
        navPosition = "right";
      } else {
        navPosition = "left";
      }

      if (
        workspace.classList.contains("ws-panel-top") &&
        workspace.classList.contains("ws-panel-x")
      ) {
        wsPosition = "top";
      } else if (
        workspace.classList.contains("ws-panel-bottom") &&
        workspace.classList.contains("ws-panel-x")
      ) {
        wsPosition = "bottom";
      } else if (workspace.classList.contains("ws-panel-right")) {
        wsPosition = "right";
      } else {
        wsPosition = "left";
      }
      return { navPosition, wsPosition };
    },
    changeTheme(theme) {
      // eslint-disable-next-line no-undef
      let themeLink = $("#theme");
      themeLink.attr("href", "/css/themes/" + theme + ".css");
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
  z-index: 9;
}
.nav-menu-x {
  right: 0;
  left: 0;
  height: var(--nav-height);
}
.nav-menu-x > nav > .collapse > .nav-list {
  flex-direction: row-reverse !important;
}
.nav-menu-x > nav > .tools {
  margin-left: 15px;
  margin-right: 15px;
  text-align: start;
  width: 100%;
  display: flex;
  align-items: center;
}

.nav-menu-y {
  top: 0;
  bottom: 0;
  width: var(--nav-width);
}
.nav-menu-y > nav {
  height: 100%;
  display: block;
}
.nav-menu-y > nav > .collapse > ul {
  padding: 0;
}
.nav-menu-y > nav > .collapse > .nav-list {
  flex-direction: column;
}
.nav-menu-y > nav > .collapse > .nav-list > .d-table {
  display: block;
}
.nav-menu-y > nav > .collapse > .nav-list > .avatar > a > span {
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
  padding: 0.5rem;
}
.focus-none {
  box-shadow: none !important;
}
</style>
