<template>
  <div class="my-16">
    <div class="graph_one">
      <img class="img_side" src="/log_one.png" alt="" />
      <table
        id="animations-example-6"
        class="charts-css column show-labels hide-data data-spacing-5 show-primary-axis"
      >
        <tbody>
          <tr>
            <th scope="row">Data</th>
            <td class="td_one"></td>
          </tr>
          <tr>
            <th scope="row">Business</th>
            <td class="td_two"></td>
          </tr>
          <tr>
            <th scope="row">Database</th>
            <td class="td_three"></td>
          </tr>
          <tr>
            <th scope="row">Coding</th>
            <td class="td_four"></td>
          </tr>
          <tr>
            <th scope="row">Cloud</th>
            <td class="td_five"></td>
          </tr>
        </tbody>
      </table>
      <img class="img_side" src="log_two.png" alt="" />
    </div>
    <h1 class="Software_heading">Softwares</h1>
    <div id="lang-wrapper">
      <swiper
        :grabCursor="true"
        :slideToClickedSlide="true"
        :centeredSlides="true"
        :modules="modules"
        :navigation="true"
        :slides-per-view="5"
        :loop="true"
        :breakpoints="{
          '1280': {
            slidesPerView: 8,
          },
        }"
      >
        <swiper-slide
          class="px-2 !mx-0 single-category"
          v-for="(cat, index) in catsFirstLine"
          :key="index"
        >
          <img
            @click="clickCategory(cat)"
            :class="`cursor-pointer max-h-16 category-img max-w-16 sm:max-h-18 sm:max-w-18 md:max-h-20 md:max-w-20 lg:max-h-24 lg:max-w-24 xl:max-h-28 xl:max-w-28 lang-logo ${cat}-logo`"
            :alt="cat"
            :src="`/logos/${cat}.png`"
          />
          <p class="category-name">{{ cat }}</p>
        </swiper-slide>
      </swiper>
    </div>
    <div id="swiper-buttons" class="flex justify-between mt-4 mx-4">
      <button @click="prev(0)">
        <svg
          class="prev w-12 fill-gray hover:fill-mikado"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <path d="M16 8v-4l8 8-8 8v-4h-16l8-8h8z" />
        </svg>
      </button>
      <button @click="next(0)">
        <svg
          class="w-12 fill-gray hover:fill-mikado"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <path d="M16 8v-4l8 8-8 8v-4h-16l8-8h8z" />
        </svg>
      </button>
    </div>
    <h1 class="data_heading">Data Skills</h1>
    <div id="lang-wrapper">
      <swiper
        :grabCursor="true"
        :slideToClickedSlide="true"
        :centeredSlides="true"
        :modules="modules"
        :navigation="true"
        :slides-per-view="5"
        :loop="true"
        :breakpoints="{
          '1280': {
            slidesPerView: 8,
          },
        }"
      >
        <swiper-slide
          class="px-2 !mx-0 single-category"
          v-for="(cat, index) in catsSecondLine"
          :key="index"
        >
          <img
            @click="clickCategory(cat)"
            :class="`cursor-pointer max-h-16 mt-10 category-img max-w-16 sm:max-h-18 sm:max-w-18 md:max-h-20 md:max-w-20 lg:max-h-24 lg:max-w-24 xl:max-h-28 xl:max-w-28 lang-logo ${cat}-logo`"
            :alt="cat"
            :src="`/logos/${cat}.png`"
          />
          <p class="category-name">{{ cat }}</p>
        </swiper-slide>
      </swiper>
    </div>
    <div id="swiper-buttons" class="flex justify-between mt-4 mx-4">
      <button @click="prev(1)">
        <svg
          class="prev w-12 fill-gray hover:fill-mikado"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <path d="M16 8v-4l8 8-8 8v-4h-16l8-8h8z" />
        </svg>
      </button>
      <button @click="next(1)">
        <svg
          class="w-12 fill-gray hover:fill-mikado"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <path d="M16 8v-4l8 8-8 8v-4h-16l8-8h8z" />
        </svg>
      </button>
    </div>
  </div>
</template>

