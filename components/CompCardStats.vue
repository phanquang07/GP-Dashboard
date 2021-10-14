<template>
  <!-- Card stats -->
  <div>
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
              <a-progress v-if="statsItem.progress === 0" type="circle" :percent="18" :width="78" />
            </div>
          </div>
        </a-col>
      </a-row>
    </section>
  </div>
</template>

<script>
export default {
  name: "CardStats",
  data() {
    return {
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
    };
  },
  methods: {}
};
</script>

<style>
</style>