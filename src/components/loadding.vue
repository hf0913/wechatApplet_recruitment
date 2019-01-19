<template>
    <div class="modalFrame" v-show="isLoadding">
      <wux-spin wux-class="spin" size="large" class="wuxSpin"/>
      <div class="dataLoadding">{{loaddingText}}</div>
    </div>
</template>
<script>
export default {
    name: 'Loadding',
    data() {
        return {
            
        }
    },
    props: ['isLoadding', 'loaddingText']
}
</script>

<style>
  .wuxSpin {
    position: absolute;
    top: 40%;
    left: 50%;
  }
  .modalFrame {
    position: absolute;
    top:0;
    left:0;
    height: 100%;
    width: 100%;
    background: rgba(241,241,241,.5);
    z-index: 999
  }
  .dataLoadding{
    position: absolute;
    top: 48%;
    left: 30%;
  }
</style>