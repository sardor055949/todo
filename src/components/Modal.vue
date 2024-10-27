<template>
  <Transition name="modal">
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h2 class="modal__title">
          {{ edit ? words.changeNote[lang] : words.addNote[lang] }}
        </h2>
        <div class="modal__inputs">
          <label>
            <span>Title</span>
            <input type="text" placeholder="Title" v-model="title" />
          </label>
          <label>
            <span>Content</span>
            <textarea placeholder="Content" v-model="text"></textarea>
          </label>
        </div>
        <div class="modal__btns">
          <button class="modal__btn cancel" @click="closeModal">{{ words.cancel[lang]}}</button>
          <button v-if="edit" class="modal__btn add" @click="editedNote">{{ words.change[lang] }}</button>
          <button v-else class="modal__btn add" @click="addNote">{{ words.add[lang] }}</button>
        </div>
      </div>
    </div>
  </Transition>
</template>
    
    <script>
export default {
  data() {
    return {
      title: "",
      text: "",
      id: this.currentId,
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
      this.title = "";
      this.text = "";
    },
    addNote() {
      if(this.title != "" && this.text != "") {
        let item = {
          id: this.id++,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", item);
        this.title = "";
        this.text = "";
      }
    },
    editedNote() {
      if(this.title != "" && this.text != "") {
        let editedNote = {
          id: this.editNote.id,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString()
        }
        this.$emit('editedNote', editedNote)
      }
    }
  },
  props: {
    currentId: Number,
    edit: Boolean,
    editNote: Object,
    lang: String
  },
  inject: ["words"]
};
</script>
    
    <style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.35);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.modal__block {
  background: linear-gradient(0deg, #fffbfe, #fffbfe),
    linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11));
  padding: 24px;
  border-radius: 28px;
  max-width: 312px;
  width: 100%;
}

.modal__title {
  line-height: 32px;
  font-size: 24px;
  color: #1c1b1f;
  font-weight: 400;
  margin-bottom: 30px;
}

.modal__inputs {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.modal__inputs label {
  position: relative;
}

.modal__inputs span {
  position: absolute;
  left: 16px;
  top: 8px;
  color: #6750a4;
  line-height: 16px;
  font-size: 12px;
}

.modal__inputs input,
.modal__inputs textarea {
  border-radius: 4px 4px 0px 0px;
  background: #e7e0ec;
  width: 100%;
  border: none;
  outline: none;
  resize: none;
  padding: 23px 0 9px 16px;
  font-size: 16px;
  color: #49454f;
  border-bottom: 1px solid #1c1b1f;
}

.modal__btns {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  margin-top: 24px;
}

.modal__btn {
  font-size: 14px;
  font-weight: 500;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
  font-family: "RM";
  padding: 10px 12px;
  cursor: pointer;
  background: transparent;
  border-radius: 5px;
  transition: 300ms;
}

.cancel {
  color: #cf1b1b;
}

.add {
  color: #6750a4;
}

.cancel:hover {
  background: #ffe1e1;
}

.add:hover {
  background: #e6ddff;
}

.modal-enter-active,
.modal-leave-active {
  transition: 0.2s linear;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.5);
}
</style>