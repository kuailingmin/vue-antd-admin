<template>
  <a-layout>
    <drawer v-if="isMobile" :openDrawer="collapsed" @change="onDrawerChange">
      <sider-menu :theme="theme" :menuData="menuData" :collapsed="false" :collapsible="false" @menuSelect="onMenuSelect"/>
    </drawer>
    <sider-menu :theme="theme" v-else-if="layout === 'side'" :menuData="menuData" :collapsed="collapsed" :collapsible="true" />
    <drawer :open-drawer="showSetting" placement="right"  @change="onSettingDrawerChange">
      <div class="setting" slot="handler">
        <a-icon :type="showSetting ? 'close' : 'setting'" />
      </div>
      <setting />
    </drawer>
    <a-layout>
      <global-header :menuData="menuData" :collapsed="collapsed" @toggleCollapse="toggleCollapse"/>
      <a-layout-content :style="{minHeight: minHeight, margin: '24px 24px 0'}">
        <slot></slot>
      </a-layout-content>
      <a-layout-footer style="padding: 0px">
        <global-footer />
      </a-layout-footer>
    </a-layout>
  </a-layout>
</template>

<script>
import ALayout from 'ant-design-vue/es/layout'
import GlobalHeader from './GlobalHeader'
import AIcon from 'ant-design-vue/es/icon/icon'
import IMenu from '../menu/menu'
import GlobalFooter from './GlobalFooter'
import Drawer from '../tool/Drawer'
import SiderMenu from '../menu/SiderMenu'
import Setting from '../setting/Setting'

const ALayoutSider = ALayout.Sider
const ALayoutHeader = ALayout.Header
const ALayoutContent = ALayout.Content
const ALayoutFooter = ALayout.Footer
const minHeight = window.innerHeight - 64 - 24 - 122

let menuData = []

export default {
  name: 'GlobalLayout',
  components: {
    Setting,
    SiderMenu,
    Drawer,
    GlobalFooter,
    AIcon,
    GlobalHeader,
    ALayout,
    ALayoutSider,
    ALayoutHeader,
    ALayoutContent,
    ALayoutFooter,
    IMenu},
  data () {
    return {
      minHeight: minHeight + 'px',
      collapsed: false,
      menuData: menuData,
      showSetting: false
    }
  },
  computed: {
    isMobile () {
      return this.$store.state.setting.isMobile
    },
    theme () {
      return this.$store.state.setting.theme
    },
    layout () {
      return this.$store.state.setting.layout
    }
  },
  methods: {
    toggleCollapse () {
      this.collapsed = !this.collapsed
    },
    onDrawerChange (show) {
      this.collapsed = show
    },
    onMenuSelect () {
      this.toggleCollapse()
    },
    onSettingDrawerChange (val) {
      this.showSetting = val
    }
  },
  beforeCreate () {
    menuData = this.$router.options.routes.find((item) => item.path === '/').children
  }
}
</script>

<style lang="less" scoped>
  .setting{
    background-color: #1890ff;
    color: #fff;
    border-radius: 5px 0 0 5px;
    line-height: 40px;
    font-size: 22px;
    width: 40px;
    height: 40px;
    box-shadow: -2px 0 8px rgba(0, 0, 0, 0.15);
  }
</style>
