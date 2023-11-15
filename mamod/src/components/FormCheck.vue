<template>
  <label class="label-check">
    <span class="descr-agree">
      Регистрируясь, Вы соглашаетесь с <a href="#">политикой конфиденциальности</a> и обработкой
      <a href="#">персональных данных</a>
    </span>
    <input
      type="checkbox"
      :name="name"
      :value="checkedValue"
      v-model="checkedValue"
      @change="updateValue"
    />
    <span class="checkmark"></span>
    <span class="error">{{ error }}</span>
  </label>
</template>
<script>
export default {
  props: ["name", "error", "value"],
  data() {
    return {
      checkedValue: this.value,
    };
  },
  methods: {
    updateValue() {
      console.log("upadate");
      this.$emit("input", this.checkedValue);
    },
  },
};
</script>

<style>
.descr-agree {
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 19px;
  /* padding-left: 16px; */
}
.descr-agree a {
  text-decoration: none;
  color: #3586ff;
}

.label-check {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-right: 50px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.label-check input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 17px;
  width: 19px;
  background-color: #ffffff;
  border: 1px solid #3586ff;
  border-radius: 5px;
  transition: background-color 0.3s ease-in;
}

.label-check:hover input ~ .checkmark {
  background-color: #f0f4ff;
}

.label-check input:checked ~ .checkmark {
  background-color: #3586ff;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.label-check input:checked ~ .checkmark:after {
  display: block;
}

.label-check .checkmark:after {
  left: 7px;
  top: 3px;
  width: 4px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
.error {
  position: absolute;
  font-size: 10px;
  color: #ed3e3e;
  top: 105%;
  left: 10px;
}
</style>
