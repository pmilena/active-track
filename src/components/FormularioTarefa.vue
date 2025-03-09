<template>
  <div class="box">
    <div class="columns">
      <div
        class="column is-8 form-container"
        role="form"
        aria-label="Formulário para criação de um novo treino"
      >
        <!-- Categoria de treino -->
        <CampoInputSelect
          class="campo-input-select"
          :isInput="false"
          :selectModel="categoriaSelecionada"
          :options="categorias"
          @update:modelValue="categoriaSelecionada = $event"
        />

        <!-- Treino selecionado -->
        <CampoInputSelect
          class="campo-input-select"
          :isInput="false"
          :selectModel="treinoEscolhido"
          :options="treinos[categoriaSelecionada]"
          @update:modelValue="treinoEscolhido = $event"
        />

        <!-- Cronômetro -->
        <CronometroAtividade
          class="cronometro"
          :tempo="tempo"
          :cronometroAtivo="cronometroAtivo"
          @iniciar-cronometro="iniciarCronometro"
          @parar-cronometro="pararCronometro"
        />

        <!-- Botão de ação -->
        <button @click="salvarTreino">Salvar Treino</button>
      </div>
    </div>
  </div>

  <!-- Treinos Concluídos -->
  <TreinosConcluidos
    class="treino-concluido"
    :treinoConcluido="treinoConcluido"
  />

  <lista-treinos-realizados :treinosRealizados="treinosRealizados" />
</template>

<script>
import CampoInputSelect from "@/components/CampoInputSelect.vue";
import CronometroAtividade from "@/components/CronometroAtividade.vue";
import TreinosConcluidos from "@/components/TreinosConcluidos.vue";
import dadosTreino from "@/assets/dadosTreino.json";
import ListaTreinosRealizados from "@/components/ListaTreinosRealizados.vue";

export default {
  name: "FormularioTarefa",
  components: {
    CampoInputSelect,
    CronometroAtividade,
    TreinosConcluidos,
    ListaTreinosRealizados,
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
      treinosRealizados: [],
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
      this.treinoConcluido.push({
        nome: this.treinoNome,
        tempo: this.formatarTempo(),
        categoria: this.categoriaSelecionada,
        treino: this.treinoEscolhido,
        data: new Date().toLocaleString(),
      });
    },
    salvarTreino() {
      this.treinosRealizados.push({
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

<style scoped>
.box {
  background-color: #f6f6f6;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin: 2rem;
}

.columns {
  display: flex;
  justify-content: center;
  align-items: center;
}

.column {
  background: #2a2a2a; /* Cor secundária para força e estabilidade */
  padding: 15px;
  border-radius: 8px;
  color: #f6f6f6;
  width: 100%;
}

/* Botões de ação */
button {
  background-color: #ff5733; /* Cor primária para energia e motivação */
  color: #fff;
  border: none;
  padding: 12px 24px;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s ease;
  font-weight: bold;
  font-size: 1em;
  width: 100%;
}

button:hover {
  background-color: #e04e2b;
}

/* Inputs e selects estilizados */
select,
input {
  width: 100%;
  padding: 12px;
  margin: 10px 0;
  border: 2px solid #ffc300; /* Cor de destaque para ação */
  border-radius: 5px;
  background: #fff;
  color: #2a2a2a;
  font-weight: bold;
  outline: none;
  font-size: 1em;
}

/* Ajuste para Vue e componentes filhos */
:deep(.campo-input-select),
:deep(.cronometro-atividade),
:deep(.treinos-concluidos) {
  width: 100%;
  margin-bottom: 15px;
}

/* Estilização específica para o cronômetro */
.cronometro {
  font-size: 1.8em;
  font-weight: bold;
  color: #28a745; /* Cor de suporte para equilíbrio e saúde */
  text-align: center;
  margin-top: 15px;
  padding: 10px;
  border-radius: 8px;
  background-color: #1c1e1d;
}

/* Treinos concluídos */
.treino-concluido {
  /* background-color: #28a745; */
  color: #fff;
  padding: 12px;
  margin-top: 10px;
  border-radius: 5px;
  text-align: center;
  font-weight: bold;
  font-size: 1.1em;
}
</style>
