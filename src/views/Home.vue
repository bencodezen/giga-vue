<script>
import { reactive, toRefs } from "vue";
import GigaVue from "@/components/GigaVue.vue";

export default {
  name: "Home",
  components: {
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
    <h1>{{ petName }}</h1>
    <GigaVue />
    <form v-if="showCreatePetForm" @submit.prevent>
      <label for="pet-name">Pet Name</label>
      <input type="text" id="pet-name" v-model="userInput" />
      <button @click="createPet">New Pet</button>
    </form>
  </div>
</template>
