<script>
import { reactive, toRefs } from "vue";
import DinoPet from "@/components/DinoPet.vue";
import GigaVue from "@/components/GigaVue.vue";

export default {
  name: "Home",
  components: {
    DinoPet,
    GigaVue
  },
  setup() {
    const state = reactive({
      petName: "",
      userInput: "",
      showCreatePetForm: true
    });

    const createPet = () => {
      state.petName = state.userInput;
      state.showCreatePetForm = false;
    };

    return {
      ...toRefs(state),
      createPet
    };
  }
};
</script>

<template>
  <div class="home">
    <h1>Giga-Vue</h1>
    <section :class="$style.wrapper">
      <GigaVue />
      <DinoPet v-if="petName" :class="$style.dinopet" />
    </section>
    <h2>{{ petName }}</h2>

    <form v-if="showCreatePetForm" @submit.prevent>
      <label for="pet-name">Pet Name</label>
      <input type="text" id="pet-name" v-model="userInput" />
      <button @click="createPet">New Pet</button>
    </form>
  </div>
</template>

<style module>
.wrapper {
  position: relative;
  display: flex;
  justify-content: center;
}

.dinopet {
  position: absolute;
  max-width: 120px;
  width: 100%;
  top: 50%;
  transform: translateY(-45%);
  z-index: 1;
}
</style>
