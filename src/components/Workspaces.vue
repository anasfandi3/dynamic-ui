<template>
  <div class="ws-panel ws-panel-bottom ws-panel-x">
    <div class="w-100 row mx-1 d-flex">
      <div class="ws-top-bar">
        <a draggable="true" @dragend="dock($event)" class="dark"
          ><i class="fas fa-th fa-lg"></i
        ></a>
        <b class="mx-3"
          >Workspaces&nbsp;&nbsp;&nbsp;&nbsp;{{ workspaces.length }}</b
        >
        <div class="text-end w-100">
          <a @click="lock()" href="#"
            ><i class="lock-icon fas fa-unlock fa-lg"></i
          ></a>
        </div>
      </div>
      <div class="cards-container d-flex justify-content-between">
        <div class="plus-container">
          <div bg-variant="light" class="card plus-card bg-light">
            <div class="card-body">
              <i class="fas fa-plus"></i>
            </div>
          </div>
        </div>
        <div class="scroll-button">
          <button @click="scroll('l')" class="focus-none btn-none btn h-100">
            <i class="fas fa-chevron-left fa-2x"></i>
          </button>
        </div>
        <div class="scrolling-wrapper">
          <div
            class="card mx-3 workspace-card scrolling-card bg-dark text-white"
            v-for="(item, index) in workspaces"
            :key="index"
          >
            <img
              :src="item.img_url"
              alt="Image"
              class="rounded-0 card-img h-0"
            />
            <p class="card-text m-bot-1">{{ item.name }}</p>
          </div>
        </div>
        <div class="scroll-button">
          <button @click="scroll('r')" class="focus-none btn btn-none h-100">
            <i class="fas fa-chevron-right fa-2x"></i>
          </button>
        </div>
      </div>
      <div
        @mouseenter="mouseEnter()"
        @mouseleave="mouseLeave()"
        class="hover-bar hover-bar-bottom hover-bar-x"
      >
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars

