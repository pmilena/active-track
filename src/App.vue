<template>
  <main class="columns is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral />
    </div>
    <div class="column is-two-quarter">
      <FormularioTarefa />
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioTarefa from "./components/FormularioTarefa.vue";

export default defineComponent({
  name: "App",
  components: { BarraLateral, FormularioTarefa },
});
</script>

<style></style>
