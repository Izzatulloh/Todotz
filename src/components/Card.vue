<template>
  <div class="notes" :class="{ grid: grid, list: !grid }" v-if="notes.length > 0">
    <div class="card " :class="item.done==true? 'done' : ''" v-for="(item, index) in notes" :key="index">
      <h2 class="card__title">{{ item.title }}</h2>
      <p class="card__time">{{ item.time }}</p>
      <p class="card__text">{{ item.content }}</p>

      <div class="card__btns" v-if="!search">
        <button class="btn edit" @click="changeNote(item.id)">
          <img src="@/assets/img/change.svg" alt="" />
          <span>{{ langWord.editbtn[lang] }}</span>
        </button>
        <button class="btn delete" @click="removeNote(item.id)">
          <img src="@/assets/img/delete.svg" alt="" />
          <span>{{ langWord.deledit[lang] }}</span>
        </button>
      </div>
      <button class="card__done" @click="$emit('doneNote',item.id)" v-if="!item.done">
        <img src="../assets/img/done.png" alt="" />
      </button>
    </div>
  </div>
  <p class="note__off" v-else>{{ langWord.nonote[lang] }}</p>
</template>
<script>
export default {
  props: {
    langWord: Object,
    lang: String,
    search: Boolean,
    notes: Array,
    grid: Boolean,
    openModal: Boolean,
    done:Boolean
  },
  methods: {
    removeNote(cardId) {
      for (let i = 0; i < this.notes.length; i++) {
        if (this.notes[i].id == cardId) {
          this.notes.splice(i, 1);
          break;
        }
      }
    },
    changeNote(cardId) {
      this.$emit("changeNote", cardId);
    },
    
  },
};
</script>
<style lang="scss">

</style>
