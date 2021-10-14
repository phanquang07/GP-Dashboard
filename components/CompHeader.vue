<template>
  <a-layout-header class="header">
    <a-row>
      <a-col :span="4" class="header-dashboard-title">
        <h2>Dashboard</h2>
      </a-col>
      <a-col :span="20" class="header-info-user">
        <div class="header-user-name">
          <a-avatar style="color: #fff; backgroundColor: #F3A100">SC</a-avatar>
          <span class="header-user-fullName">{{ userName }}</span>
        </div>
        <div class="header-region">
          <!-- <img :src="require(`/assets/images/${productItem.img}`)" /> -->
          <div class="header-user-active">
            <img src="~assets/images/user_active.png" />
          </div>
          <div class="header-region-flag">
            <img src="~assets/images/region.jpg" alt="region" />
          </div>
          <span class="header-region-name">VN</span>
        </div>
      </a-col>
    </a-row>
  </a-layout-header>
</template>

<script>
export default {
  data() {
    return {
      userName: "Sun Cometics",
    };
  },
};
</script>

<style>
.header {
  padding: 0 20px !important;
  height: 50px;
  background: var(--white-color);
  box-shadow: 0px 1px 12px rgba(0, 34, 112, 0.12);
}

.header-dashboard-title h2 {
  line-height: 50px;
  font-size: 17px;
  font-weight: 700;
}

.header-info-user {
  line-height: 50px;
  display: flex;
  justify-content: flex-end;
}

.header-region {
  display: flex;
  margin-left: 37px;
}

.header-region-flag {
  margin-left: 12px;
  margin-right: 6px;
}

.header-user-avt {
  font-size: 1.4rem;
  font-weight: 700;
}
</style>