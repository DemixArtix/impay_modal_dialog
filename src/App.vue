<template lang="pug">
button.btn.primary(@click="modal = true") show modal
Teleport(to="#app")
  transition(name="fade")
    modalDialog(v-if="modal" @hideModal="modal = false" v-slot="{ resolve }")
      .modal__custom_text Сhoose an answer
      button.modal__custom_btn.btn(v-for="{ value, classBtn} in items" :class="classBtn" :key="value" @click="resolve(value)") {{value}}
</template>

<script lang="ts">
import { defineComponent } from 'vue';
//@ts-ignore
import modalDialog from 'components/modal-dialog';

export default defineComponent({
  name: 'App',
  components: {
    modalDialog
  },
  data: function () {
    return {
      modal: false,
      items: [
        {
          value: 'Ok',
          classBtn: ['success']
        },
        {
          value: 'Warning',
          classBtn: ['danger']
        },
        {
          value: 'Some',
          classBtn: ['warning', 'small']
        },
        {
          value: '1',
          classBtn: ['info']
        },
        {
          value: 'Cancel',
          classBtn: ['dark', 'big']
        },
      ]
    }
  }
});
</script>

<style lang="sass">


$danger: rgb(255,186,0)
$success: rgb(70,201,58)
$warning: rgb(255,71,87)
$info: darkgrey
$primary: rgb(59,89,153)
$dark:  rgb(30,30,30)

*
  box-sizing: border-box
html
  font-size: 15px
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px


.modal__custom_text
  padding: 1rem

.btn
  padding: 0.5rem
  cursor: pointer
  margin: 0.1em
  background-color: #000
  color: #fff
  border-radius: 0.2rem
  border: none
  position: relative
  transition: background-color .2s
  &.danger
    background-color: $danger
    &:hover
      background-color: lighten($danger, 10)
  &.success
    background-color: $success
    &:hover
      background-color: lighten($success, 10)
  &.warning
    background-color: $warning
    &:hover
      background-color: lighten($warning, 10)
  &.info
    background-color: $info
    &:hover
      background-color: lighten($info, 10)
  &.primary
    background-color: $primary
    &:hover
      background-color: lighten($primary, 10)
  &.dark
    background-color: $dark
    &:hover
      background-color: lighten($dark, 10)
  &.big
    font-size: 1.2rem
    padding: 0.5rem 1rem
  &.small
    font-size: 0.6rem
    padding: 0.45rem

.fade-enter-active,
.fade-leave-active
  transition: opacity 0.5s ease

.fade-enter-active
  animation: bounce-in 0.5s
.fade-leave-active
  animation: bounce-in 0.5s reverse

.fade-enter-from,
.fade-leave-to
  opacity: 0

@keyframes bounce-in
  0%
    transform: scale(0)
  50%
    transform: scale(1.25)
  100%
    transform: scale(1)




</style>
