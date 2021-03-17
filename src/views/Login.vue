<template>
  <div class="container">

    <h1>Login</h1>

    <form @submit.prevent="efetuarLogin">
      <div class="form-group">
        <label for="name">E-mail</label>
        <input type="email" class="form-control" v-model="usuario.email">
      </div>

      <div class="form-group">
        <label for="name">Senha</label>
        <input type="password" class="form-control" v-model="usuario.senha">
      </div>

      <p class="alert alert-danger" v-if="mensagemErro">
        {{ mensagemErro }}
      </p>

      <button class="btn btn-primary" type="submit">
        Entrar
      </button>

      <router-link :to="{ name: 'novo.usuario' }">
        Não possui um cadastro? Cadastre-se aqui!
      </router-link>
    </form>

  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: {
        email: '',
        senha: '',
      },
      mensagemErro: ''
    }
  },
  methods: {
    efetuarLogin() {
      this.$store.dispatch('efetuarLogin', this.usuario)
        .then(() => {
          this.$router.push({ name: 'gerentes' })
          this.mensagemErro = ''
        })
        .catch( erro => {
          if(erro.request.status === 401) {
            this.mensagemErro = 'Login ou senha inválido(s)'
          }
        })
    }
  }
}
</script>