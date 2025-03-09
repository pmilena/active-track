<template>
  <div class="column">
    <div class="is-flex is-align-items-center is-justify-content-space-between">
      <section>
        <strong>{{ formatarTempo() }}</strong>
      </section>
      <button
        class="button"
        @click="iniciarCronometro"
        :disabled="cronometroAtivo"
      >
        <span class="icon">
          <i class="fas fa-play"></i>
        </span>
        <span>Iniciar</span>
      </button>
      <button
        class="button"
        @click="pararCronometro"
        :disabled="!cronometroAtivo"
      >
        <span class="icon">
          <i class="fas fa-stop"></i>
        </span>
        <span>Parar</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CronometroAtividade",
  props: {
    tempo: {
      type: Number,
      default: 0,
    },
    cronometroAtivo: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    iniciarCronometro() {
      this.$emit("iniciar-cronometro");
    },
    pararCronometro() {
      this.$emit("parar-cronometro");
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
