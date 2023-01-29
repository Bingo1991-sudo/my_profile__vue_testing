<template>
  <div class="pass-reset">
    <h1 class="h1">Изменение пароля
    </h1>
    <Form class="recovery-password" @submit="onSubmit" v-slot="{ errors }">
      <div class="row form-group">
        <div class="label">
          <label>Текущий пароль</label><sup>*</sup>
        </div>
        <div class="">
          <Field name="pass"
                 v-model="password"
                 type="password"
                 class="form-control login-input"
                 :rules="isRequired"
          />
          <div class="error-message">{{ errors.pass }}</div>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Новый пароль</label><sup>*</sup>
        </div>
        <div class="">
          <Field name="newPas"
                 v-model="newPassword"
                 type="password"
                 class="form-control login-input"
                 :rules="isRequired"
          />
          <div class="error-message">{{ errors.newPas }}</div>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Повторите пароль</label><sup>*</sup>
        </div>
        <div class="">
          <Field name="repeatPass"
                 v-model="repeatPassword"
                 type="password"
                 class="form-control login-input"
                 :rules="isConfirm"
          />
          <div name="repeatPass" class="error-message">{{ errors.repeatPass }}</div>
        </div>
      </div>
    </Form>
  </div>
</template>
<script>

import {Form, Field} from 'vee-validate';

export default {
  components: {
    Form,
    Field
  },
  data: function () {
    return {
      password: "12345678",
      newPassword: "",
      repeatPassword: ""
    };
  },
  methods: {
    getResetPasswordToken: function () {
    },
    resetPassword: function () {
    },

    isRequired(value) {
      if (!value) {
        return 'Пожалуйста, заполните поле';
      }

      return true;
    },
    isConfirm() {
      if (this.newPassword != this.repeatPassword) {
        return 'Пароли не совпадают';
      }

      return true;
    },

    onSubmit(values) {
      alert(JSON.stringify(values, null, 3));
    }
  },
};
</script>
<style lang="scss">

</style>
