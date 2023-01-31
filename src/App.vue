<template>
  <div class="container">
    <Avatar></Avatar>
    <div class="form-wr">
      <UserInfo></UserInfo>
      <ResetPassword></ResetPassword>
    </div>
    <SaveBtn></SaveBtn>
  </div>
</template>

<script>
import Avatar from './components/Avatar.vue'
import UserInfo from './components/UserInfo.vue'
import ResetPassword from './components/ResetPassword.vue'
import SaveBtn from './components/SaveButton.vue'

export default {
  name: 'App',
  components: {
    Avatar,
    UserInfo,
    ResetPassword,
    SaveBtn
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.h1 {
  color: #000;
  font-size: 20px;
  font-weight: normal;
  text-align: left;
  margin-bottom: 30px;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex-wrap: wrap;
}

.row, .form-wr {
  display: flex;
  justify-content: space-between;
}

.form-group {
  margin-bottom: 8px;

  & .form-control, & input.form-control {
    display: block;
    width: 150px !important;
    height: 35px;
    padding: 0 12px;
    font-size: 16px;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
  }
}

.label {
  font-size: 14px;
  color: #000;
  margin-right: 10px;
  line-height: 35px;
}

input[type="date"] {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

input:focus-visible {
  outline-color: #6c757d;
}

.error-message {
  font-size: 12px;
  color: #cc0000;
  text-align: left;
}

@media(max-width: 630px) {
  .form-wr {
    flex-wrap: wrap;
    justify-content: center;

    & .form-control, & input.form-control {
      width: 149px !important;
    }
  }

  .container {
    margin-bottom: 50px;
  }
}

</style>