let $ = require("jquery");
export default {
  name: "Workspaces",
  data() {
    return {
      hover: false,
      locked: false,
      workspaces: [
        {
          name: "workspace1",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace2",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace3",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace4",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace5",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace6",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
        {
          name: "workspace7",
          img_url: "https://picsum.photos/400/400/?image=20",
        },
      ],
    };
  },
  methods: {
    hoverAction1() {
      var elementsArray = document.getElementsByClassName("workspace-card");
      var plusCard = document.getElementsByClassName("plus-card");
      plusCard[0].classList.add("card-open");
      plusCard[0].classList.add("plus-card-open");
      for (let i = 0; i < elementsArray.length; i++) {
        elementsArray[i].classList.add("card-open");
        elementsArray[i].children[0].classList.remove("h-0");
        elementsArray[i].children[1].classList.add("card-text");
      }
    },
    hoverOutAction1() {
      if (!this.locked) {
        var elementsArray = document.getElementsByClassName("workspace-card");
        var plusCard = document.getElementsByClassName("plus-card");
        plusCard[0].classList.remove("card-open");
        plusCard[0].classList.remove("plus-card-open");
        for (let i = 0; i < elementsArray.length; i++) {
          elementsArray[i].classList.remove("card-open");
          elementsArray[i].children[0].classList.add("h-0");
          elementsArray[i].children[1].classList.add("m-bot-1");
        }
      }
    },
    scroll(dir) {
      if ($(".ws-panel-x")[0]) {
        if (dir === "l") {
          $(".scrolling-wrapper").animate(
            {
              scrollLeft: "-=" + 250 + "px",
            },
            500
          );
        } else if (dir === "r") {
          $(".scrolling-wrapper").animate(
            {
              scrollLeft: "+=" + 250 + "px",
            },
            500
          );
        }
      } else if ($(".ws-panel-y")) {
        if (dir === "l") {
          $(".scrolling-wrapper").animate(
            {
              scrollTop: "-=" + 180 + "px",
            },
            500
          );
        } else if (dir === "r") {
          $(".scrolling-wrapper").animate(
            {
              scrollTop: "+=" + 180 + "px",
            },
            500
          );
        }
      }
    },
    enterAction(lockAction = false) {
      if (!this.locked || lockAction) {
        let duration = 100;
        $(".workspace-card").animate(
          {
            height: 160 + "px",
          },
          duration
        );
        $(".rounded-0").animate(
          {
            height: 130 + "px",
          },
          duration
        );
        $(".plus-card").animate(
          {
            lineHeight: 140 + "px",
            height: 160 + "px",
          },
          duration
        );
      }
    },
    leaveAction(unlockAction = false) {
      if (!this.locked || unlockAction) {
        let duration = 100;
        $(".workspace-card").animate(
          {
            height: 64 + "px",
          },
          duration
        );
        $(".rounded-0").animate(
          {
            height: 0 + "px",
          },
          duration
        );
        $(".plus-card").animate(
          {
            lineHeight: 0 + "px",
            height: 64 + "px",
          },
          duration
        );
      }
    },
    mouseEnter() {
      let x = this;
      setTimeout(function () {
        x.enterAction();
      }, 100);
    },
    mouseLeave() {
      let x = this;
      setTimeout(function () {
        x.leaveAction();
      }, 100);
    },
    dock($event) {
      //screen width and height
      let browser_width = window.innerWidth;
      let browser_height = window.innerHeight;

      //mouse coords
      let sX = event.screenX;
      let sY = $event.screenY;

      //elements to dock
      let nav = $(".nav-menu")[0];
      let workspace = $(".ws-panel")[0];

      let dFromRight = browser_width - sX;
      let dFromLeft = sX;
      let dFromBottom = browser_height - sY;
      let dFromTop = sY;

      if (
        dFromRight < dFromLeft &&
        dFromRight < dFromTop &&
        dFromRight < dFromBottom
      ) {
        workspace.className = "ws-panel ws-panel-right ws-panel-top ws-panel-y";
      } else if (
        dFromLeft < dFromRight &&
        dFromLeft < dFromTop &&
        dFromLeft < dFromBottom
      ) {
        workspace.className = "ws-panel ws-panel-left ws-panel-top ws-panel-y";
      } else if (
        dFromTop < dFromRight &&
        dFromTop < dFromLeft &&
        dFromTop < dFromBottom
      ) {
        workspace.className = "ws-panel ws-panel-top ws-panel-x";
      } else if (
        dFromBottom < dFromRight &&
        dFromBottom < dFromLeft &&
        dFromBottom < dFromTop
      ) {
        workspace.className = "ws-panel ws-panel-bottom ws-panel-x";
      }
      this.checkPositions(nav, workspace);
      if ($(".ws-panel")[0].classList.contains("ws-panel-y")) {
        $(".scrolling-wrapper")[0].style.setProperty(
          "max-height",
          window.innerHeight * 0.5 + "px"
        );
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
      let hoverBar = $(".hover-bar")[0];
      if (wsPosition === "top") {
        hoverBar.className = "hover-bar hover-bar-top hover-bar-x";
      } else if (wsPosition === "bottom") {
        hoverBar.className = "hover-bar hover-bar-bottom hover-bar-x";
      } else if (wsPosition === "right") {
        hoverBar.className = "hover-bar hover-bar-right hover-bar-y";
      } else if (wsPosition === "left") {
        hoverBar.className = "hover-bar hover-bar-left hover-bar-y";
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
    lock() {
      this.locked = !this.locked;
      let icon = $(".lock-icon")[0];
      if (this.locked === true) {
        icon.classList.remove("fa-unlock");
        icon.classList.add("fa-lock");
        this.enterAction(true);
      } else {
        icon.classList.remove("fa-lock");
        icon.classList.add("fa-unlock");
        this.leaveAction(true);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ws-panel-bottom {
  bottom: 0px;
}
.ws-panel-bottom-menu {
  bottom: var(--nav-height) !important;
}
.ws-panel-top {
  top: 0px;
}
.ws-panel-top-menu {
  top: var(--nav-height) !important;
}
.ws-panel-right {
  right: 0px;
}
.ws-panel-right-menu {
  right: var(--nav-width) !important;
}
.ws-panel-left {
  left: 0px;
}
.ws-panel-left-menu {
  left: var(--nav-width) !important;
}
.ws-panel {
  position: fixed;
  background-color: rgba(128, 128, 128, 0.7);
}
.ws-panel-x {
  right: 0;
  left: 0;
}
.ws-panel-y {
  top: 0;
  bottom: 0;
}
.ws-panel-y > div {
  height: 100%;
  flex-direction: column;
}
.ws-panel-y > div > .cards-container > .scrolling-wrapper {
  display: flex;
  flex-direction: column;
  overflow-x: hidden;
  overflow-y: scroll;
}
.ws-panel-y > div > .cards-container > .plus-container > .plus-card {
  line-height: 140px !important;
  height: 160px !important;
}
.ws-panel-y > div > .cards-container > .scroll-button > button > * {
  transform: rotate(90deg);
}
.ws-panel-y > div > .cards-container {
  flex-direction: column !important;
}
.ws-panel-x > div > .cards-container {
  flex-direction: row !important;
  margin-bottom: 1rem;
  margin-top: 1rem;
}
.ws-panel-x > div > .cards-container > .scrolling-wrapper {
  overflow-x: scroll;
  overflow-y: hidden;
}
.cards-container {
  display: flex;
}
.card-open {
  height: 160px;
}

.workspace-card {
  width: 200px;
  margin-left: auto;
  margin-right: auto;

  margin-bottom: 10px;
}

.plus-card-open {
  line-height: 140px;
}
.plus-card {
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 10px;
  position: relative;
  width: 160px;
}

.lock:focus {
  color: red;
}

.scrolling-wrapper {
  white-space: nowrap;
}
.scrolling-card {
  display: inline-block;
}

.scrolling-wrapper {
  -webkit-overflow-scrolling: touch;
}
.scrolling-wrapper::-webkit-scrollbar {
  display: none;
}
.h-0 {
  height: 0px;
}
.m-bot-1 {
  margin-bottom: 1rem !important;
}
.focus-none:focus {
  box-shadow: none;
}
.dark {
  color: var(--bs-dark);
}
.hover-bar {
  position: absolute;
  padding: 3px;
  display: flex;
}
.hover-bar > div {
  background: var(--bs-dark);
  border-radius: 30px;
}
.hover-bar-x {
  right: 0;
  left: 0;
  height: 20px;
}
.hover-bar-bottom {
  bottom: 0;
}
.hover-bar-left {
  left: 0;
}
.hover-bar-right {
  right: 0;
}
.hover-bar-x > div {
  height: 10px;
  width: 100%;
  margin-left: 15rem;
  margin-right: 15rem;
}
.hover-bar-y {
  top: 0;
  bottom: 0;
  width: 20px;
}
.hover-bar-y > div {
  width: 10px;
  margin-top: 15rem;
  margin-bottom: 15rem;
}
.ws-top-bar {
  display: flex;
  text-align: start;
  margin-bottom: 1rem;
  margin-top: 0.5rem;
}
.ws-top-bar > a {
  z-index: 9;
}
</style>
