<template>
  <div class="stats-page">
    <div class="title">
      <h2>{{ title }}</h2>
    </div>
    <div class="list-stats" v-for="(item, index) in statsTime" :key="index">
      <h3>{{ item.time }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  layout: "dashboard",
  layout(context) {
    return "dashboard";
  },
  data() {
    return {
      title: "Thống kê",
      statsTime: [
        {
          time: "30days",
        },
        {
          time: "7days",
        },
        {
          time: "1days",
        },
      ],
    };
  },
  // Hooks
  // Chạy trước khi hệ thống phản ứng hoạt động
  beforeCreate() {
    console.log("beforeCreate", this.title, document.querySelector('.list-stats'));
  },
  // Gọi API, ajax
  created() {
    console.log("created", this.title, document.querySelector('.list-stats'));
  },
  beforeMount() {
    console.log("beforeMount", this.title, document.querySelector('.list-stats'));
  },
  // Chỉ truy xuất được DOM trong mounted => có thể sử dụng jQuery
  mounted() {
    console.log("mounted", this.title, document.querySelector('.list-stats').classList);
  },
  // Làm gì đó trước khi thay đổi dữ liệu
  beforeUpdate() {
    console.log("beforeUpdate");
    this.title;
  },
  // Làm gì đó sau khi thay đổi dữ liệu
  updated() {
    console.log("updated");
    this.title;
  },
  // beforeUnmount() {
  //   console.log("beforeActivated");
  // },
  // unmounted() {
  //   console.log("unmounted");
  // },
  // dừng đối tượng Vue
  // activated() {
  //   console.log("activated");
  // },
  // deactivated() {
  //   console.log("deActivated");
  // },
  // Hủy bỏ đối tượng Vue
  // beforeDestroy() {
  //   console.log("beforeDestroy");
  // },
  // destroyed() {
  //   console.log("destroyed");
  // }
};
</script>

<style>
</style>