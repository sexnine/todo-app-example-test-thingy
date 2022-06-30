<template>
  <div
    ref="el"
    class="test-anim cursor-pointer rounded-md bg-red-500 py-2 px-4 text-xl text-white"
    @click="remove"
  >
    {{ todo }}
  </div>
</template>

<script lang="ts">
  import { defineComponent } from "vue";

  export default defineComponent({
    props: {
      todo: {
        type: String,
        required: true,
      },
    },
    emits: ["remove"],
    mounted() {
      setTimeout(
        () => (this.$refs.el as Element).classList.remove("test-anim"),
        500
      );
      console.log("Todo Mounted: " + this.todo);
    },
    methods: {
      remove() {
        (this.$refs.el as Element).classList.add("test-anim-2");

        setTimeout(() => {
          (this.$refs.el as Element).classList.remove("test-anim-2");
          this.$emit("remove");
        }, 500);
      },
    },
  });
</script>

<style scoped>
  @keyframes push-anim {
    0% {
      margin-top: -44px;
      opacity: 0%;
    }
    100% {
      margin-top: 0px;
      opacity: 100%;
    }
  }

  .test-anim {
    animation-name: push-anim;
    animation-duration: 0.3s;
    animation-iteration-count: 1;
  }

  @keyframes fly-anim {
    0% {
      margin-top: 0px;
      margin-left: 0px;
      margin-right: 0px;
    }
    100% {
      margin-top: -52px;
      margin-left: -100vw;
      margin-right: 100vw;
    }
  }

  .test-anim-2 {
    animation-name: fly-anim;
    animation-duration: 0.5s;
    animation-iteration-count: 1;
  }
</style>
