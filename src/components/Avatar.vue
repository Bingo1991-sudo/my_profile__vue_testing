<template>
  <div class="user-avatar">
    <div class="user-avatar__box" :class="sizeClass">
      <div v-if="avatar" class="user-avatar__image">
        <img :src="imgSrc" :alt="'Аватар пользователя ' + username"/>
      </div>

      <div v-else class="user-avatar__image user-avatar__image--empty">
        <span>{{ username.charAt(0) }}</span>
      </div>

      <div class="user-avatar__upload">
        <div class="user-avatar__upload-btn">
          <button @click=toggleList() :data-title="'Обновить аватар'">
            <svg width="15" height="15" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                  d="M9.91914 7.19558C9.91914 8.54392 8.83397 9.64078 7.5 9.64078C6.16603 9.64078 5.08127 8.54392 5.08127 7.19558C5.08127 5.84725 6.16603 4.75039 7.5 4.75039C8.83397 4.75039 9.91914 5.84767 9.91914 7.19558ZM15 3.72353V10.6685C15 11.5943 14.2573 12.345 13.3414 12.345H1.65865C0.74266 12.345 0 11.5943 0 10.6685V3.72353C0 2.79768 0.74266 2.04702 1.65865 2.04702H3.69879V1.46695C3.69879 0.656773 4.34815 0 5.15011 0H9.84989C10.6518 0 11.3012 0.656773 11.3012 1.46695V2.0466H13.3414C14.2573 2.04702 15 2.79768 15 3.72353ZM11.1631 7.19558C11.1631 5.15401 9.51982 3.49301 7.5 3.49301C5.48059 3.49301 3.83729 5.15401 3.83729 7.19558C3.83729 9.23716 5.48059 10.8982 7.5 10.8982C9.51982 10.8982 11.1631 9.23716 11.1631 7.19558Z"
                  fill="currentColor"
              />
            </svg>
          </button>
        </div>
        <transition name="fade">
          <div class="user-avatar__upload-list" v-if="isListOpen">
            <p class="user-avatar__dialog-btn">Загрузить</p>
            <p class="user-avatar__dialog-btn">Удалить</p>
          </div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "user-avatar",
  components: {},

  data() {
    return {
      isListOpen: false,
      query: false,
    };
  },

  props: {
    username: {
      type: String,
      default: "User",
      required: true,
    },

    avatar: {
      type: String,
      default: () => "",
    },

    upload: {
      type: Boolean,
      default: false,
    },

    size: {
      type: String,
      default: "big",
    },
  },

  computed: {
    sizeClass() {
      return `user-avatar__box--${this.size}`;
    },

    imgSrc() {
      return `/img/avatar.png`;
    },
  },

  mounted() {
    this.popupItem = this.$el;
  },

  methods: {
    toggleList() {
      if (!this.isListOpen) {
        this.isListOpen = true
      } else this.isListOpen = false;
    },
  },
};
</script>

<style lang="scss">
.user-avatar {
  &__box {
    position: relative;
    width: 102px;
    height: 102px;
  }

  &__image {
    display: flex;

    width: 100%;
    height: 100%;
    border-radius: 50%;
    overflow: hidden;

    &--empty {
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #4e75fa;

      span {
        color: #fff;
        text-transform: uppercase;
        font-size: 30px;
      }
    }
  }

  &__dialog-btn {
    text-align: left;
    font-size: 16px;
    color: #007bff;
    font-weight: 500;
    padding: 6px 12px;
    margin: 0;

    &:hover {
      cursor: pointer;
      text-decoration: underline;
    }
  }

  &__upload {
    position: absolute;
    bottom: 3px;
    right: 1px;

    &-btn {
      button {
        display: inline-flex;
        align-items: center;
        justify-content: center;

        padding: 0;
        margin: 0;

        width: 35px;
        height: 35px;

        transition: 0.3s ease;

        background-color: #ebebeb;
        border: 0;
        border-radius: 50%;

        outline: none;

        cursor: pointer;

        &:hover {
          background-color: #d9d9d9;
        }

        svg {
          margin-top: 3px;
          flex-shrink: 0;
        }
      }
    }

    &-list {
      position: absolute;
      left: 0;
      top: 100%;

      padding: 5px;

      border-radius: 6px;
      background-color: #fff;
      box-shadow: 0 5px 17px #d6d6d6;

      .input-wr {
        width: 0;
        height: 0;
        visibility: hidden;
      }
    }
  }
}

@media(max-width: 630px) {
  .user-avatar {
    &__box {
      width: 90px;
      height: 90px;
    }
  }
}
</style>
