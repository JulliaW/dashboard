<template>
  <div id="chart">
    <apexchart
      v-if="load"
      type="line"
      height="350"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
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
      load: false,

      series: [
        {
          name: "Lucro",
          data: [],
          color: getComputedStyle(document.documentElement).getPropertyValue(
            "--cor-p1"
          ),
        },
      ],
      chartOptions: {
        chart: {
          height: 350,
          type: "line",
          zoom: {
            enabled: false,
          },
          background: getComputedStyle(
            document.documentElement
          ).getPropertyValue("--cor4"),
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          width: [5, 7],
          curve: "straight",
          dashArray: [0, 8],
        },
        title: {
          text: "Lucro por dia",
          align: "center",
          style: {
            color: getComputedStyle(document.documentElement).getPropertyValue(
              "--cor1"
            ),
            fontSize: "20px",
          },
        },
        legend: {
          tooltipHoverFormatter: function (val, opts) {
            return (
              val +
              " - " +
              opts.w.globals.series[opts.seriesIndex][opts.dataPointIndex] +
              ""
            );
          },
          labels: {
            colors: getComputedStyle(document.documentElement).getPropertyValue(
              "--cor1"
            ),
          },
        },
        markers: {
          size: 0,
          hover: {
            sizeOffset: 6,
          },
        },
        xaxis: {
          categories: [],
          labels: {
            style: {
              colors: getComputedStyle(
                document.documentElement
              ).getPropertyValue("--cor1"),
              fontSize: "16px",
            },
          },
        },
        yaxis: {
          labels: {
            style: {
              colors: getComputedStyle(
                document.documentElement
              ).getPropertyValue("--cor1"),
              fontSize: "16px",
            },
          },
        },
        tooltip: {
          y: [],
        },
      },
    };
  },
  mounted() {
    this.series[0].data = this.p_data.qtd;
    this.chartOptions.xaxis.categories = this.p_data.dias;

    this.load = true;
  },

  watch: {
    p_data: {
      immediate: true,
      handler() {
        this.series[0].data = this.p_data.qtd;
        this.chartOptions.xaxis.categories = this.p_data.dias;

        this.load = true;
      },
    },
  },
};
</script>

<style></style>
