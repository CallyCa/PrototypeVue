<template>
  <form>
      <div class="usuario" v-if="mostrarDadosLogin">
        <label for="nome">Nome</label>
        <input type="text" name="nome" v-model="nome" id="nome">
        <label for="email">Email</label>
        <input type="email" name="email" v-model="email" id="email">
        <label for="senha">Senha</label>
        <input type="password" name="senha" v-model="senha" id="senha">
      </div>

      <label for="cep">Cep</label>
      <input type="text" name="cep" v-model="cep" id="cep" @keyup="preencherCep">
      <label for="rua">Rua</label>
      <input type="text" name="rua" v-model="rua" id="rua">
      <label for="numero">Numero</label>
      <input type="text" name="numero" v-model="numero" id="numero">
      <label for="bairro">Bairro</label>
      <input type="text" name="bairro" v-model="bairro" id="bairro">
      <label for="cidade">Cidade</label>
      <input type="text" name="cidade" v-model="cidade" id="cidade">
      <label for="estado">Estado</label>
      <input type="text" name="estado" v-model="estado" id="estado">
      <div class="button">
          <slot></slot>

      </div>
  </form>
</template>

<script>

import { mapFields} from "@/helpers.js";
import { getCep } from "@/services.js";

export default {
    computed: {
        ...mapFields({
            fields: 
            [
                "nome", 
                "email", 
                "senha", 
                "rua", 
                "cep", 
                "numero", 
                "bairro", 
                "cidade", 
                "estado"
            ],
            base: "usuario",
            mutation: "UPDATE_USUARIO"
        }),
        mostrarDadosLogin() {
            return (!this.$store.state.login || (this.$route.name === 'usuario-editar'))
        }
    },
    methods: {
        preencherCep() {
            const cep = this.cep.replace(/\D/g, "");
            if(cep.length === 8) {
                getCep(cep).then(response => {
                    this.rua = response.data.longradouro;
                    this.bairro = response.data.bairro;
                    this.estado = response.data.uf;
                    this.cidade = response.data.localidade;
                })
            }
        }
    }

}
</script>

<style scoped>
form,
.usuario{
    display: grid;
    grid-template-columns: 80px 1fr;
    align-items: center;
}

.usuario {
    grid-column: 1 / 3;
}

.button {
    grid-column: 2;
    margin-top: 10px;
}
</style>