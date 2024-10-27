<template>
  <div class="notes__item">
    <div class="notes__item-top">
        <h2 class="notes__item-title">{{note.title}}</h2>
        <p class="notes__item-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-text">{{note.text}}</p>
    <div class="notes__item-btns" v-show="searchOn = !searchOn">
        <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
            <img src="@/assets/img/edit.svg" alt="">
            <span>{{ words.edit[lang] }}</span>
        </button>
        <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
            <img src="@/assets/img/del.svg" alt="">
            <span>{{ words.del[lang] }}</span>
        </button>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        note: Object,
        searchOn: Boolean,
        lang: String
    },
    inject: ["words"]
}
</script>

<style>
.notes__item {
  background: linear-gradient(0deg, #fffbfe, #fffbfe),
    linear-gradient(0deg, rgba(103, 80, 164, 0.05), rgba(103, 80, 164, 0.05));
  box-shadow: 0px 1px 3px 1px #00000026;
  border-radius: 16px;
  padding: 16px;
}

.notes__item-title {
    color: #1C1B1F;
    font-size: 16px;
    font-family: "RM";
    font-weight: 500;
    line-height: 24px;
}
.notes__item-date {
    color: #CAC4D0;
    font-size: 14px;
    letter-spacing: 0.25px;
    line-height: 20px;
}
.notes__item-text {
    font-size: 14px;
    letter-spacing: 0.25px;
    color: #49454F;
    margin: 16px 0;
}
.notes__item-btns {
    display: flex;
    justify-content: flex-end;
    align-items: center;
}
.notes__item-btn {
    font-size: 14px;
    padding: 12px;
    letter-spacing: 0.1px;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: 300ms;
}

.edit {
    color: #6750A4;
}

.del {
    color: #CF1B1B; 
}

.edit:hover {
    background: #E6DDFF;
}

.del:hover {
    background: #FFE1E1;
}
</style>