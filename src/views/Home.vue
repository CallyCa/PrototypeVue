<template>
  <section>
    <h1>Comprar Produtos</h1>
    <ProdutosBuscar/>
    <ProdutosLista/>
  </section>
</template>

<script>
import ProdutosBuscar from "@/components/ProdutosBuscar.vue";
import ProdutosLista from "@/components/ProdutosLista.vue";

export default {
  name: "home",
  components: {
    ProdutosBuscar,
    ProdutosLista
  }

}
</script>

<style scoped>
h1 {
  font-size: 2rem;
  color: rgb(255, 146, 107);
  margin-top: 40px;
  text-align: center;
}

</style>