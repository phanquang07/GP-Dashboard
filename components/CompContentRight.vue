<template>
  <div>
    <!-- Content right -->
    <!-- Say Hello -->
    <section class="sayHello">
      <h2 class="sayHello-title">Xin chào! {{ user.name }}</h2>
      <p>
        Gói đang sử dụng:
        <NuxtLink to="/">{{ user.optionLink }}</NuxtLink>
      </p>
    </section>
    <!-- Stats info -->
    <div class="stats-info">
      <a-row :gutter="[14, 14]">
        <a-col
          :xl="24"
          :lg="12"
          :md="24"
          v-for="(statsInfoItem, idx) in statsInfoList"
          :key="idx"
        >
          <section class="stats-info-item stats-today">
            <h2>{{ statsInfoItem.title }}</h2>
            <a-row :gutter="[0, 12]" class="stats-today-item">
              <a-col :xs="7" class="revenue-today-text">{{ statsInfoItem.revenueText }}</a-col>
              <a-col
                :xs="17"
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
                :sm="12"
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
              <a-col :xs="12" class="quantity-today-text">{{ statsInfoItem.canceledText }}</a-col>
              <a-col
                :xs="12"
                class="quantity-today-monney"
              >{{ statsInfoItem.canceledValue }}</a-col>
            </a-row>
            <a-row :gutter="[12, 12]" class="stats-today-item">
              <a-col :xs="12" class="quantity-today-text">{{ statsInfoItem.closedText }}</a-col>
              <a-col
                :xs="12"
                class="quantity-today-monney"
              >{{ statsInfoItem.closedValue }}</a-col>
            </a-row>
            <a-row :gutter="[12, 12]" class="stats-today-item">
              <a-col
                :xs="12"
                class="quantity-today-text"
              >{{ statsInfoItem.succeededText }}</a-col>
              <a-col
                :xs="12"
                class="quantity-today-monney"
              >{{ statsInfoItem.succeededValue }}</a-col>
            </a-row>
          </section>
        </a-col>
      </a-row>
    </div>
  </div>
</template>

<script>
export default {
  // props: ['userName'],
  data() {
    return {
      user: {
        name: "Sun Cometics",
        optionLink: 'Silver',
      },
      // Stats info list
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
    };
  },
};
</script>

<style>
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
</style>