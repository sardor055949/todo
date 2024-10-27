<template>
  <header class="header">
    <Transition name="header__notes">
      <div class="header__notes" v-show="header === true">
        <button class="header__lang" @click="changeLang">
          {{ lang == "ru" ? "RU" : "UZ" }}
        </button>
        <h1 class="header__title">{{ words.notes[lang] }}</h1>
        <button
          class="header__search"
          @click="(header = false), $emit('searchOpen')"
        >
          <img src="@/assets/img/search.svg" alt="" />
        </button>
      </div>
    </Transition>
    <Transition name="header__form">
      <div class="header__form" v-show="header === false">
        <button
          class="header__back"
          @click="(header = true), (search = ''), $emit('searchClose')"
        >
          <img src="@/assets/img/back.svg" alt="" />
        </button>
        <input
          type="text"
          class="header__input"
          :placeholder="words.search[lang]"
          v-model="search"
        />
        <button class="header__close" @click="search = ''">
          <img src="@/assets/img/close.svg" alt="" />
        </button>
      </div>
    </Transition>
  </header>
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: "",
    };
  },
  watch: {
    search(val) {
      this.$emit("searchValue", val);
    },
  },
  props: {
    lang: String,
  },
  methods: {
    changeLang() {
      this.$emit('changeLang', this.lang == "ru" ? "uz" : "ru")
    }
  },
  inject: ["words"]
};
</script>

<style>
.header {
  height: 64px;
  overflow: hidden;
  background: #f3edf7;
  box-shadow: 0px 4px 4px 0px #00000040;
}
.header__notes,
.header__form {
  padding: 0 25px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
.header__title {
  font-size: 22px;
  font-weight: 400;
  color: #1c1b1f;
}
.header__lang {
  font-size: 25px;
  font-weight: 700;
  color: #1c1b1f;
}
.header__input {
  width: 80%;
  border: none;
  outline: none;
  background: none;
  font-size: 16px;
}

.header__input::placeholder {
  color: #9d9d9d;
}

/* Transition start */

.header__notes-enter-active,
.header__notes-leave-active {
  transition: 0.5s linear;
}

.header__notes-enter-from,
.header__notes-leave-to {
  opacity: 0;
  transform: translateY(-200px);
}
.header__notes-enter-to,
.header__notes-leave-from {
  opacity: 1;
  transform: translateY(0);
}
/* ################################################# */
.header__form-enter-active,
.header__form-leave-active {
  transition: 1s linear;
}
.header__form-enter-from,
.header__form-leave-to {
  opacity: 1;
  /* transform: translateY(0); */
}
.header__form-enter-to,
.header__form-leave-from {
  opacity: 0;
  /* transform: translateY(200px); */
}
</style>