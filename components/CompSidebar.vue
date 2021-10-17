<template>
  <a-layout-sider v-model="collapsed" :trigger="null" collapsible>
    <div :class="['sidebar', collapsed ? 'isClose' : 'isOpen']">
      <nuxt-link to="/">
        <h1 class="logo-dashboard">
          <img src="~/assets/images/logo.png" alt="Go Page" />
        </h1>
      </nuxt-link>
      <a-menu
        :default-selected-keys="['1']"
        :default-open-keys="['sub1']"
        mode="inline"
        theme="dark"
        :inline-collapsed="collapsed"
      >
        <a-button
          type="primary"
          shape="circle"
          style="margin-bottom: 16px"
          @click="toggleCollapsed"
        >
          <a-icon :type="collapsed ? 'right' : 'left'" />
        </a-button>

        <a-menu-item key="1">
          <nuxt-link to="/">
            <a-icon type="appstore" />
            <span>Dashboard</span>
          </nuxt-link>
        </a-menu-item>
        <a-menu-item key="2">
          <nuxt-link to="/stats">
            <a-icon type="line-chart" />
            <span>Thống kê</span>
          </nuxt-link>
        </a-menu-item>
        <a-menu-item key="3">
          <nuxt-link to="/sell-products">
            <a-icon type="shopping-cart" />
            <span style="color: #fff">Bán hàng</span>
          </nuxt-link>
        </a-menu-item>
        <a-menu-item key="4">
          <nuxt-link to="/order-products">
            <a-icon type="profile" />
            <span>Đơn hàng</span>
          </nuxt-link>
        </a-menu-item>
        <a-sub-menu key="sub1">
          <span slot="title">
            <a-icon type="inbox" />
            <span>Sản phẩm</span>
          </span>
          <a-menu-item key="5">
            <nuxt-link to="/products-management">Quản lý sản phẩm</nuxt-link>
          </a-menu-item>
          <a-menu-item key="6">
            <nuxt-link to="/import-products">Nhập hàng</nuxt-link>
          </a-menu-item>
          <a-menu-item key="7">
            <nuxt-link to="/export-products">Xuất hàng</nuxt-link>
          </a-menu-item>
          <a-menu-item key="8">
            <nuxt-link to="/products-sales-history">Lịch sử bán hàng</nuxt-link>
          </a-menu-item>
          <a-menu-item key="9">
            <nuxt-link to="/warehouse">Kho hàng</nuxt-link>
          </a-menu-item>
          <a-menu-item key="10">
            <nuxt-link to="/warehouse-transfer">Chuyển kho</nuxt-link>
          </a-menu-item>
        </a-sub-menu>
        <a-menu-item key="11">
          <nuxt-link to="/customers">
            <a-icon type="team" />
            <span>Khách hàng</span>
          </nuxt-link>
        </a-menu-item>
        <a-menu-item key="12">
          <nuxt-link to="/setting">
            <a-icon type="setting" />
            <span>Cài đặt</span>
          </nuxt-link>
        </a-menu-item>
      </a-menu>
    </div>
  </a-layout-sider>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      collapsed: false,
    };
  },
  methods: {
    toggleCollapsed() {
      this.collapsed = !this.collapsed;
    },
  },
};
</script>

<style>
.ant-layout-sider {
  background: var(--sidebar-color);
  transition: none;
}

.ant-layout-sider-dark {
  flex: 0 0 240px !important;
  max-width: 240px !important;
  min-width: 240px !important;
  width: 240px !important;
}

.ant-layout-sider-collapsed {
  flex: 0 0 69px !important;
  width: 69px !important;
  min-width: 69px !important;
  max-width: 69px !important;
}

.sidebar {
  position: fixed;
  height: 100%;
  background: var(--sidebar-color);
}

.sidebar .ant-menu-dark {
  color: #fff !important;
  background: var(--sidebar-color) !important;
}

.logo-dashboard {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  overflow: hidden;
  transition: all 0.3s ease;
  margin: 24px 0px;
}

