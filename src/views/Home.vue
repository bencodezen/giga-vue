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
      <DinoPet :class="$style.dinopet" v-if="petName" />
      <h2>{{ petName }}</h2>
    </section>
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
}

.dinopet {
  max-width: 120px;
  position: absolute;
  left: 250px;
  top: 210px;
}
</style>
