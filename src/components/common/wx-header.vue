<template>
  <!--复兴性高，数据交互比较频繁-->
  <div id="wx-header">
    <!--右上角图标-->
    <div class="other">
      <!--只在“微信”页显示 更多图标-->
      <span class="iconfont icon-add" v-show="$route.path==='/'" v-on:click="$store.commit('toggleTipsStatus')"></span>
      <!--只在“联系人”页显示 显示添加好友图标-->
      <router-link tag="span" to="/contact/add-friend" class="iconfont icon-friends" v-show="$route.path==='/contact'"></router-link>
      <!--只在“添加朋友”页显示 -->
      <span v-show="$route.path==='/contact/new-friends'">添加朋友</span>
      <!--下面这个好像有些多余 sad -->
      <span class="iconfont icon-chat-friends" v-show="$route.path==='/wechat/dialogue'"></span>
      <!-- 更多图标的菜单 附带过渡效果-->
      <ul class="tips-menu" :class="[$store.state.tipsStatus?'tips-open':'tips-close']" v-on:click="$store.commit('toggleTipsStatus', -1)">
        <li>
          <span class="iconfont icon-tips-xiaoxi"></span>
          <div>发起群聊</div>
        </li>
        <router-link tag="li" to="/wehchat/add-friend">
          <span class="iconfont icon-friends"></span>
          <div>添加朋友</div>
        </router-link>
      </ul>
    </div>
    <div class="center">
      <!--显示当前页的名字-->
      <span>{{$store.state.currentPageName}}</span>
      <!--微信群 显示群名以及成员人数 好像和 dialogue 组件 写重了 sad -->
      <span class="parentheses" v-show='$route.query.group_num&&$route.query.group_num!=1'>{{$route.query.group_num}}</span>
    </div>
  </div>
</template>
<script>
    export default {
        props: ["pageName"],
        data() {
            return {
                // 暂且用不到
                chatCount: true
            }
        },
        methods: {
            // 暂且用不到 先留着
            goBack() {
              //保证返回操作后正确显示页面名称
              // this.$store.commit("setPageName", this.$store.state.backPageName)
              this.$router.go(-1);
            }
        }
    }
</script>
<style>

</style>
