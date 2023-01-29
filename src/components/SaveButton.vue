<template>
  <div class="row">
    <span class="profile-btn" @click="save">
    Сохранить
    <span class="spinner-border" role="status" aria-hidden="true" v-if="saveInProgress"></span>
  </span>
  </div>
</template>

<script>

export default {
  name: "save-btn",
  data: function () {
    return {
      saveInProgress: false,
    };
  },
  methods: {
    save: function () {
    }
  }
};
</script>
<style lang="scss" scoped>

.spinner-border {
  display: block;
  width: 2.5rem;
  height: 2.5rem;
}

.profile-btn {
  display: block;
  border-radius: 15px;
  color: #fff;
  width: 130px;
  padding: 8px 23px;
  font-size: 16px;
  background-color: #6c757d;
  border-color: #6c757d;
  position: relative;
  margin-top: 15px;

  &:hover {
    cursor: pointer;
  }
}
@media(max-width: 630px) {
 .profile-btn {
   position: fixed;
   bottom: 0;
   left: 0;
   rihgt: 0;
   width: 100%;
   border-radius: 0;
   padding: 14px;
 }
}

</style>
