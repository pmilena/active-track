<template>
  <div class="lista-treinos-realizados">
    <h2>Histórico de Treinos</h2>
    <ul>
      <li v-for="(treino, index) in treinosRealizados" :key="index">
        <strong>{{ treino.data }}</strong> - {{ treino.categoria }}:
        {{ treino.treino }} ({{ treino.tempo }})
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    treinosRealizados: Array,
  },
};
</script>

<style scoped>
.treinos-realizados {
  margin-top: 20px;
  padding: 15px;
  background: #f6f6f6;
  border-radius: 5px;
}
</style>
