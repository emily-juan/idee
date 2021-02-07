<template>
  <a-layout-sider
    :theme="sideTheme"
    :class="['side-menu', 'beauty-scroll', isMobile ? null : 'shadow']"
    width="256px"
    :collapsible="collapsible"
    v-model="collapsed"
    :trigger="null"
  >
    <div :class="['logo', theme]">
      <router-link to="/dashboard/workplace">
        <img src="@/assets/img/logo.png" />
        <h1>{{ systemName }}</h1>
      </router-link>
    </div>
    <i-menu
      :theme="theme"
      :collapsed="collapsed"
      :options="menuData"
      @select="onSelect"
      @contextmenu="onContextmenu"
      class="menu"
    />
    <contextmenu
      :itemList="menuItemList"
      :visible.sync="menuVisible"
      @select="onMenuSelect"
    />
  </a-layout-sider>
</template>

<script>
import IMenu from './menu';
import Contextmenu from '@/components/menu/Contextmenu';
import { mapState } from 'vuex';
export default {
  name: 'SideMenu',
  components: { IMenu, Contextmenu },
  data() {
    return {
      menuVisible: false,
    };
  },
  props: {
    collapsible: {
      type: Boolean,
      required: false,
      default: false,
    },
    collapsed: {
      type: Boolean,
      required: false,
      default: false,
    },
    menuData: {
      type: Array,
      required: true,
    },
    theme: {
      type: String,
      required: false,
      default: 'dark',
    },
  },
  computed: {
    sideTheme() {
      return this.theme == 'light' ? this.theme : 'dark';
    },
    menuItemList() {
      return [
        { key: '1', icon: 'vertical-right', text: 'ssss' },
        { key: '2', icon: 'vertical-left', text: 'aaaaa' },
        { key: '3', icon: 'close', text: 'bbnbb' },
        { key: '4', icon: 'sync', text: 'cccccc' },
      ];
    },
    ...mapState('setting', ['isMobile', 'systemName']),
  },
  methods: {
    onSelect(obj) {
      this.$emit('menuSelect', obj);
    },
    onContextmenu(e) {
      // if (pageKey) {
      e.preventDefault();
      // e.meta = pageKey;
      this.menuVisible = true;
      // }
    },
    onMenuSelect(key, target, pageKey) {
      console.log(key, target, pageKey);
      // switch (key) {
      //   case '1': this.closeLeft(pageKey); break
      //   case '2': this.closeRight(pageKey); break
      //   case '3': this.closeOthers(pageKey); break
      //   case '4': this.refresh(pageKey); break
      //   default: break
      // }
    },
  },
};
</script>

<style lang="less" scoped>
@import 'index';
</style>
