<template>
<div class="home">
  <!-- 内容开始 -->
  <article>
    <section class="index-top">
      <img :src = 'logoSrc' >
      <a href="javascript:;" class="btnType1 logout" @click="logout">退出</a>
    </section>
    <section class="index-main vm-1px-tb">
      <a href="javascript:;" class="vm-1px-r">
          <span>a</span>
      </a>
      <a href="javascript:;" class="vm-1px-r">
          <span>b</span>
      </a>
      <a href="javascript:;" class="vm-1px-r">
          <span>c</span>
      </a>
      <a href="javascript:;">
          <span>d</span>
      </a>
    </section>
    <section class="index-main vm-1px-b">
      <ul>
      <li class="vm-1px-r">
          <a href="javascript:;" class="btnType1" @click="getUserInfo">用户信息</a>
      </li>
      <li class="vm-1px-r">
          <a href="javascript:;" class="btnType1">按钮2</a>
      </li>
      <li class="vm-1px-r">
          <a href="javascript:;" class="btnType1">按钮3</a>
      </li>
      <li>
          <a href="javascript:;" class="btnType1">按钮4</a>
      </li>
      </ul>
    </section>
  </article>
  <!-- 内容结束 -->
</div>
</template>

<script>
import getDpr from '@/utils/getDpr';
import {mapActions} from 'vuex';
import {LOGOUT, GET_USER_INFO} from '@/constants/apiTypes';
export default {
  name: 'home',
  data() {
    return{
      logoSrc: null,
    }
  },
  created(){
    const dpr = getDpr();
    this.logoSrc = require('@/assets/logo@'+dpr+'x.png');
  },
  mounted(){
  },
  methods: {
    ...mapActions([LOGOUT, GET_USER_INFO]),
    logout() {
      this[LOGOUT]().then(res => {
        this.$router.replace({path: '/'}, () => {
          this.$vux.toast.show('成功退出!');
          // location.reload();
        });
      });
    },
    getUserInfo() {
      this[GET_USER_INFO]().then(res => {
        console.log('getUserInfo:::res:::', res);
        const resData = res.data || {};
        if (res.success) {
          this.$vux.alert.show({
            title: `Hello ${resData.nick}`,
            content: JSON.stringify(res.data),
          });
        }
      }).catch(error => {
        console.log('getUserInfo:::error:::', error);
      });
    }
  }
}
</script>
<style lang="less" scoped>
  @import '~@/styles/modules/home.less';
  .logout{
    width:140px; 
    height:56px; 
    line-height:56px; 
    font-size:32px; 
    color:#fff; 
    text-align:center; 
    display: block;
    position: absolute;
    right: 20px;
    top: 20px;
    &.btnType1{
      display:block; 
      background:#00beda; 
      border-radius:6px; 
      color:#fff; 
      text-decoration:none; 
      cursor:pointer; 
      font-size:32px; 
      &:hover{
        background:#089555; 
        color:#fff; 
        text-decoration:none;
      }
    }
  }
</style>
