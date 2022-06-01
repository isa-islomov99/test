<template>
  <div
    :style="{
      gridColumn: `${items.gridColumn}`,
      gridRow: `${items.gridRow}`,
      padding: '0 5px',
    }"
    :class="{ display: items.cssStyle }"
  >
    <label class="form-label">{{ items.label }}</label>
    <select
      v-if="items.type === 'select'"
      class="form-select custom_input"
      :required="items.isRequired"
      aria-label="Default select example"
    >
      <option value=""></option>
      <option v-for="option in items.data" :key="option.id" :value="option.id">
        {{ option.name }}
      </option>
    </select>
    <div v-else class="input-group input-group-sm mb-2">
      <input
        :type="items.type"
        :placeholder="items.placeholder"
        :required="items.isRequired"
        :maxlength="items.maxLength"
        :pattern="items.mask"
        :class="[
          'form-control',
          'custom_input',
          { 'text-center': items.textAlign },
          { valid_input: validationInput },
        ]"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-sm"
        @input="handleInput"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      validationInput: false,
    };
  },

  methods: {
    handleInput(e) {
      if (
        this.items.minLength &&
        e.target.value.length < this.items.minLength
      ) {
        this.validationInput = true;
      } else this.validationInput = false;
    },
  },
};
</script>

<style  scoped>
.display {
  display: none;
}
.custom_input {
  height: 33px;
}
.valid_input:focus {
  border: 3px solid red;
}
</style>