<template>
  <div class="header">
    <div class="minW flexB">
      <div class="logo"><img src="@/assets/img/defis.png" alt=""></div>
      <div class="nav flexB" v-if="!$store.state.app.minScreen">
        <span @click="handleToDiv('vision')">{{ $t('nav.vision') }}</span>
        <span @click="handleToDiv('dfs')">{{ $t('nav.dfs') }}</span>
        <span @click="handleToDiv('project')">{{ $t('nav.project') }}</span>
        <!-- <span>{{ $t('nav.faq') }}</span> -->
        <span v-if="language !== 'en'" @click="handleChangeLang('en')">EN</span>
        <span v-else @click="handleChangeLang('zh-CN')">CN</span>
      </div>
      <!-- Mobile -->
      <div class="flex" v-else>
        <img class="img" src="@/assets/img/more.png" alt="" @click="handleShowNav">
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'myHeader',
  data() {
    return {
    }
  },
  computed:{
    ...mapState({
      // 箭头函数可使代码更简练
      language: state => state.app.language,
    })
  },
  methods: {
    handleShowNav() {
      this.$emit('listenShowNav', true)
    },
    handleChangeLang(type) {
      this.$i18n.locale = type;
      this.$store.dispatch('setLanguage', type);
    },
    handleToDiv(name) {
      this.$emit('listenToDiv', name)
    }
  }
}
</script>

<style lang="scss" scoped>
.header{
  padding: 13px auto;
  .minW{
    height: 80px;
    min-width: 1200px;
    width: 1200px;
    margin: auto;
  }
  .flexB{
    display: flex;
    align-content: center;
    justify-content: space-between;
  }
  .logo{
    height: 80px;
    width: 200px;
    display: flex;
    align-items: center;
    img{
      width: 100%;;
    }
  }
  .nav{
    span{
      color: #000;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-left: 30px;
      font-size: 16px;
      font-weight: bold;
      letter-spacing: 0.89px;
      cursor: pointer;
    }
  }
}

@media screen  and (max-width: 750px) {
  .header{
    .minW{
      width: 100%;
      min-width: 100%;
    }
    .flex{
      display: flex;
      align-items: center;justify-content: center;
      .img{
        cursor: pointer;
        width: 32px;
        margin-right: 20px;
      }
    }
  }
}
</style>