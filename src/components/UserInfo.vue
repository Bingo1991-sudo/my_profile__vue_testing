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
        <select name="multiSelect" id="multiSelect" multiple multiselect-search="true" multiselect-select-all="true"
                multiselect-max-items="3"
                onchange="multiSelect.innerHTML='<option value='+languages[0].code+'>'+languages[0].name+'</option><option selected value='+languages[1].code+'>'+languages[1].name+'</option><option value='+languages[2]+'>'+languages[2].name+'</option>';"
                onblur="multiSelect.loadOptions()">
          <option value={{languageSelected.code}}>{{ languageSelected.name }}</option>
          <option v-for="option in languagesOptions" v-bind:key="option.code">{{ option.name }}</option>
        </select>
      </div>
      <mySelect></mySelect>
    </Form>
  </div>
</template>
<script>

import {Form, Field} from 'vee-validate';
import mySelect from '../js/Select'

export default {
  name: "user-info",
  components: {
    Form,
    Field,
    mySelect
  },
  data() {
    return {
      displayName: "",
      mail: "",
      date: "",
      phone: '',
      city: '',
      phones: [],
      languageSelected: {name: 'Русский', code: 'ru'},
      languagesOptions: [
        {name: 'Английский', code: 'en'},
        {name: 'Корейский', code: 'ko'}
      ],
      mySelect
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
<style lang="scss">

.info {
  max-width: 720px;
  margin-right: 20px;
}

.multiselect-dropdown {
  width: 139px !important;
  display: inline-block;
  padding: 4px 30px 0px 5px;
  border-radius: 4px;
  border: solid 1px #ced4da;
  background-color: white;
  position: relative;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill='none' stroke='%23343a40' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M2 5l6 6 6-6'/%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right .75rem center;
  background-size: 16px 12px;
  text-align: left;
  height: auto !important;
}

.multiselect-dropdown span.optext {
  padding: 3px 12px;
  background: #d2d7ff;
  display: inline-block;
  max-width: 130px;
  overflow: hidden;
  color: #35495e;
  font-size: 14px;
  border-radius: 20px;
}

.multiselect-dropdown span.optext:hover{
  background: #eaeaea;
  cursor: pointer;
}

.multiselect-dropdown span.placeholder {
  color: #ced4da;
}

.multiselect-dropdown-list-wrapper {
  box-shadow: gray 0 0 1px;
  z-index: 100;
  padding: 0;
  border-radius: 4px;
  border: solid 1px #ced4da;
  display: none;
  margin: -1px;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  background: white;
  width: 176px;
}

.multiselect-dropdown-list-wrapper .multiselect-dropdown-search {
  margin-bottom: 5px;
}

.multiselect-dropdown-list {
  width: 176px;
  padding: 2px;
  height: auto !important;
  overflow-y: auto;
  overflow-x: hidden;
}

.multiselect-dropdown-list::-webkit-scrollbar {
  width: 6px;
}

.multiselect-dropdown-list::-webkit-scrollbar-thumb {
  background-color: #bec4ca;
  border-radius: 3px;
}

.multiselect-dropdown-list div {
  padding: 5px;
  text-align: left;
}

.multiselect-dropdown-list input {
  height: 1.15em;
  width: 1.15em;
  margin-right: 0.35em;
}

.multiselect-dropdown-list div.checked {
}

.multiselect-dropdown-list div:hover {
  background-color: #ced4da;
}

.multiselect-dropdown span.maxselected {
  width: 100%;
}

.multiselect-dropdown-all-selector {
  border-bottom: solid 1px #ced4da;
  text-align: left;
}

@media(max-width: 630px) {
  .multiselect-dropdown-list, .multiselect-dropdown-list-wrapper {
    width: 175px;
  }
}
</style>
