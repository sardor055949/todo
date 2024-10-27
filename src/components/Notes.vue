<template>
  <main class="main">
    <div class="notes">
        <div class="container">
            <div class="notes__top">
                <h2 v-if="searchOn" class="notes__top-title">Поиск</h2>
                <h2 v-else class="notes__top-title">{{ notesLength > 0 ? words.allNotes[lang] : words.noNotes[lang] }}</h2>
                <button class="notes__top-btn" @click="grid = !grid">
                    <img v-if="grid" src="@/assets/img/list.svg" alt="">
                    <img v-else src="@/assets/img/grid.svg" alt="">
                    <span>{{ grid ? words.list[lang] : words.grid[lang] }}</span>
                </button>
            </div>
            <div class="notes__list">
                <NotesItem 
                    v-for="note in notes" :key="note.id"
                    :note="note"
                    @delNote="$emit('delNote', note.id)"
                    @changeNote="$emit('changeNote', note.id)"
                    :searchOn="searchOn"
                    :lang="lang"
                />
            </div>
        </div>
    </div>
  </main>
</template>

<script>
import NotesItem from '@/components/NotesItem.vue'
export default {
    data() {
        return {
            grid: true
        }
    },
    components: {
        NotesItem
    },
    computed: {
        notesLength() {
            return this.notes.length
        }
    },
    props: {
        notes: Array,
        searchOn: Boolean,
        lang: String
    },
    inject: ["words"]
}
</script>

<style>
.notes__top {
    margin: 30px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.notes__top-title {
    color: #323232;
    font-size: 22px;
    line-height: 26px;
    font-weight: 400;
}

.notes__top-btn {
    width: 121px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    border-radius: 16px;
    background: linear-gradient(0deg, #FFFBFE, #FFFBFE),
    linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11));
    box-shadow: 0px 4px 8px 3px #00000026;
    font-size: 14px;
    color: #6750A4;
    letter-spacing: 0.1px;
}
.notes__list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
}
</style>