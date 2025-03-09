<template>
  <div class="box">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulário para criação de um novo treino"
      >
        <!-- Nome do treino -->
        <input
          type="text"
          v-model="treinoNome"
          class="input"
          placeholder="Qual exercício você deseja iniciar?"
        />

        <!-- Categoria de treino -->
        <div class="select is-fullwidth">
          <select v-model="categoriaSelecionada">
            <option
              v-for="categoria in categorias"
              :key="categoria"
              :value="categoria"
            >
              {{ categoria }}
            </option>
          </select>
        </div>

        <!-- Treino selecionado -->
        <div class="select is-fullwidth mt-2">
          <select v-model="treinoEscolhido">
            <option
              v-for="treino in treinos[categoriaSelecionada]"
              :key="treino"
              :value="treino"
            >
              {{ treino }}
            </option>
          </select>
        </div>
        <!-- Cronômetro -->
        <CronometroAtividade
          :tempo="tempo"
          :cronometroAtivo="cronometroAtivo"
          @iniciar-cronometro="iniciarCronometro"
          @parar-cronometro="pararCronometro"
        />
      </div>
    </div>
  </div>
  <!-- Treinos Concluídos -->
  <TreinosConcluidos :treinoConcluido="treinoConcluido" />
</template>

<script>
import CronometroAtividade from "@/components/CronometroAtividade.vue";
import TreinosConcluidos from "@/components/TreinosConcluidos.vue";
import dadosTreino from "@/assets/dadosTreino.json";

export default {
  name: "FormularioTarefa",
  components: {
    CronometroAtividade,
    TreinosConcluidos,
  },
  data() {
    return {
      treinoNome: "",
      tempo: 0,
      cronometroAtivo: false,
      treinoConcluido: [],
      categorias: dadosTreino.categorias,
      categoriaSelecionada: "Musculação",
      treinos: dadosTreino.treinos,
      treinoEscolhido: "",
    };
  },
  methods: {
    iniciarCronometro() {
      this.cronometroAtivo = true;
      this.tempo = 0;
      this.contagemTempo();
    },
    contagemTempo() {
      if (this.cronometroAtivo) {
        setTimeout(() => {
          this.tempo++;
          this.contagemTempo();
        }, 1000);
      }
    },
    pararCronometro() {
      this.cronometroAtivo = false;
      this.salvarTreino();
    },
    salvarTreino() {
      this.treinoConcluido.push({
        nome: this.treinoNome,
        tempo: this.formatarTempo(),
        categoria: this.categoriaSelecionada,
        treino: this.treinoEscolhido,
        data: new Date().toLocaleString(),
      });
      this.treinoNome = "";
      this.tempo = 0;
    },
    formatarTempo() {
      let horas = Math.floor(this.tempo / 3600);
      let minutos = Math.floor((this.tempo % 3600) / 60);
      let segundos = this.tempo % 60;
      return `${this.pad(horas)}:${this.pad(minutos)}:${this.pad(segundos)}`;
    },
    pad(num) {
      return num < 10 ? `0${num}` : num;
    },
  },
};
</script>

<style scoped></style>
