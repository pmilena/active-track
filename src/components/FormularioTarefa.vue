<template>
  <div class="box">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulário para criação de um novo treino"
      >
        <!-- Categoria de treino -->
        <CampoInputSelect
          :isInput="false"
          :selectModel="categoriaSelecionada"
          :options="categorias"
          @update:modelValue="categoriaSelecionada = $event"
        />

        <!-- Treino selecionado -->
        <CampoInputSelect
          :isInput="false"
          :selectModel="treinoEscolhido"
          :options="treinos[categoriaSelecionada]"
          @update:modelValue="treinoEscolhido = $event"
        />

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
import CampoInputSelect from "@/components/CampoInputSelect.vue";
import CronometroAtividade from "@/components/CronometroAtividade.vue";
import TreinosConcluidos from "@/components/TreinosConcluidos.vue";
import dadosTreino from "@/assets/dadosTreino.json";

export default {
  name: "FormularioTarefa",
  components: {
    CampoInputSelect,
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
