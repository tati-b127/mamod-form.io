<template>
  <div class="form__select-block">
    <select class="form__select" v-model="selected" @change="updateSelect" name="role" required>
      <option class="form__option" disabled value="0">Должность</option>
      <option v-for="position in positions" :key="position.value" :value="position.value">
        {{ position.name }}
      </option>
    </select>
    <span>{{ error }}</span>
  </div>
</template>
<script>
export default {
  data: function () {
    return {
      selected: this.value,
    };
  },
  props: ["positions", "error", "value"],
  methods: {
    updateSelect() {
      this.$emit("input", this.selected);
    },
  },
};
</script>
<style>
.form__select-block {
  position: relative;
  grid-row: 3 / span 1;
  grid-column: 2 / span 1;
}
.form__select-block span {
  position: absolute;
  font-size: 10px;
  color: #ed3e3e;
  top: 105%;
  left: 10px;
}
.form__select {
  width: 100%;
  padding: 10px;
  font-size: 14px;
  background-color: #fff;
  border-radius: 11px;
  color: #000;
  border: 1px solid #e6e6eb;
}
.form__option {
  font-size: 14px;
  padding: 10px;
  background-color: #fff;
}
option:first-child {
  color: #929292;
}
</style>
