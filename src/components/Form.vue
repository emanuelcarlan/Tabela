<template>
  <div class="formulario-produto">
    <InputText
      class="input-produto"
      type="text"
      v-model="nome"
      placeholder="Nome do produto"
    />
    <InputText
      class="input-produto"
      type="text"
      v-model="marca"
      placeholder="Marca do produto"
    />
    <InputText
      class="input-produto"
      type="text"
      v-model="codgo"
      placeholder="Codigo de barra"
    />

    <Button class="p-button-success" @click="enviar">Salvar</Button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";
import InputText from "primevue/inputtext";
import Button from "primevue/button";

export default defineComponent({
  components: { InputText, Button },
  name: "Form",
  props: ["produto"],
  data() {
    return {
      nome: "",
      marca: "",
      codgo: "",
    };
  },
  watch: {
    produto() {
      this.nome = this.produto.nome;
      this.marca = this.produto.marca;
      this.codgo = this.produto.codgo;
    },
  },
  methods: {
    enviar() {
      const form = {
        nome: this.nome,
        marca: this.marca,
        codgo: this.codgo,
      };

      if (this.produto.codgo) {
        this.$emit("editar", form);
      } else {
        this.$emit("adicionar", form);
      }

      this.limparFormulario();
    },
    limparFormulario() {
      this.nome = "";
      this.marca = "";
      this.codgo = "";
    },
  },
});
</script>

<style>
.formulario-produto {
  width: 480px;
  margin: 32px auto;
  box-shadow: rgba(0, 0, 0, 0.02) 0px 1px 3px 0px,
    rgba(27, 31, 35, 0.15) 0px 0px 0px 1px;
  padding: 32px 20px;
}

.formulario-produto .input-produto {
  width: 100%;
  margin-bottom: 16px;
  padding: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.formulario-produto .p-button {
  height: 48px;
  width: 160px;
  justify-content: center;
  font-size: 20px;
  font-weight: 600;
  margin-top: 16px;
  border-radius: 6px;
}
</style>
