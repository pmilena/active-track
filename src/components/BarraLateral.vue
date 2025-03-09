<script>
export default {
  name: "BarraLateral",
};
</script>

<template>
  <header class="header">
    <img
      src="../assets/logo.png"
      alt="logo da Active Track que apresenta a silhueta de um homem correndo nas cores laranja, verde e vermelho e fundo com gradiente cinza."
      class="logo"
    />
  </header>
  <nav class="sidebar">
    <ul>
      <!-- Outros itens do menu -->
      <li>
        <router-link to="/historico-treinos">Histórico de Treinos</router-link>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.header {
  background: #29333dff;
  width: 100%;
  height: 100vh;
}

.logo {
  width: 420px;
  padding-top: 2rem;
}
@media only screen and (max-width: 768ps) {
  .header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
