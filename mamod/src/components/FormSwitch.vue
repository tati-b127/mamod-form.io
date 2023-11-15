<template>
  <div class="form__switch">
    <label class="switch">
      <input
        type="checkbox"
        :name="name"
        :value="checkedValue"
        v-model="checkedValue"
        @change="updateValue"
      />
      <span class="slider round"></span>
    </label>
    <div class="block__descr">
      <p class="descr">Хотите чтобы Ваш профиль видели другие участники платформы?</p>
      <p class="des">Включает профиль для просмотра другими пользователями по ссылке</p>
    </div>
  </div>
</template>
<script>
export default {
  props: ["name", "value"],
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
.switch {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 20px;
}
.switch input {
  display: none;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 20px;
  width: 20px;
  left: 0px;
  bottom: 0px;
  border: 0.5px solid #d9d9d9;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #3586ff;
}

input:focus + .slider {
  box-shadow: 0 0 1px #3586ff;
}

input:checked + .slider:before {
  -webkit-transform: translateX(20px);
  -ms-transform: translateX(20px);
  transform: translateX(20px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
.descr {
  font-size: 16px;
  font-style: normal;
  font-weight: 500;
  line-height: 19px;
  margin-bottom: 10px;
}
.des {
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 19px;
  color: #696977;
}
.form__switch {
  display: flex;
  margin-bottom: 30px;
}
.block__descr {
  padding-left: 5px;
  display: flex;
  flex-direction: column;
}
</style>
