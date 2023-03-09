<template>
  <transition name="fade" mode="out-in">
    <nav class="nav" v-if="!search">
      <transition name="slide-up">
        <button class="nav__lang" @click="changeLang">
          <span v-if="lang == 'ru'">Uz</span>
          <img
            v-if="lang == 'ru'"
            class="nav__lang-flag"
            src="@/assets/img/Uzbekistan-flag.webp"
            alt=""
          />
          <span v-if="lang == 'uz'">Ru</span>
          <img
            v-if="lang == 'uz'"
            class="nav__lang-flag"
            src="@/assets/img/russia.png"
            alt=""
          />
        </button>
      </transition>
      <h1 class="nav__title">{{ langWord.appbartitle[lang] }}</h1>
      <button class="nav__search" @click="searching">
        <img src="@/assets/img/search.svg" alt="" />
      </button>
    </nav>

    <nav class="nav" v-else>
      <button class="nav__close" @click="back">
        <img src="@/assets/img/back.svg" alt="" />
      </button>
      <div class="container">
        <input
          class="search"
          type="text"
          :placeholder="langWord.infobarsearch[lang]"
          v-model="searchValue"
        />
      </div>
      <button class="nav__reset" @click="reset">
        <img src="@/assets/img/clear.svg" alt="" />
      </button>
    </nav>
  </transition>
</template>
<script>
export default {
  data() {
    return {
      searchValue: this.searchValue,
    };
  },
  props: {
    lang: String,
    langWord: Object,
    search: Boolean,
  },
  methods: {
    changeLang() {
      this.$emit("changeLang", this.lang == "uz" ? "ru" : "uz");
    },
    searching() {
      this.$emit("searching", !this.search);
    },
    back() {
      this.searchValue = "";
      this.$emit("back", false);
    },
    reset() {
      this.searchValue = "";
    },
  },
  watch: {
    searchValue(value) {
      // watch value har bir harakatini kuzatadi
      this.$emit("searchValue", value);
    },
  },
};
</script>

<style lang="scss">
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.5s ease-out;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.slide-up-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
/* we will explain what these classes do next! */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
