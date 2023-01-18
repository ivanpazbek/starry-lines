<template>
  <vue-final-modal
    v-slot="{ params, close }"
    v-bind="$attrs"
    v-model="showModalModel"
    classes="flex justify-center items-center"
    content-class="relative flex flex-col max-h-full mx-4 p-4 border rounded bg-night-blue text-white"
    @closed="closed"
    :transition="{
      'enter-active-class': 'transition duration-350 ease-in-out transform',
      'enter-class': 'translate-y-full',
      'enter-to-class': 'translate-y-0',
      'leave-active-class': 'transition duration-350 ease-in-out transform',
      'leave-to-class': 'translate-y-full',
      'leave-class': 'translate-y-0',O
    }"
  >
    <div
      class="flex-grow overflow-y-auto text-left sm: px-6 xl:px-32 max-w-lg lg:max-w-2xl xl:max-w-3xl 2xl:max-w-7xl"
    >
      <slot v-bind:params="params"></slot>
      <h1 v-if="isPrerender" class="text-3xl">
        Most starred lines of code on GitHub
      </h1>
      <h2 class="text-2xl mt-4 font-bold text-mikado">x
        Welcome to Julian Passebecq apps
      </h2>

      <h2 class="text-xl mt-6">- Tutorials</h2>
      <div class="ml-2 md:ml-4">
        <h3 class="mt-2">it is a Vue js visual interface</h3>

        <h3>
          If you want to reach me
          <a
            href="https://www.linkedin.com/"
            class="no-underline hover:underline text-mikado"
            >Linkedin.</a
          >
        </h3>
      </div>
    </div>
    <button
      @click="closed"
      class="absolute top-0 right-2 mt-2 mr-2 text-2xl sm:text-base"
    >
      X
    </button>
  </vue-final-modal>
</template>

<script>
import { VueFinalModal, ModalsContainer } from "vue-final-modal";

export default {
  props: {
    showModal: {
      type: Boolean,
      required: true,
    },
    isPrerender: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    showModalModel: {
      get() {
        return this.showModal;
      },
      set(value) {
        if (value === false) {
          this.closed();
        }
      },
    },
  },
  name: "Readme",
  components: {
    VueFinalModal,
    ModalsContainer,
  },
  methods: {
    closed() {
      this.$emit("close");
    },
  },
};
</script>
