<template>
  <a-layout id="components-layout-demo-custom-trigger">
    <comp-sidebar />
    <a-layout>
      <a-layout-header class="header">
        <a-row>
          <a-col :span="4" class="header-dashboard-title">
            <h2>Dashboard</h2>
          </a-col>
          <a-col :span="20" class="header-info-user">
            <div class="header-user-name">
              <a-avatar style="color: #fff; backgroundColor: #F3A100">SC</a-avatar>
              <span class="header-user-fullName">{{ user.name }}</span>
            </div>
            <div class="header-region">
              <div class="header-user-active">
                <img :src="require(`/assets/images/${user.avt}`)" />
              </div>
              <div class="header-region-flag">
                <img :src="require(`/assets/images/${user.regionImg}`)" />
              </div>
              <span class="header-region-name">VN</span>
            </div>
          </a-col>
        </a-row>
      </a-layout-header>
      <a-layout-content class="main">
        <a-row :gutter="[14, 14]">
          <a-col :xl="{ span:16 }" class="content-left">
            <!-- compare-stat -->
            <section class="compare-stats">
              <a-form layout="inline" class="form-compare">
                <label for="compare-stats" style="line-height: 35px">So sánh thống kê:</label>
                <a-form-item class="form-item">
                  <a-select default-value="30days" style="width: 126px">
                    <a-select-option value="30days">30 ngày qua</a-select-option>
                    <a-select-option value="1week">tuần qua</a-select-option>
                    <a-select-option value="1day">ngày qua</a-select-option>
                  </a-select>
                </a-form-item>
                <a-form-item class="form-item form-item-two">
                  <label for="labelWith">với</label>
                  <a-select default-value="30days" style="width: 154px">
                    <a-select-option value="30days">30 ngày trước đó</a-select-option>
                    <a-select-option value="1week">tuần trước đó</a-select-option>
                    <a-select-option value="1day">ngày trước đó</a-select-option>
                  </a-select>
                </a-form-item>
                <a-form-item class="form-item">
                  <a-select default-value="all" style="width: 140px">
                    <a-select-option value="all">Tất cả các kho</a-select-option>
                    <a-select-option value="ware1">Kho 1</a-select-option>
                    <a-select-option value="ware2">Kho 2</a-select-option>
                  </a-select>
                </a-form-item>
              </a-form>
            </section>
            <!-- card-stats -->
            <section class="card-stats">
              <a-row :gutter="[12, 12]">
                <a-col
                  :lg="{ span: 8 }"
                  :md="{ span: 12 }"
                  class="card-stats-col"
                  v-for="(statsItem, idx) in statsList"
                  :key="idx"
                >
                  <div
                    :class="['card-stats-item', idx === 0 ? 'bg-purple'  : idx === 1 ? 'bg-pink' : idx === 2 ? 'bg-orange' : 'bg-white' ]"
                  >
                    <div class="revenue-stats-text">
                      <h3>
                        {{ statsItem.title }}
                        <a-icon class="question-icon" type="question-circle" />
                      </h3>
                      <p class="number-data">{{ statsItem.value }}</p>
                      <p class="percent-data">
                        <a-icon :type="statsItem.trend === 0 ? 'arrow-down' : 'arrow-up' " />
                        {{ statsItem.valueTrend }}
                      </p>
                    </div>
                    <div class="icon-right">
                      <a-icon
                        :type="statsItem.iconRight === 0 ? 'dollar' : statsItem.iconRight === 1 ? 'medicine-box' : statsItem.iconRight === 2 ? 'team' : 'icon-none' "
                      />
                      <a-progress
                        v-if="statsItem.progress === 0"
                        type="circle"
                        :percent="18"
                        :width="78"
                      />
                    </div>
                  </div>
                </a-col>
              </a-row>
            </section>
            <!-- stats-chart -->
            <section class="stats-chart">
              <div class="card-container">
                <a-tabs :default-active-key="tabDefault" type="card">
                  <a-tab-pane
                    class="stats-chart-item"
                    v-for="(tabsItem, idx) in tabsList"
                    :key="idx+1"
                  >
                    <span slot="tab" class="stats-chart-content">
                      <h3 class="stats-chart-title">{{ tabsItem.title }}</h3>
                      <p class="stats-chart-value">{{ tabsItem.value }}</p>
                      <a-icon
                        class="stats-chart-trend"
                        :type=" tabsItem.trend === 0 ? 'arrow-down' : 'arrow-up' "
                      />
                      <span class="stats-chart-valueTrend">{{ tabsItem.valueTrend }}</span>
                    </span>
                    <div class="line-chart">
                      <LineChartD />
                    </div>
                  </a-tab-pane>
                </a-tabs>
              </div>
            </section>
            <!-- top-product-staff -->
            <section class="top-product-staff" v-for="(item, idx) in topList" :key="idx">
              <a-row class="product-staff-title">
                <a-col :sm="{ span: 18 }" class="product-staff-title-item">
                  <h2>{{ item.title }}</h2>
                </a-col>
                <a-col :sm="{ span: 6 }" class="product-staff-title-item">
                  <NuxtLink to="/">
                    {{ item.linkName }}
                    <a-icon type="double-right" />
                  </NuxtLink>
                </a-col>
              </a-row>
              <a-row :gutter="[0, 6]" class="product-staff-item product-staff-heading">
                <a-col :xs="{ span: 1 }" class="orders">
                  <h3>#</h3>
                </a-col>
                <a-col :xs="{ span: 11 }">
                  <h3>{{ item.productTitle }}</h3>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <h3>{{ item.revenueTitle }}</h3>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <h3>{{ item.completedOrdersTitle }}</h3>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <h3>{{ item.canceledOrdersTitle}}</h3>
                </a-col>
              </a-row>
              <a-row
                :gutter="[0, 6]"
                v-for="(productItem, idx) in item.listProduct"
                :key="idx"
                class="product-staff-item staffs products"
              >
                <a-col :xs="{ span: 1 }" class="orders">
                  <p>{{ productItem.orderNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 11 }" class="product-staff-name-wrap">
                  <div class="products-img">
                    <img :src="require(`/assets/images/${productItem.img}`)" />
                  </div>
                  <div class="products-text">
                    <p>{{ productItem.productName }}</p>
                    <p>{{ productItem.productType }}</p>
                  </div>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ productItem.revenueNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ productItem.completedOrdersNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ productItem.canceledOrdersNumber }}</p>
                </a-col>
              </a-row>
              <a-row
                :gutter="[0, 6]"
                v-for="(staffItem, idx) in item.listStaff"
                :key="idx"
                class="product-staff-item staffs"
              >
                <a-col :xs="{ span: 1 }" class="orders">
                  <p>{{ staffItem.orderNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 11 }" class="product-staff-name-wrap">
                  <div class="staffs-img">
                    <img :src="require(`/assets/images/${staffItem.img}`)" />
                  </div>
                  <div class="staffs-text">
                    <p>{{ staffItem.staffName }}</p>
                  </div>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ staffItem.revenueNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ staffItem.completedOrdersNumber }}</p>
                </a-col>
                <a-col :xs="{ span: 4 }">
                  <p>{{ staffItem.canceledOrdersNumber }}</p>
                </a-col>
              </a-row>
            </section>
          </a-col>
          <!-- content-right -->
          <a-col :xl="{ span:8 }" class="content-right">
            <!-- sayHello -->
            <section class="sayHello">
              <h2 class="sayHello-title">Xin chào! {{ user.name }}</h2>
              <p>
                Gói đang sử dụng:
                <NuxtLink to="/">{{ user.optionLink }}</NuxtLink>
              </p>
            </section>
            <!-- stats-info -->
            <div class="stats-info">
              <a-row :gutter="[14, 14]">
                <a-col
                  :xl="{ span: 24 }"
                  :lg="{ span: 12 }"
                  :md="{ span: 24 }"
                  v-for="(statsInfoItem, idx) in statsInfoList"
                  :key="idx"
                >
                  <section class="stats-info-item stats-today">
                    <h2>{{ statsInfoItem.title }}</h2>
                    <a-row :gutter="[0, 12]" class="stats-today-item">
                      <a-col
                        :xs="{ span: 7 }"
                        class="revenue-today-text"
                      >{{ statsInfoItem.revenueText }}</a-col>
                      <a-col
                        :xs="{ span: 17 }"
                        class="revenue-today-value"
                        style="text-align: right"
                      >{{ statsInfoItem.revenueValue }}</a-col>
                    </a-row>
                    <a-row
                      v-if="statsInfoItem.cardBlueId === 1"
                      :gutter="[12, 12]"
                      class="stats-today-item card-blue"
                    >
                      <a-col
                        :sm="{ span: 12 }"
                        class="stats-today-col"
                        v-for="(statsTodayItem, idx) in statsInfoItem.cardStatsToday"
                        :key="idx"
                      >
                        <div class="quantity-stats-today-item">
                          <a-icon :type="statsTodayItem.icon === 0 ? 'gift' : 'user' " />
                          <div class="orders">
                            <p class="orders-text">{{ statsTodayItem.title }}</p>
                            <p class="orders-number">{{ statsTodayItem.value }}</p>
                          </div>
                        </div>
                      </a-col>
                    </a-row>
                    <a-row
                      v-if="statsInfoItem.selectWarehouse === 1"
                      :gutter="[12, 12]"
                      class="warehouse-info"
                    >
                      <a-col>
                        <a-select
                          default-value="warehouse1"
                          class="warehouse-info-selection"
                          style="width: 50%"
                        >
                          <a-select-option value="warehouse1">Kho 1</a-select-option>
                          <a-select-option value="warehouse2">Kho 2</a-select-option>
                          <a-select-option value="warehouse3">Tất cả các kho</a-select-option>
                        </a-select>
                      </a-col>
                    </a-row>
                    <a-row :gutter="[12, 12]" class="stats-today-item">
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-text"
                      >{{ statsInfoItem.canceledText }}</a-col>
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-monney"
                      >{{ statsInfoItem.canceledValue }}</a-col>
                    </a-row>
                    <a-row :gutter="[12, 12]" class="stats-today-item">
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-text"
                      >{{ statsInfoItem.closedText }}</a-col>
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-monney"
                      >{{ statsInfoItem.closedValue }}</a-col>
                    </a-row>
                    <a-row :gutter="[12, 12]" class="stats-today-item">
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-text"
                      >{{ statsInfoItem.succeededText }}</a-col>
                      <a-col
                        :xs="{ span: 12 }"
                        class="quantity-today-monney"
                      >{{ statsInfoItem.succeededValue }}</a-col>
                    </a-row>
                  </section>
                </a-col>
              </a-row>
            </div>
          </a-col>
        </a-row>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
