<template>
  <div class="container">

    <h1>Novo usuário</h1>

    <form @submit.prevent="enviarFormulario">
      <div class="form-group">
        <label for="name">Nome</label>
        <input type="text" class="form-control" v-model="usuario.nome">
      </div>
  
      <div class="form-group">
        <label for="name">E-mail</label>
        <input type="email" class="form-control" v-model="usuario.email">
      </div>

      <div class="form-group">
        <label for="name">Senha</label>
        <input type="password" class="form-control" v-model="usuario.senha">
      </div>

      <button class="btn btn-primary" type="submit">
        Cadastrar
      </button>
    </form>

  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: {
        nome: '',
        email: '',
        senha: ''
      }
    }
  },
  methods: {
    enviarFormulario() {
      this.$http.post('auth/register', this.usuario)
        .then(resposta => {
          console.log(resposta)
          this.$router.push({ name: 'login' })
        })
        .catch(erro => console.log(erro))
    }
  }
}
</script>