<style>
.graph_one {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0px 10px;
}
.img_side {
  width: 50px;
  height: 50px;
}
.Software_heading {
  font-size: 16px;
  margin-top: -10px;
  margin-bottom: 10px;
  color: #fff;
  text-decoration: underline;
}
.data_heading {
  font-size: 16px;
  margin-top: 27px;
  margin-bottom: -37px;
  color: #fff;
  text-decoration: underline;
}
#lang-wrapper {
  mask-image: linear-gradient(
    to right,
    transparent,
    #0c173c 5%,
    #0c173c 95%,
    transparent 100%
  );
}
.swiper-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  align-self: center;
}
.swiper-button-prev,
.swiper-button-next {
  display: none;
}
.prev {
  transform: rotate(180deg);
}

@media all and (max-width: 640px) {
  #swiper-buttons {
    display: none !important;
  }
}
.lang-logo {
  opacity: 0.5;
}
.lang-logo:hover {
  opacity: 1;
}
.logo-selected {
  opacity: 1;
}

.swiper-slide.single-category {
  display: flex;
  flex-direction: column;
}

.single-category p.category-name {
  color: wheat;
}
graph_one {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

#animations-example-6 {
  height: 100px;
  max-width: 350px;
  margin: 0 auto;
}
#animations-example-6 td {
  background-image: linear-gradient(
    45deg,
    #beffe7,
    #f8beff,
    #fff1be,
    #beecff,
    #e5d3ff,
    #ffd3d3
  );
  background-size: 600%;
  animation: gradient-animation 3s linear infinite alternate;
}
@keyframes gradient-animation {
  0% {
    background-position: 0%;
  }
  100% {
    background-position: 100%;
  }
}
.graph_one {
  margin-top: -50px;
  margin-bottom: 28px;
}
.graph_one th {
  color: #fff;
  margin-top: 3px;
  font-style: italic;
  font-weight: 200;
  font-size: 11px;
}
.graph_one tr {
  display: flex !important;
  flex-direction: column-reverse !important;
  width: 42px;
  margin: 7px;
}
.graph_one td {
  border: 2px solid #fff;
}
.graph_one .td_one {
  height: 45px;
}
.graph_one .td_two {
  height: 65px;
}
.graph_one .td_three {
  height: 37px;
}
.graph_one .td_four {
  height: 55px;
}
.graph_one .td_five {
  height: 27px;
}
.graph_one tbody {
  display: flex !important;
}
</style>

<script lang="ts">
import { defineComponent } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Keyboard, FreeMode, Navigation } from "swiper";

// Import Swiper styles
import "swiper/css";

const CATEGORIESFIRSTLINE = [
  "wind",
  "geothermal",
  "renewable",
  "fossil",
  "amazon",
  "apple",
  "microsoft",
  "tesla",
];
const CATEGORIESSECONDLINE = [
  "telecom",
  "uv",
  "water",
  "solar panel",
  "flood",
  "earth",
  "solar",
  "electricity",
  "google",
];

function highlightSelected(cat: string) {
  if (cat != "" && cat != "all") {
    const logos = document.querySelectorAll(".lang-logo");
    logos.forEach((logo) => {
      logo.classList.remove("logo-selected");
    });
    document.querySelectorAll(`.${cat}-logo`).forEach((logo) => {
      logo.classList.add("logo-selected");
    });
  } else {
    const logos = document.querySelectorAll(".lang-logo");
    logos.forEach((logo) => {
      logo.classList.add("logo-selected");
    });
  }
}

export default defineComponent({
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      catsFirstLine: CATEGORIESFIRSTLINE,
      catsSecondLine: CATEGORIESSECONDLINE,
      modules: [Keyboard, Navigation, FreeMode],
      navValue: undefined,
    };
  },
  methods: {
    clickCategory(cat: string) {
      this.$emit("clickCategory", cat);
      highlightSelected(cat);
    },
    next(index) {
      let button = document?.getElementsByClassName("swiper-button-next")[
        index
      ] as HTMLElement;
      console.log("button: ", button);
      button.click();
    },
    prev(index) {
      let button = document?.getElementsByClassName("swiper-button-prev")[
        index
      ] as HTMLElement;
      button.click();
    },
  },
  mounted() {
    highlightSelected("all");
    setTimeout(() => {
      this.navValue = true;
    }, 2000);
  },
});
</script>
