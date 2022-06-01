<template>
  <div class="app">
    <div class="container">
      <h3 class="text-center mt-4">{{ formData[0].addTitle }}</h3>
      <form
        @submit.prevent
        v-for="form in formData"
        :key="form.id"
        class="form_grid mt-4"
      >
        <FormInputs
          v-for="input in form.elements"
          :key="input.id"
          :items="input"
        />
      </form>
    </div>
  </div>
</template>

<script>
import { formData } from "@/data.js";
import FormInputs from "@/components/FormInputs.vue";

export default {
  name: "App",
  components: {
    FormInputs,
  },

  data() {
    return {
      formData: formData,
    };
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.form_grid {
  display: grid;
  grid-template-columns: repeat(1fr, 24);
  grid-auto-rows: repeat(1fr, 3);
}
</style>
