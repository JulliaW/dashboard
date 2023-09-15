<template>
  <div id="chart">
    <apexchart
      v-if="load"
      type="bar"
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
      data: this.p_data.qtd,
      categorias: this.p_data.descricao,
      load: false,

      series: [
        {
          data: [],
        },
      ],
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
          background: getComputedStyle(
            document.documentElement
          ).getPropertyValue("--cor4"),
        },
        title: {
          text: "",
          align: "center",
          style: {
            color: getComputedStyle(document.documentElement).getPropertyValue(
              "--cor1"
            ),
            fontSize: "20px",
          },
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: "50%",
            endingShape: "rounded",
          },
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          show: true,
          width: 2,
          colors: ["transparent"],
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
        fill: {
          opacity: 1,
          colors: [
            getComputedStyle(document.documentElement).getPropertyValue(
              "--cor-p1"
            ),
          ],
        },
      },
    };
  },
  mounted() {
    this.series[0].data = this.data;
    this.chartOptions.xaxis.categories = this.categorias;

    this.chartOptions.title.text = this.p_data.titulo;

    this.load = true;
  },

  watch: {
    p_data: {
      immediate: true,
      handler() {
        this.series[0].data = this.data;
        this.chartOptions.xaxis.categories = this.categorias;
        this.chartOptions.title.text = this.p_data.titulo;

        this.load = true;
      },
    },
  },
};
</script>

<style></style>
