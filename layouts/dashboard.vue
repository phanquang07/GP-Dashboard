<template>
  <div class="app">
    <a-layout id="components-layout-demo-custom-trigger">
      <!-- Sidebar -->
      <comp-sidebar />
      <a-layout>
        <!-- Header -->
        <comp-header :userName="userName" :abbreviation="abbreviation" :region="region" />
        <!-- Main -->
        <a-layout-content class="main">
          <a-row :gutter="[14, 14]">
            <a-col :xl="16" class="content-left">
              <Nuxt />
            </a-col>
            <a-col :xl="8" class="content-right">
              <comp-content-right :userName="userName" />
            </a-col>
          </a-row>
        </a-layout-content>
      </a-layout>
    </a-layout>
  </div>
</template>

<script>
import CompSidebar from "@/components/CompSidebar.vue";
import CompHeader from "@/components/CompHeader.vue";
import CompContentRight from '@/components/CompContentRight.vue';
export default {
  components: {
    CompSidebar,
    CompHeader,
    CompContentRight,
  },
  data() {
    return {
       userName: 'Sun Cometics',
       abbreviation: 'SC',
       region: 'VN'
    }
  }
};
</script>

<style>
/* Main */
.ant-layout-content {
  margin: 0;
  padding: 14px 10px;
  background: #e5e5e5;
  min-height: auto !important;
}
.main {
  padding: 14px 20px;
}
</style>