<template>
  <div class="info">
    <h1 class="h1">Hастройки</h1>
    <Form @submit="onSubmit" v-slot="{ errors }">
      <div class="row form-group">
        <div class="label">
          <label>ФИО</label><sup>*</sup>
        </div>
        <div class="">
          <Field name="displayName" type="text" v-model="displayName" class="form-control" :rules="isRequired"/>
          <div class="error-message">{{ errors.displayName }}</div>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Дата рождения</label>
        </div>
        <div class="">
          <input type="date" v-model="date" class="form-control"/>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>E-mail</label><sup>*</sup>
        </div>
        <div class="">
          <Field name="mail" type="text" v-model="mail" class="form-control" :rules="isMailValidate"/>
          <div class="error-message">{{ errors.mail }}</div>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Город</label>
        </div>
        <div class="">
          <input v-model="city" class="form-control"/>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Телефон</label>
        </div>
        <div class="">
          <input v-model="phone" class="form-control"/>
        </div>
      </div>
      <div class="row form-group">
        <div class="label">
          <label>Языки</label>
        </div>
        <div class="">
          <Multiselect v-model="languages" tag-placeholder="Добавьте языки" placeholder="Языки"
                       label="name" track-by="code" :options="languagesOptions" :multiple="true" :taggable="true"
                       @tag="addTag"></Multiselect>
        </div>
      </div>
    </Form>
  </div>
</template>
<script>

import {Form, Field} from 'vee-validate';
import Multiselect from '@vueform/multiselect'

export default {
  name: "user-info",
  components: {
    Form,
    Field,
    Multiselect
  },
  data() {
    return {
      displayName: "",
      mail: "",
      date: "",
      phone: '',
      city: '',
      phones: [],
      languages: [
        {name: 'Русский', code: 'ru'}
      ],
      languagesOptions: [
        {name: 'Английский', code: 'en'},
        {name: 'Корейский', code: 'ko'}
      ]
    };
  },

  methods: {
    isRequired(value) {
      if (!value) {
        return 'Пожалуйста, заполните поле';
      }

      return true;
    },

    isMailValidate(value) {

      const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
      if (!regex.test(value)) {
        return 'Укажите корректный e-mail';
      }

      return true;
    },
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },

    addTag(newTag) {
      const tag = {
        name: newTag,
        code: newTag.substring(0, 2) + Math.floor((Math.random() * 10000000))
      }
      this.options.push(tag)
      this.value.push(tag)
    }
  }
};
</script>
<style lang="scss" scoped>

.info {
  max-width: 720px;
  margin-right: 20px;
}

</style>
