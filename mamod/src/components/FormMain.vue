<template>
  <div class="container">
    <form class="form" @submit.prevent="submitForm" action="#" method="post">
      <h1 class="form__title">Регистрация</h1>
      <div class="form__block grid">
        <h2 class="form__subtitle">Заполните Ваши данные</h2>
        <FormInput
          type="text"
          name="name"
          placeholder="Имя"
          v-model="formData.username"
          :error="formErrors.errorUser"
        ></FormInput>
        <FormInput
          type="mail"
          name="email"
          placeholder="Email"
          v-model="formData.email"
          :error="formErrors.errorEmail"
        ></FormInput>
        <FormSelect
          :error="formErrors.errorRole"
          v-model="formData.role"
          :positions="positions"
        ></FormSelect>
        <FormInput
          type="password"
          name="password"
          placeholder="Пароль"
          v-model="formData.password"
          :error="formErrors.errorPass"
        ></FormInput>
        <FormInput
          type="password"
          name="confPassword"
          placeholder="Повторите пароль"
          v-model="formData.password_repeat"
          :error="formErrors.errorPassConf"
        ></FormInput>
      </div>
      <div class="form__block">
        <FormSwitch name="public" v-model="formData.public"></FormSwitch>
        <div class="form__block-agree">
          <FormCheck
            :error="formErrors.errorAgree"
            name="agree"
            v-model="formData.agree"
          ></FormCheck>
          <button class="form__btn" type="submit">Зарегестрироваться</button>
        </div>
      </div>
    </form>
    <!-- <div v-if="errosShow" class="form__error">
      <ul class="list">
        <li class="item" v-for="error in errorList" :key="error">
          {{ error }}
        </li>
      </ul>
    </div> -->
    <div v-if="registrationSuccess" class="form__success">
      <p class="form__message">Регистрация успешно завершена</p>
      <button class="form__btn" @click="closeMessage">Закрыть</button>
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";
import FormInput from "./FormInput.vue";
import FormSelect from "./FormSelect.vue";
import FormSwitch from "./FormSwitch.vue";
import FormCheck from "./FormCheck.vue";
import axios from "axios";
export default defineComponent({
  components: { FormInput, FormSelect, FormCheck, FormSwitch },
  data() {
    return {
      formData: {
        public: true,
        agree: true,
        username: "",
        role: 0,
        email: "",
        password: "",
        password_repeat: "",
      },
      positions: [
        { value: 1, name: "Программист" },
        { value: 2, name: "UX/UI дизайнер" },
        { value: 3, name: "Тестировщик" },
        { value: 4, name: "SEO специалист" },
      ],
      formErrors: {
        errorUser: "",
        errorEmail: "",
        errorRole: "",
        errorPass: "",
        errorPassConf: "",
        errorAgree: "",
      },
      errorList: [],
      registrationSuccess: false,
      errosShow: false,
    };
  },
  computed: {
    isFormValid() {
      return (
        this.formData.username !== "" &&
        this.formData.email !== "" &&
        this.formData.role !== 0 &&
        this.formData.password !== "" &&
        this.formData.password_repeat !== "" &&
        this.formData.password === this.formData.password_repeat &&
        this.formData.public &&
        this.formData.agree === true
      );
    },
  },
  methods: {
    validEmail(email) {
      var re =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    closeMessage() {
      this.registrationSuccess = false;
    },
    validationAttributes() {
      if (this.formData.username === "") {
        this.formErrors.errorUser = "Вы не ввели имя";
        this.errorList.push(this.formErrors.errorUser);
      }
      if (this.validEmail(this.formData.email) === false) {
        this.formErrors.errorEmail = "Некорректный Email";
        this.errorList.push(this.formErrors.errorEmail);
      }
      if (this.formData.role === 0) {
        this.formErrors.errorRole = "Выберите должность";
        this.errorList.push(this.formErrors.errorRole);
      }
      if (this.formData.password === "") {
        this.formErrors.errorPass = "Введите пароль";
        this.errorList.push(this.formErrors.errorPass);
      }
      if (this.formData.password !== this.formData.password_repeat) {
        this.formErrors.errorPassConf = "Пароли не совпадают";
        this.errorList.push(this.formErrors.errorPassConf);
      }
      if (this.formData.agree !== true) {
        this.formErrors.errorAgree = "Обязательное поле";
        this.errorList.push(this.formErrors.errorAgree);
      }
    },
    resetErrors() {
      this.formErrors.errorUser = "";
      this.formErrors.errorEmail = "";
      this.formErrors.errorRole = "";
      this.formErrors.errorPass = "";
      this.formErrors.errorPassConf = "";
      this.formErrors.errorAgree = "";
    },
    submitForm() {
      console.log("Отправка данных:", this.formData);
      console.log(this.isFormValid);
      console.log(this.validEmail(this.formData.email));
      console.log(this.formErrors);
      this.resetErrors();
      this.errorList = [];
      if (this.isFormValid && this.validEmail(this.formData.email)) {
        axios
          .post("https://jsonplaceholder.typicode.com/posts", this.formData)
          .then((response) => {
            console.log(response.data);
            this.errosShow = false;
            this.registrationSuccess = true;
          })
          .catch((error) => {
            console.error("Ошибка при регистрации:", error);
          });
      } else {
        this.registrationSuccess = false;
        this.validationAttributes;
        console.log(this.validationAttributes());
      }
    },
  },
});
</script>
<style>
.container {
  position: relative;
  margin: 0 auto;
  max-width: 960px;
  background-color: #fff;
  border-radius: 15px;
  overflow: hidden;
}
.form {
  width: 100%;
}
.form__title {
  font-size: 19px;
  font-style: normal;
  font-weight: 700;
  line-height: 27px;
  letter-spacing: -0.066px;
  padding: 17px 30px;
}
.form__block {
  padding: 17px 31px 31px;
  border-top: 1px solid #d9d9d9;
}
.form__subtitle {
  font-size: 16px;
  font-style: normal;
  font-weight: 500;
  line-height: 19px;
  margin-bottom: 34px;
  grid-column: 1 / span 2;
}
.form__block .form__label:nth-child(5n),
.form__block .form__label:nth-child(6n) {
  grid-row: 4 / span 1;
}
.form__block-agree {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}
.form__btn {
  min-width: 300px;
  padding: 10px 20px;
  border: 1px solid rgba(73, 122, 218, 0.2);
  border-radius: 8px;
  background-color: rgba(73, 122, 218, 0.2);
  color: #497ada;
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 19px;
  cursor: pointer;
  transition: 0.2s background-color ease-in, 0.2s color ease-in;
}
.form__btn:hover,
.form__btn:focus-visible {
  background-color: #497ada;
  color: #fff;
}
.form__success {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 100%;
  font-size: 36px;
  color: #497ada;
  padding: 100px;
  text-align: center;
  background-color: #fff;
  top: 0;
  left: 0;
  border-radius: 15px;
}
.form__message {
  margin-top: 60px;
  margin-bottom: 60px;
}
.list {
  list-style: none;
  display: flex;
  margin: 0 auto;
  padding: 60px;
  flex-direction: column;
  align-items: flex-start;
}
.item {
  font-size: 10px;
  color: #f6383e;
}
@media (max-width: 768px) {
  .block__descr {
    padding-left: 10px;
  }
  .form__block-agree {
    flex-direction: column;
    align-items: flex-start;
  }
  .label-check {
    margin-bottom: 40px;
  }
  .descr-agree {
    font-size: 12px;
    line-height: 14px;
  }
  .descr {
    font-size: 14px;
    line-height: 16px;
  }
  .des {
    font-size: 12px;
    line-height: 14px;
  }
  .form__btn {
    min-width: 100%;
  }
  .grid {
    display: flex;
    flex-direction: column;
  }
  #app {
    padding: 40px 20px;
  }
}
</style>
