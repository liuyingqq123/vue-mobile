<template>
  <div id="app">
    <div v-transfer-dom>
      <loading v-model="isLoading"></loading>
    </div>
    <router-view/>
  </div>
</template>

<script>
import { Loading, TransferDom } from 'vux'
import { mapState } from 'vuex'

export default {
  directives: {
    TransferDom
  },
  components: {
    Loading
  },
  computed: {
    ...mapState({
      isLoading: state => state.vux.isLoading
    })
  }
}
</script>
<style lang="less">
  #app{
    background: inherit;
    height: 100%;
  }
</style>
