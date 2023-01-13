<template>
  <div class="my-16">
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
  "tesla"
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
  "google"
];

function highlightSelected(cat: string) {
  if(cat!="" && cat!='all') {
  const logos = document.querySelectorAll(".lang-logo");
  logos.forEach((logo) => {
    logo.classList.remove("logo-selected");
  });
  document.querySelectorAll(`.${cat}-logo`).forEach((logo) => {
    logo.classList.add("logo-selected");
  });
}
else{
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
    };
  },
  methods: {
    clickCategory(cat: string) {
      this.$emit("clickCategory", cat);
      highlightSelected(cat);
    },
    next(index: number) {
      let button = document?.getElementsByClassName(
        "swiper-button-next"
      )[index] as HTMLElement;
      console.log("button: " ,button);
      button.click();
    },
    prev(index: number) {
      let button = document?.getElementsByClassName(
        "swiper-button-prev"
      )[index] as HTMLElement;
      button.click();
    },
  },
  mounted() {
    highlightSelected("all");
  },
});
</script>
