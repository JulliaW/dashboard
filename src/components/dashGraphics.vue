<template>
  <div v-if="load" id="loading">
    <img id="loading-image" src="@/assets/processando.gif" />
  </div>

  <div class="container" v-if="!load">

    <div class="graficos">
      <div class="graficos-cards">
        <div class="card spark">
          <div class="card-body">
            <div class="card-info">
              <span>{{ dadoscard1.titulo }}</span>
              <span>{{ dadoscard1.qtd }}</span>
            </div>
            <div class="sparkline">
              <spark :p_data="dadoscard1" />
            </div>
          </div>
        </div>

        <div class="card spark">
          <div class="card-body">
            <div class="card-info">
              <span>{{ dadoscard2.titulo }}</span>
              <span>{{ dadoscard2.qtd }}</span>
            </div>
            <div class="sparkline">
              <spark :p_data="dadoscard2" />
            </div>
          </div>
        </div>
      </div>

      <div class="graficos-cards">
        <div class="card spark">
          <div class="card-body">
            <div class="card-info">
              <span>{{ dadoscard3.titulo }}</span>
              <span>{{ dadoscard3.qtd }}</span>
            </div>
            <div class="sparkline">
              <spark :p_data="dadoscard3" />
            </div>
          </div>
        </div>

        <div class="card spark">
          <div class="card-body">
            <div class="card-info">
              <span>{{ dadoscard4.titulo }}</span>
              <span>{{ dadoscard4.uf }}</span>
            </div>
          </div>
        </div>
      </div>

      <bar class="card grafico" :p_data="lucroEmpresa" />
      <line-a class="card grafico" :p_data="lucroDia" />
    </div>
  </div>
</template>

<script>
import lineA from "./graphics/line-graphic.vue";
import bar from "./graphics/bar-graphic.vue";
import spark from "./graphics/spark-graphic.vue";

export default {
  components: {
    spark,
    bar,
    lineA,
  },
  data() {
    return {
      url: "",
      dataInicial: "",
      dataFinal: "",
      load: true,
      showTooltip: false,
      dadoscard1: {
        data: [],
        titulo: "Total de Faturamento",
        qtd: 0,
      },
      dadoscard2: {
        data: [],
        titulo: "Total de Lucro (mês)",
        qtd: 0,
      },
      dadoscard3: {
        data: [],
        titulo: "Quantidade de Empresas",
        qtd: 0,
      },
      dadoscard4: {
        titulo: "UF com maior faturamento",
        uf: "",
      },
      lucroEmpresa: {
        titulo: "Lucro por Empresa",
        qtd: [],
        descricao: [],
      },
      lucroDia: {
        qtd: [],
        dias: [],
      },
    };
  },
  methods: {
    consumirAPI() {
      this.load = true;

      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch("http://127.0.0.1:5000/GetData", requestOptions)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);

          this.dadoscard1.qtd = data.Faturamento;
          this.dadoscard1.data = data.LinhasFaturamento.faturamento;

          this.dadoscard2.qtd = data.Lucro;
          this.dadoscard2.data = data.GraficoLinhas.lucro;

          this.dadoscard3.qtd = data.QtdeEmpresas;
          this.dadoscard4.uf = data.Uf;

          this.lucroDia.qtd = data.GraficoLinhas.lucro;
          this.lucroDia.dias = data.GraficoLinhas.dia;

          this.lucroEmpresa.qtd = data.GraficoBarras.lucro;
          this.lucroEmpresa.descricao = data.GraficoBarras.empresa;

          this.load = false;
        });
    },
  },
  mounted() {
    if (this.load) {
      this.consumirAPI();
    }
  },
};
</script>

<style></style>
