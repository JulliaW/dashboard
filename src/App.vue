<template>
  <dash />
</template>

<script>
import dash from "./components/dashGraphics.vue";

export default {
  name: "App",
  components: {
    dash,
  },
  data() {
    return {};
  },
};
</script>

<style>
:root {
  --cor1: #000000;
  --cor2: #1a1f23;
  --cor3: #262b2f;
  --cor4: #f1f1f1;
  --cor5: #f2f2f2;
  --cor6: #ffffff;

  --cor-p1: #2e354c;
  --cor-p2: #FEBD11;
  --sombra: rgba(0, 0, 0, 0.2);
}

@media (prefers-color-scheme: dark) {
  :root {
    --cor1: #ffffff;
    --cor2: #f1f1f1;
    --cor3: #999999;
    --cor4: #262b2f;
    --cor5: #1a1f23;
    --cor6: #1b2024;

    --cor-p1: #5b6997;
    --sombra: rgba(0, 0, 0, 0.2);
  }
} 

body {
  background-color: var(--cor6);
  font-family: Montserrat, Arial, sans-serif;
  /* font-family: 'Roboto', sans-serif; */
}

.card {
  border: 2px solid var(--cor5);
  border-radius: 5px;
  background-color: var(--cor4);
  box-shadow: 0 2px 4px 0 var(--sombra);
  transition: 0.3s;
}

.card:hover {
  box-shadow: 0 4px 8px 0 var(--sombra);
}

.card-body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.card-info {
  font-size: 30px;
  font-weight: 500;
}

.card-info span {
  display: inline-block;
  color: var(--cor1);
}

.card-info :nth-child(1) {
  color: var(--cor3);
  font-size: 14px;
}

.container {
  padding-top: 10px;
}
</style>
