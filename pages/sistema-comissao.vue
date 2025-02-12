<template>
  <div class="title text-center" style="margin-top: 15vh">
    <h1>Sistema de Comissão</h1>
  </div>
  <v-card
    class="mx-auto"
    style="margin-top: 5vh;"
    width="800"
    height="600"
    rounded="lg"
    elevation="3"
  >
    <v-row>
      <v-spacer>
      </v-spacer>
      <v-col cols="10">
        <h2 class="text-center mt-1">Configure as taxas de comissão</h2>
        <v-form @submit.prevent>
          <v-row class="flex justify-center mt-1">
            <v-col cols="8">
              <v-autocomplete
                label="Vendedor"
                :items="vendedores"
                v-model="vendedorSelecionado"
                item-title="nome"
                item-value="id"
                :rules="rule"
              ></v-autocomplete>
            </v-col>
          </v-row>
          <v-row class="flex justify-center">
            <v-col cols="8">
              <v-text-field
                class="mt-n6"
                label="Vendas efetuadas"
                outlined
                prefix="R$"
                :rules="rule"
                v-model="vendasEfetuadas"
              ></v-text-field>
              <v-text-field
                label="Taxa de comissão"
                outlined
                prefix="%"
                v-model="taxaComissaoDisplay"
                readonly
              ></v-text-field><v-text-field
                label="Valor da comissão"
                outlined
                prefix="R$"
                v-model="valorComissaoDisplay"
                readonly
              ></v-text-field>
              <v-btn color="blue" block type="submit" @click="salvarComissao">
                Salvar
              </v-btn>
              <h2 class="text-center mt-16">Comissão salva com sucesso!</h2>
            </v-col>
          </v-row>
        </v-form>
        </v-col>
      <v-spacer>
      </v-spacer>
    </v-row>
  </v-card>
</template>
<script>
export default {
  data: () => {
    return {
      vendedores: [
        {
          id: 1,
          nome: "Jonas",
          totalVendas: null,
          taxaComissao: null,
          valorComissao: null,
        },
        {
          id: 2,
          nome: "Maria",
          totalVendas: null,
          taxaComissao: null,
          valorComissao: null,
        },
        {
          id: 3,
          nome: "Eduardo",
          totalVendas: null,
          taxaComissao: null,
          valorComissao: null,
        },
        {
          id: 4,
          nome: "Pedro",
          totalVendas: null,
          taxaComissao: null,
          valorComissao: null,
        },
        {
          id: 5,
          nome: "Juliana",
          totalVendas: null,
          taxaComissao: null,
          valorComissao: null,
        },
      ],
      vendedorSelecionado: null,
      vendasEfetuadas: null,
      taxaComissaoDisplay: null,
      valorComissaoDisplay: null,
      rule: [
        value => {
          if (value !== (0 || null)) return true

          return 'Necessario inserir um Valor.'
        },
      ],
    };
  },

  mounted() {
    const savedData = localStorage.getItem("vendedores");
    if (savedData) {
      this.vendedores = JSON.parse(savedData);
    }
  },

  watch: {
    vendasEfetuadas() {
      this.atualizarComissao(this.vendasEfetuadas);
    },
    vendedorSelecionado(){
      const vendedorIndex = this.vendedores.findIndex(v => v.id === this.vendedorSelecionado);
      this.vendasEfetuadas = this.vendedores[vendedorIndex].totalVendas;
      this.taxaComissaoDisplay = this.vendedores[vendedorIndex].taxaComissao;
      this.valorComissaoDisplay = this.vendedores[vendedorIndex].valorComissao;
    }
  },

  methods: {
    atualizarComissao(vendas) {
      if (vendas > 0.01 && vendas < 1000.00) {
        this.taxaComissaoDisplay = 5;
        this.valorComissaoDisplay = (vendas * 0.05).toFixed(2);
      } else if (vendas > 1000.01 && vendas < 10000.00) {
        this.taxaComissaoDisplay = 10;
        this.valorComissaoDisplay = (vendas * 0.10).toFixed(2);
      } else if (vendas > 10000.01 && vendas < 100000.00) {
        this.taxaComissaoDisplay = 20;
        this.valorComissaoDisplay = (vendas * 0.2).toFixed(2);
      } else if (vendas > 100000.01 && vendas < 1000000.00) {
        this.taxaComissaoDisplay = 30;
        this.valorComissaoDisplay = (vendas * 0.3).toFixed(2);
      }
    },
    salvarComissao() {
      if (this.vendedorSelecionado == null || this.vendasEfetuadas == null) {
        return;
      }
      const vendedorIndex = this.vendedores.findIndex(v => v.id === this.vendedorSelecionado);

      if (vendedorIndex !== -1) {
        Object.assign(this.vendedores[vendedorIndex], {
          totalVendas: this.vendasEfetuadas,
          taxaComissao: this.taxaComissaoDisplay,
          valorComissao: this.valorComissaoDisplay
        });
      }
      localStorage.setItem("vendedores", JSON.stringify(this.vendedores));
      alert("Dados salvos com sucesso!");
    },
  },
};
</script>