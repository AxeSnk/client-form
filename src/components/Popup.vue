<template>
  <div class="popup">
    <div class="popup__overlay">
      <div class="popup__window">
        <span class="popup__title">Новый клиент успешно создан!</span>
        <button class="btn-close" @click="closePopup">&times;</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'popup',
    methods: {
      closePopup() {
        this.$emit('closePopup')
      }
    }
  }
</script>

<style lang="scss" scoped>
.popup {
  &__overlay {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, .5);
    z-index: 99;
  }
  &__window {
    position: relative;
    width: 600px;
    border-radius: 5px;
    background: #fff;
    margin: 100px auto;
    padding: 20px;
  }
  &__title {
    font-size: 1.5rem;
    font-weight: bold;
  }
}
.btn-close {
  position: absolute;
  right: 5px;
  top: 5px;
  width: fit-content;
  padding: 4px 8px;
  cursor: pointer;
  background: #fff;
  border-style: none;
  font-size: 1.5rem;;
  outline: none;
}
.btn-close:active,
.btn-close:hover {
  outline: none;
}
.btn-close:hover {
  font-weight: bold;
}
</style>