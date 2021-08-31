<template>
  <div
    class="ws-panel ws-panel-bottom ws-panel-left ws-panel-x"
    @mouseenter="mouseEnter()"
    @mouseleave="mouseLeave()"
  >
    <b-row class="w-100 mx-1 d-flex">
      <div class="d-flex text-start mb-3 mt-2">
        <a draggable="true" @dragend="dock($event)" class="dark"
          ><i class="fas fa-th fa-lg"></i
        ></a>
        <b class="mx-3"
          >Workspaces&nbsp;&nbsp;&nbsp;&nbsp;{{ workspaces.length }}</b
        >
        <div class="text-end w-100">
          <a
            :style="locked === true ? 'color:red' : 'color: blue'"
            @click="locked = !locked"
            href="#"
            ><i class="fas fa-lock fa-lg"></i
          ></a>
        </div>
      </div>
      <div class="cards-container">
        <div class="plus-container">
          <b-card bg-variant="light" class="plus-card">
            <i class="fas fa-plus"></i>
          </b-card>
        </div>
        <div class="scroll-button">
          <b-button @click="scroll('l')" class="focus-none h-100" variant="none"
            ><i class="fas fa-chevron-left fa-2x"></i
          ></b-button>
        </div>
        <div class="scrolling-wrapper">
          <b-card
            bg-variant="dark"
            text-variant="white"
            no-body
            class="mx-3 workspace-card scrolling-card"
            v-for="(item, index) in workspaces"
            :key="index"
          >
            <b-card-img
              :src="item.img_url"
              alt="Image"
              class="rounded-0 h-0"
            ></b-card-img>
            <b-card-text class="m-bot-1"> {{ item.name }} </b-card-text>
          </b-card>
        </div>
        <div class="scroll-button">
          <b-button @click="scroll('r')" class="focus-none h-100" variant="none"
            ><i class="fas fa-chevron-right fa-2x"></i
          ></b-button>
        </div>
      </div>
    </b-row>
  </div>
</template>

<script>
import JQuery from "jquery";
let $ = JQuery;
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
    },
    enterAction() {
      if (!this.locked) {
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
      if ($(".ws-panel")[0].classList.contains("ws-panel-y")) {
        $(".scrolling-wrapper")[0].style.setProperty(
          "max-height",
          screen.height * 0.55 + "px"
        );
      }
    },
    leaveAction() {
      if (!this.locked) {
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
      window.test();
      // let screen_width = screen.width;
      let screen_height = screen.height;
      // let sX = event.screenX;
      let sY = $event.screenY;
      console.log(sY);
      let el = $(".ws-panel")[0];
      let nav = $(".nav-menu")[0];
      console.log(nav.offsetHeight);
      if (sY < screen_height * 0.35) {
        el.classList.remove("ws-panel-bottom");
        el.style.removeProperty("bottom");
        el.classList.add("ws-panel-top");
        if (nav.classList.contains("nav-menu-top"))
          el.style.setProperty("top", nav.offsetHeight + "px");
      } else if (sY > screen_height * 0.65) {
        el.classList.remove("ws-panel-top");
        el.style.removeProperty("top");
        el.classList.add("ws-panel-bottom");
        if (nav.classList.contains("nav-menu-bottom"))
          el.style.setProperty("bottom", nav.offsetHeight + "px");
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
.ws-panel-top {
  top: 0px;
}
.ws-panel-right {
  right: 0px;
}
.ws-panel-left {
  left: 0px;
}
.ws-panel {
  position: fixed;
  opacity: 0.7;
}
.ws-panel-x {
  width: 100%;
}
.ws-panel-y {
  height: 100%;
}
.ws-panel-y > div {
  height: 100%;
  flex-direction: column;
}
.ws-panel-y > div > .cards-container > .scrolling-wrapper {
  display: flex;
  flex-direction: column;
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
}
.cards-container {
  display: flex;
}
.ws-panel {
  background-color: gray;
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
  overflow-x: scroll;
  overflow-y: hidden;
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
</style>