import CompSidebar from "@/components/CompSidebar.vue";
import LineChartD from "@/components/chartjs/LineChartD.vue";
export default {
  components: {
    CompSidebar,
    LineChartD,
  },
  data() {
    return {
      tabDefault: 1,
      user: {
        avt: "user_active.png",
        name: "Sun Cometics",
        regionImg: "region.jpg",
        optionLink: "Silver",
      },

      // statsList
      statsList: [
        {
          title: "Doanh thu",
          value: "588.000.000 đ",
          trend: 1,
          valueTrend: "16% ~ 67.000.000 đ",
          iconRight: 0,
        },
        {
          title: "Đơn hàng thành công",
          value: "1.426",
          trend: 1,
          valueTrend: "1.6%",
          iconRight: 1,
        },
        {
          title: "Số lượng khách hàng",
          value: "342",
          trend: 0,
          valueTrend: "4.9%",
          iconRight: 2,
        },
        {
          title: "Tiền hàng hoàn",
          value: "89.000.000 đ",
          trend: 1,
          valueTrend: "1.5%",
          iconRight: 0,
        },
        {
          title: "Số lượng đơn hoàn",
          value: "132",
          trend: 0,
          valueTrend: "1.5%",
          iconRight: 1,
        },
        {
          title: "Tỉ lệ đơn hoàn",
          trend: 1,
          valueTrend: "1.5%",
          progress: 0,
        },
      ],
      // tabsList
      tabsList: [
        {
          title: "Doanh thu",
          value: "558.000.000 đ",
          trend: 1,
          valueTrend: "12.7%",
        },
        {
          title: "Lợi nhuận",
          value: "378.000.000 đ",
          trend: 1,
          valueTrend: "4.6%",
        },
        {
          title: "SL Đơn chốt",
          value: "25",
          trend: 0,
          valueTrend: "18.7%",
        },
        {
          title: "Giá trị trung bình",
          value: "930.500 đ",
          trend: 1,
          valueTrend: "6.9%",
        },
        {
          title: "SL bán được",
          value: "1.426",
          trend: 1,
          valueTrend: "1.6%",
        },
        {
          title: "SL bán được TB",
          value: "4.2",
          trend: 0,
          valueTrend: "6.5%",
        },
      ],
      // statsInfoList
      statsInfoList: [
        {
          title: "Thống kê hôm nay",
          revenueText: "Doanh thu:",
          revenueValue: "12.350.000 đ",
          canceledText: "SL đơn hủy / xóa:",
          canceledValue: "0",
          closedText: "SL đơn đã chốt:",
          closedValue: "124",
          succeededText: "SL hàng đã bán:",
          succeededValue: "124",
          cardBlueId: 1,
          selectWarehouse: 0,
          cardStatsToday: [
            {
              icon: 0,
              title: "Đơn hàng",
              value: "134",
            },
            {
              icon: 1,
              title: "Khách hàng",
              value: "52",
            },
          ],
        },
        {
          title: "Thông tin kho",
          closedText: "Giá trị tồn kho:",
          closedValue: "250.000.000 đ",
          canceledText: "SL tồn kho:",
          canceledValue: "1.424",
          cardBlueId: 0,
          selectWarehouse: 1,
        },
      ],
      // topList
      topList: [
        {
          title: "Tốp sản phẩm bán chạy",
          linkName: "Xem tất cả",
          order: "#",
          productTitle: "Tên sản phẩm",
          revenueTitle: "Doanh thu",
          completedOrdersTitle: "SL hàng chốt",
          canceledOrdersTitle: "SL hàng hoàn",
          listProduct: [
            {
              orderNumber: "1",
              img: "products.jpg",
              productName: "Tẩy trang Garnier Micellar Rose Water",
              productType: "Type: Honey",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "2",
              img: "products.jpg",
              productName: "Tẩy trang Garnier Micellar Rose Water",
              productType: "Type: Honey",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "3",
              img: "products.jpg",
              productName: "Tẩy trang Garnier Micellar Rose Water",
              productType: "Type: Honey",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "4",
              img: "products.jpg",
              productName: "Tẩy trang Garnier Micellar Rose Water",
              productType: "Type: Honey",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "5",
              img: "products.jpg",
              productName: "Tẩy trang Garnier Micellar Rose Water",
              productType: "Type: Honey",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
          ],
        },
        {
          title: "Tốp nhân viên doanh số cao",
          linkName: "Xem tất cả",
          order: "#",
          productTitle: "Tên nhân viên",
          revenueTitle: "Doanh thu",
          completedOrdersTitle: "SL hàng chốt",
          canceledOrdersTitle: "SL hàng hoàn",
          listStaff: [
            {
              orderNumber: "1",
              productType: "Type: Honey",
              img: "staffs.jpg",
              staffName: "Nguyễn Thị Thu Hiền",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "2",
              productType: "Type: Honey",
              img: "staffs.jpg",
              staffName: "Nguyễn Việt Anh",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "3",
              productType: "Type: Honey",
              img: "staffs.jpg",
              staffName: "Nguyễn Khánh Chi",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "4",
              productType: "Type: Honey",
              img: "staffs.jpg",
              staffName: "Hồ Xuân Dũng",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
            {
              orderNumber: "5",
              productType: "Type: Honey",
              img: "staffs.jpg",
              staffName: "Phan Xuân Quang",
              revenueNumber: "2.340.000",
              completedOrdersNumber: "56",
              canceledOrdersNumber: "5",
            },
          ],
        },
      ],
    };
  },
  methods: {},
};
</script>

<style>
/* Header */

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

/* Main */

.ant-layout-content {
  margin: 0;
  padding: 14px 10px;
  background: #e5e5e5;
  min-height: auto !important;
}

/* Content-left */

.main {
  padding: 14px 20px;
}

/* Form stats */

.form-item {
  margin: 0 !important;
}

.form-item:not(:last-child) {
  margin-right: 2px !important;
}

.form-item:last-child {
  margin-left: 12px !important;
}

.form-item-two label {
  margin-right: 6px;
}

.ant-form-item-control {
  line-height: 35px;
}

.ant-select-selection {
  height: 35px;
}

.ant-select-selection:hover {
  outline: none;
}

.ant-select-selection__rendered {
  line-height: 33px;
}

.ant-select-arrow {
  margin-top: -4px;
}

/* Compare stats */

.compare-stats {
  margin-bottom: 40px;
}

/* Card stats */

.card-stats {
  margin-bottom: 25px !important;
}

.card-stats-item {
  padding: 16px 16px 12px 16px;
  color: var(--white-color);
  display: flex;
  justify-content: space-between;
  border-radius: 15px;
}

.card-stats-item h3 {
  color: var(--white-color);
  font-size: 14px;
  line-height: 16px;
  font-weight: 700;
  margin-bottom: 4px;
  white-space: nowrap;
}

.card-stats-item .question-icon {
  font-size: 11px;
  line-height: 21px;
}

.card-stats-item .number-data {
  font-size: 20px;
  line-height: 23px;
  font-weight: 800;
  margin-bottom: 8px;
  white-space: nowrap;
}

.card-stats-item .percent-data {
  font-size: 14px;
  line-height: 21px;
  white-space: nowrap;
}

.card-stats-item .icon-right {
  font-size: 24px;
}

.bg-purple {
  background: #7957ff !important;
}

.card-stats-item.bg-purple .number-data {
  font-size: 25px !important;
  line-height: 21px;
}

.bg-pink {
  background: #f05ee1 !important;
}

.bg-orange {
  background: #f8902f !important;
}

.bg-white {
  color: var(--text2-color) !important;
  background: var(--white-color);
}

.card-stats-item.bg-white h3 {
  color: var(--text2-color);
}

.card-stats-item.bg-white .number-data {
  color: var(--text-color) !important;
}

.card-stats-item .icon-right i {
  padding: 10px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.12);
}

.card-stats-item.bg-white .icon-right i {
  padding: 10px;
  border-radius: 50%;
  background: rgb(74, 128, 255, 0.1);
}

.anticon-icon-none {
  display: none;
}

/* stats chart */

.stats-chart {
  background: var(--white-color);
  border-radius: 10px;
}

.stats-chart .stats-chart-title {
  font-size: 14px;
  line-height: 21px;
  color: var(--text2-color);
  margin-bottom: 7px;
}

.stats-chart .stats-chart-value {
  font-size: 17px;
  font-weight: 700;
  line-height: 20px;
  color: var(--text-color);
  margin-bottom: 3px;
}

.card-container {
  background: #fff;
  overflow: hidden;
  padding: 10px;
  border-radius: 10px;
}

.card-container > .ant-tabs-card > .ant-tabs-content {
  margin-top: -16px;
}

.card-container > .ant-tabs-card > .ant-tabs-content > .ant-tabs-tabpane {
  background: #fff;
  padding: 16px;
}

.card-container > .ant-tabs-card > .ant-tabs-bar {
  border-color: #fff;
}

.card-container > .ant-tabs-card > .ant-tabs-bar .ant-tabs-tab {
  border-color: transparent;
  background: transparent;
}

.card-container > .ant-tabs-card > .ant-tabs-bar .ant-tabs-tab-active {
  border-color: #fff;
  background: #fff;
}

.ant-tabs.ant-tabs-card .ant-tabs-card-bar .ant-tabs-nav-container,
.ant-tabs.ant-tabs-card .ant-tabs-card-bar .ant-tabs-tab {
  height: 100% !important;
}

.ant-tabs.ant-tabs-card .ant-tabs-card-bar .ant-tabs-tab {
  line-height: 100%;
  margin-right: 0 !important;
  padding: 11px 5px 11px 13px !important;
  background: var(--white-color) !important;
}

.ant-tabs.ant-tabs-card .ant-tabs-card-bar .ant-tabs-tab-active {
  background: #f5f6fa !important;
  border-radius: 10px;
  box-shadow: none !important;
}

.ant-tabs-nav-container-scrolling {
  padding: 0;
}

.ant-tabs-tab-prev,
.ant-tabs-tab-next {
  display: none !important;
}

/* Top List */

.top-product-staff {
  padding-top: 12px;
}

.product-staff-title {
  margin-bottom: 19px;
  margin-top: 37px;
}

.product-staff-title h2 {
  font-size: 20px;
  font-weight: 700;
  line-height: 23px;
  color: var(--text-color);
}

.top-product-staff .product-staff-title-item:last-child {
  text-align: right !important;
}

.top-product-staff .product-staff-title-item:last-child a {
  font-size: 14px;
  line-height: 21px;
  color: var(--blue-color);
}

.top-product-staff .product-staff-item {
  margin-bottom: 6px !important;
  padding: 11px 0;
  background: var(--white-color);
  border-radius: 5px;
}

.top-product-staff .product-staff-heading h3 {
  font-weight: 700;
  font-size: 14px;
  line-height: 16px;
  color: var(--text2-color);
}

.top-product-staff .product-staff-item .orders {
  text-align: center;
}

.top-product-staff .product-staff-name-wrap {
  display: flex;
}

.top-product-staff .products-img,
.top-product-staff .staffs-img {
  margin-right: 10px;
}

.top-product-staff .products-text p,
.top-product-staff .staffs-text p {
  white-space: nowrap !important;
}

/* Content right */

/* Say hello */

.content-right .sayHello {
  margin-bottom: 30px;
  position: relative;
}

.content-right .sayHello::before {
  content: "";
  position: absolute;
  height: 42px;
  border-left: 3px solid var(--blue-color);
}

.content-right .sayHello-title {
  font-size: 20px;
  line-height: 23px;
  font-weight: 700;
  margin-left: 12px;
}

.content-right .sayHello p {
  margin-left: 12px;
}

.content-right .sayHello p a {
  color: var(--blue-color);
}

/* Stats today */

.content-right .stats-info-item {
  padding: 20px 16px;
  border-radius: 10px;
  background: var(--white-color);
}

.content-right .stats-today h2 {
  font-size: 20px;
  font-weight: 700;
  line-height: 23px;
  margin-bottom: 6px;
  color: var(--text-color);
}

.content-right .card-blue {
  margin-bottom: 14px !important;
}

.content-right .stats-today-item .revenue-today-text {
  font-size: 14px;
  line-height: 33px;
}

.content-right .revenue-today-value {
  font-size: 28px;
  font-weight: 700;
  line-height: 33px;
}

.content-right .quantity-stats-today-item {
  display: flex;
  padding: 10px;
  border-radius: 10px;
  color: var(--white-color);
  background: var(--blue-color);
}

.content-right .quantity-stats-today-item i {
  margin: auto 0;
  margin-right: 10px;
  font-size: 18px;
  line-height: 21px;
  padding: 9px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.12);
}

.content-right .quantity-stats-today-item .orders {
  font-size: 14px;
  line-height: 21px;
}

.content-right .quantity-stats-today-item .orders-number {
  font-size: 20px;
  font-weight: 700;
  line-height: 24px;
}

.content-right .stats-today-item .quantity-today-text {
  font-size: 14px;
  line-height: 21px;
}

.content-right .stats-today-item .quantity-today-monney {
  font-size: 17px;
  line-height: 21px;
  font-weight: 700;
  text-align: right;
}

/* Warehouse info */

.content-right .warehouse-info-selection {
  margin: 12px 0;
}

@media screen and (min-width: 1200px) {
}

@media screen and (max-width: 1199px) {
  .sayHello {
    display: none;
  }
}

@media screen and (max-width: 991px) {
}

@media screen and (max-width: 767px) {
  .content-right .warehouse-info-selection {
    width: 100% !important;
  }
}

@media screen and (max-width: 575px) {
  .header-user-fullName,
  .header-region-name {
    display: none;
  }
  .header-region {
    margin-left: 10px;
  }
}
</style>
