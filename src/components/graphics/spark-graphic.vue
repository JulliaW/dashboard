<template>
  <apexchart
    v-if="load"
    type="line"
    :options="options"
    :series="series"
  ></apexchart>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";
export default {
  props: {
    p_data: Object,
  },
  components: {
    apexchart: VueApexCharts,
  },
  data() {
    return {
      data: this.p_data.data,

      load: false,
      series: [
        {
          data: [],
        },
      ],
      options: {
        chart: {
          toolbar: {
            show: false,
          },
          sparkline: {
            enabled: true,
          },
        },
        stroke: {
          curve: "smooth",
          width: 2,
        },
        colors: [
          getComputedStyle(document.documentElement).getPropertyValue("--cor1"),
        ],
        tooltip: {
          enabled: false,
        },
        grid: {
          show: false,
        },
        xaxis: {
          labels: {
            show: false,
          },
          tooltip: {
            enabled: false,
          },
          axisTicks: {
            show: false,
          },
          crosshairs: {
            show: false,
          },
        },
        yaxis: {
          labels: {
            show: false,
          },
        },
      },
    };
  },
  mounted() {
    if (this.p_data) {
      this.series[0].data = this.p_data.data;
      this.load = true;
    }
  },

  watch: {
    p_data: {
      immediate: true,
      handler() {
        this.series[0].data = this.p_data.data;
        this.load = true;
      },
    },
  },
};
</script>
