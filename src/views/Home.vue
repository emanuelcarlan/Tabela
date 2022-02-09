<template>
  <div class="home">
    <DataTable :value="produtos" stripedRows responsiveLayout="scroll">
      <Column field="nome" header="Nome do Produto"></Column>
      <Column field="marca" header="Marca"></Column>
      <Column field="codgo" header="Codgo de  barras"></Column>
      <Column header="opções">
        <template #body="slotProps">
          <Button
            class="p-button-warning"
            @click="editarProduto(slotProps.data)"
          >
            Editar
          </Button>
          <Button
            class="p-button-danger"
            @click="deletarProduto(slotProps.data)"
            >Deletar</Button
          >
        </template>
      </Column>
    </DataTable>
    <Form
      :produto="produto"
      @editar="editarProdutoNaTabela"
      @adicionar="adicionaProdutoNaTabela"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DataTable from "primevue/datatable";
import Column from "primevue/column";
import Form from "@/components/Form.vue";
import Button from "primevue/button";

export default defineComponent({
  name: "Home",
  components: {
    DataTable,
    Column,
    Form,
    Button,
  },
  data() {
    return {
      produto: {},
      produtos: [
        { nome: "Lixa", marca: "Bela", codgo: 30 },
        { nome: "Acetona", marca: "Nova", codgo: 25 },
        { nome: "algodão", marca: "Forte", codgo: 15 },
      ],
    };
  },
  methods: {
    adicionaProdutoNaTabela(form: any) {
      this.produtos.push(form);
    },
    editarProdutoNaTabela(form: any) {
      this.deletarProduto(this.produto);
      this.adicionaProdutoNaTabela(form);
      this.produto = {};
    },
    editarProduto(produto: any) {
      this.produto = produto;
    },
    deletarProduto(produto: any) {
      this.produtos = this.produtos.filter(
        (item) => item.codgo !== produto.codgo
      );
    },
  },
});
</script>
<style scoped></style>
