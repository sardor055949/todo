<template>
  <button class="modal__open-btn" @click="$emit('openModal')">
    <img src="@/assets/img/edit.svg" alt="">
  </button>
</template>

<script>
export default {

}
</script>

<style>
.modal__open-btn{
    position: fixed;
    right: 30px;
    bottom: 30px;
    width: 56px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #6750a41c;
    box-shadow: 0px 4px 8px 3px #00000026;
    border-radius: 16px;
}
</style>