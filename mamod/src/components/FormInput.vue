<!-- eslint-disable vuejs-accessibility/form-control-has-label -->
<template>
  <label class="form__label">
    <input
      class="form__input"
      required
      :type="type"
      :name="name"
      :placeholder="placeholder"
      :value="internalValue"
      v-model="internalValue"
      @input="updateValue"
    />
    <span>{{ error }}</span>
  </label>
</template>
<script>
export default {
  props: ["type", "name", "placeholder", "error", "value"],
  data() {
    return {
      internalValue: this.value,
    };
  },
  methods: {
    updateValue() {
      this.$emit("input", this.internalValue);
    },
  },
};
</script>
<style>
.form__label {
  position: relative;
}
.form__label span {
  position: absolute;
  font-size: 10px;
  color: #ed3e3e;
  top: 105%;
  left: 10px;
}
.form__input {
  width: 100%;
  padding: 10px;
  border-radius: 11px;
  border: 1px solid #e6e6eb;
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 19px;
}
.form__input::placeholder {
  color: #9292a0;
}
</style>