.sidebar.isClose .logo-dashboard {
  display: block;
  width: 52px;
  margin: 24px 10px;
}

.sidebar .ant-btn-circle {
  position: absolute;
  top: 140px;
  min-width: 22px !important;
  height: 22px;
  font-size: 10px;
  right: -11px;
  margin-bottom: 0 !important;
  color: var(--sidebar-color);
  background: var(--white-color);
  border: none;
}

.sidebar .ant-menu {
  padding: 0 13px !important;
  background: var(--sidebar-color);
}

.sidebar.isClose .ant-menu-inline-collapsed {
  width: 43px;
}

.sidebar .ant-menu-item {
  width: 100%;
  max-width: 214px;
  border-radius: 10px;
  padding-left: 13px !important;
  padding-right: 0;
  height: 45px !important;
  line-height: 45px !important;
}

.ant-menu-inline .ant-menu-item:not(:last-child) {
  margin-bottom: 0;
}

.ant-menu-vertical .ant-menu-item:not(:last-child) {
  margin-bottom: 0;
}

.sidebar.isClose .ant-menu-item {
  padding: 0 13px !important;
  width: 43px;
}

/* icon */

.ant-menu-item .anticon {
  margin-right: 14px;
  width: 15px;
  opacity: 77%;
}

.ant-menu-submenu .anticon {
  margin-right: 14px;
  width: 15px;
  opacity: 77%;
}

/* menu-submenu */

.sidebar .ant-menu-submenu {
  border-radius: 10px;
}

.sidebar.isClose .ant-menu-submenu {
  border-radius: 10px;
  width: 43px;
}

.sidebar.isClose .ant-menu-submenu:hover {
  background: var(--blue-color) !important;
  padding: 0 !important;
}

.sidebar.isClose .ant-menu-submenu-active {
  color: #fff !important;
  background: var(--blue-color) !important;
}

.sidebar .ant-menu-submenu-title {
  padding-left: 13px !important;
  padding-right: 0;
  border-radius: 10px;
  height: 45px !important;
  line-height: 45px !important;
  margin-bottom: 0;
}

.sidebar .ant-menu-submenu-title:hover {
  background: var(--blue-color);
}

.sidebar .ant-menu-submenu-title .ant-menu-submenu-arrow {
  right: 0;
}

.sidebar.isClose .ant-menu-submenu-title {
  padding: 0 13px !important;
  width: 43px;
  margin-bottom: 0;
  margin-top: 4px;
}

/* menu sub */

.sidebar .ant-menu-submenu .ant-menu-item {
  margin-left: 19px !important;
  max-width: 182px;
}

.sidebar.isClose .ant-menu-sub {
  width: 43px;
}

.sidebar .ant-menu-inline.ant-menu-sub {
  background: var(--sidebar-color);
  box-shadow: none;
}

.ant-menu-item:hover {
  background: var(--blue-color) !important;
}

.ant-menu-item-selected {
  background: var(--blue-color) !important;
}

.ant-menu-dark .ant-menu-item,
.ant-menu-dark .ant-menu-item-group-title,
.ant-menu-dark .ant-menu-item > a {
  color: #fff;
}

.ant-menu-dark,
.ant-menu-dark .ant-menu-sub {
  color: #fff;
}

.isOpen {
  width: 240px;
}

.isClose {
  width: 69px;
}

.ant-menu-submenu-popup {
  left: 71px !important;
}

.sidebar.isClose .ant-menu-dark,
.ant-menu-dark .ant-menu-sub {
  background: var(--sidebar-color);
}

.ant-menu-vertical.ant-menu-sub {
  min-width: 190px !important;
  border-radius: 10px !important;
  padding: 9px 12px;
}

.ant-menu-vertical.ant-menu-sub .ant-menu-item {
  height: 45px;
  line-height: 45px;
  border-radius: 10px;
}

.ant-tooltip {
  left: 66px !important;
}
</style>
