<template lang="pug">
.modal
  transition(name="block")
    .modal__block(v-if="result" key="result")
      .modal__result You have chosen: {{result}}
  transition(name="block")
    .modal__block(v-if="!result" key="content")
      .modal__content
        slot(ref="slotBlock" :resolve="resolve" )
          .modal__default
            .modal__default_text default modal

</template>

<script lang="ts">
  import { defineComponent, ref, onMounted, onUnmounted } from 'vue'
  import { Ref } from 'vue'

  export default defineComponent({
    name: "index",
    props: {

    },
    setup(props, {emit}) {
      let result: Ref<any> = ref(null);
      let promise: any = null;
      let resolve: Ref<any> = ref(null);
      let html = document.querySelector('html');

      let resultBlock: Ref<any> = ref(null);
      let slotBlock: Ref<any> = ref(null);

      onMounted(() => {
        html!.style.overflow = 'hidden';
        promise = show();
        promise.then((res: any) => {
          result.value = res;
          setTimeout(() => {
            emit('hideModal')
          }, 2000)
        })
      });

      onUnmounted(() => {
        setTimeout(() => html!.style.overflow = 'auto', 500)
      });

      function show() {
        return new Promise((res) => {
          resolve.value = function (value: any) {
            res(value)
          }
        })
      }

      return {
        result,
        resolve,

        resultBlock,
        slotBlock,
      }
    },
  })
</script>

<style scoped lang="sass">
.modal
  position: absolute
  left: 0
  top: 0
  width: 100vw
  height: 100vh
  background-color: rgba(#000, .3)
  &__
    &block
      width: 25rem
      transition: width .2s
      padding: 1rem
      background-color: #fff
      position: absolute
      left: 50%
      bottom: 50%
      transform: translate(-50%, 50%)
      min-width: 15rem
      min-height: 10rem
      border-radius: 0.5rem
      display: flex
      align-items: center
      justify-content: center
      flex-direction: column

.block-enter-active
  animation: bounce-in 1s
.block-leave-active
  animation: bounce-in 0.5s reverse

@keyframes bounce-in
  0%
    bottom: 100%
    transform: scaleY(0) translate(-50%, 50%)
  100%
    bottom: 50%
    transform: scaleY(1) translate(-50%, 50%)
</style>