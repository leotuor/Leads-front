<template>
  <div class="title text-center" style="margin-top: 15vh">
    <h1>Relatório de dias🧮</h1>
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
        <v-form @submit.prevent>
          <h2 class="text-center mt-5">
            Selecione os anos e meses
          </h2>
          <v-combobox
            multiple
            label="Anos"
            :rules="ruleValidate"
            :items="anos"
            v-model="anosSelecionados"
            class="mt-5"
          >
          </v-combobox>
          <v-combobox
            multiple
            label="Mêses (opcional)"
            :items="meses"
            v-model="mesesSelecionados"
          ></v-combobox>
          <div class="d-flex justify-center">
            <v-btn color="blue" type="submit" block @click="calcularDias()">
              Calcular
            </v-btn>
          </div>
        </v-form>
        <h3 :style="{ textAlign: 'center', marginTop: '4%' }" v-if="diasTotais">
          Dias totais: {{ diasTotais }}
        </h3>
        <v-carousel
          class="mx-auto" width="400" height="200"
          v-if="diaPorAnoLista && diaPorAnoLista.length > 0"
          show-arrows
        >
          <v-carousel-item
            v-for="(item, i) in this.diaPorAnoLista"
            :key="i"
            elevation="3"
          >
            <v-sheet
              class="fill-height"
            >
              <div class="d-flex fill-height justify-center align-center">
                <h2>
                  Ano: {{ item.ano }} - Dias: {{ item.total }}
                </h2>
              </div>
            </v-sheet>
          </v-carousel-item>
        </v-carousel>
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
      meses: [
        'Janeiro', 
        'Fevereiro', 
        'Março', 
        'Abril', 
        'Maio', 
        'Junho', 
        'Julho', 
        'Agosto', 
        'Setembro', 
        'Outubro', 
        'Novembro', 
        'Dezembro'
      ],
      anos: Array.from({ length: 2025 }, (notUsed, i) => i + 1).reverse(),
      mesesSelecionados: [],
      anosSelecionados: [],
      diaPorAnoLista: [],
      diasTotais: null,
      ruleValidate: [
        value => {
          if (value.length !== 0) return true

          return 'Selecione ao menos um ano.'
        },
      ],
    };
  },

  methods: {
    calcularDias() {
      if (this.anosSelecionados.length === 0) {
        alert("Selecione ao menos um ano!");
        return;
      }
      this.diasTotais = 0;
      let diasBissexto = 0;
      let anosTotais = 0;
      this.diaPorAnoLista = this.anosSelecionados.map(item => ({
        ano: item,
        total: 0
      }));

      this.anosSelecionados.forEach(ano => {
        if (ano % 4 === 0 && (this.mesesSelecionados.includes('Fevereiro') || this.mesesSelecionados.length === 0)) {
          diasBissexto++;
          anosTotais++;
          
        } else {
          anosTotais++;
        }
      });
      if (this.mesesSelecionados.length !== 0) {
        this.mesesSelecionados.forEach(mes => {
        if (mes === 'Fevereiro') {
          this.diasTotais += 28;
        } else if (mes === 'Abril' || mes === 'Junho' || mes === 'Setembro' || mes === 'Novembro') {
          this.diasTotais += 29;
        } else {
          this.diasTotais += 30;
        }
      });

      this.diaPorAnoLista.forEach(item => {
        if (item.ano % 4 === 0 && this.mesesSelecionados.includes('Fevereiro')) {
          item.total = this.diasTotais + 1;
        } else {
          item.total = this.diasTotais;
        }
      });

      this.diasTotais = this.diasTotais * anosTotais + diasBissexto;
      } else {
        this.diasTotais = anosTotais * 365 + diasBissexto;
        this.diaPorAnoLista = [];
      }
    },
  },
};
</script>