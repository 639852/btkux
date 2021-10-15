<template>
  <section class="container mb-5">
    <h2>Первое задание</h2>

    <form ref="form" @submit.prevent="placeAnOrder">
      <FormInput
        v-for="(param, index) of params"
        :key="index"
        :param="param"
        :errors="errors"
        @bindValue="bindValue"
      />
      <FormButton text="Отправить" />
    </form>
  </section>
</template>

<script>
import FormInput from "./FormInput.vue";
import FormButton from "./FormButton.vue";
import axios from "axios";

export default {
  data() {
    return {
      params: [
        {
          header: "Представьтесь",
          inputType: "text",
          typeValue: "name",
          isInvalid: false
        },
        {
          header: "Адрес доставки",
          inputType: "text",
          typeValue: "address",
          isInvalid: false
        },
        {
          header: "Телефон",
          inputType: "tel",
          typeValue: "phone",
          isInvalid: false
        },
        {
          header: "Эл. почта",
          inputType: "email",
          typeValue: "email",
          isInvalid: false
        },
        {
          header: "Комментарий",
          inputType: "textarea",
          typeValue: "comment",
          isInvalid: false
        }
      ],
      errors: {},
      user: {
        name: "",
        address: "",
        phone: "",
        email: "",
        comment: ""
      }
    };
  },
  components: { FormInput, FormButton },
  methods: {
    placeAnOrder() {
      axios
        .get("https://vue-study.skillbox.cc/api/users/accessKey")
        .then(response => {
          return axios.post(
            "https://vue-study.skillbox.cc/api/orders",
            this.user,
            {
              params: {
                userAccessKey: response.data.accessKey
              }
            }
          );
        })
        .then(() => {
          alert("Ваш заказ успешно оформлен!");
          this.$refs.form.reset();
        })
        .catch(err => {
          const errorMessage = err.response.data.error.message;
          if (errorMessage) alert("Возникла ошибка: " + errorMessage + "!");

          this.errors = err.response.data.error.request;
          for (let i = 0; i < this.params.length; i++) {
            const type = this.params[i].typeValue;

            for (let key in this.errors) {
              if (key === type) this.params[i].isInvalid = true;
            }
          }
        });
    },
    bindValue(typeValue, value) {
      this.user[typeValue] = value;
      delete this.errors[typeValue];
    }
  }
};
</script>