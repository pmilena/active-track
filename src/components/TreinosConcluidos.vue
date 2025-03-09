<template>
  <div class="mt-4">
    <h4>Treinos Concluídos</h4>
    <ul>
      <li v-for="(treino, index) in treinoConcluido" :key="index">
        <strong>{{ treino.nome }}</strong> - {{ treino.categoria }} -
        {{ treino.treino }} <br />
        Tempo: {{ treino.tempo }} <br />
        Concluído em: {{ treino.data }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TreinosConcluidos",
  props: {
    treinoConcluido: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
