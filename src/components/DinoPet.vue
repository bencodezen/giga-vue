<script>
import { defineAsyncComponent } from "vue";

export default {
  components: {
    DinoAngry: defineAsyncComponent(() => import("./DinoAngry")),
    DinoHappy: defineAsyncComponent(() => import("./DinoHappy")),
    DinoSleep: defineAsyncComponent(() => import("./DinoSleep"))
  },
  props: {
    mood: {
      type: String,
      default: "Angry"
    }
  },
  data: () => ({
    innerMood: "Sleep"
  }),
  computed: {
    dinoMood() {
      return `Dino${this.mood}`;
    }
  },
  methods: {
    updatePetMood() {
      this.$emit("update-pet-mood", {
        mood: this.innerMood
      });
    }
  }
};
</script>

<template>
  <div :class="$style.wrapper">
    <component :is="dinoMood" />
    <button :class="$style.button" @click="updatePetMood">Update Mood</button>
  </div>
</template>

<style module>
.wrapper {
  position: relative;
}

.button {
  position: absolute;
  left: 10px;
  top: 50%;
}
</style>
