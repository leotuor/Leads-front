<template>
  <div class="background-color">
    <v-row>
      <v-col>
        <v-card style="max-width: 500px; margin: auto; margin-bottom: 30vh; margin-top: 2vh;">
          <h1 style="margin-left: 38%;">Trancity</h1>
        </v-card>
        <v-card elevation="10" style="max-width: 400px; margin: auto;">
          <div>
            <h1 class="text-center">Bem-vindo ao Transporte Urbano</h1>
            <p class="text-center">Acesse o sistema para gerenciar suas rotas e veículos.</p>
          </div>
          <v-img src="/Transporte-Urbano.jpg" cover>
            <v-form>
                <v-text-field variant="solo" label="email" required class="mb-3" v-model="email"></v-text-field>
                <v-text-field variant="solo" label="Senha" type="password" required class="mb-3" v-model="password"></v-text-field>
                <div class="right-align">
                  <v-btn color="success" class="mt-2" @click="login" style="margin-left: 38%;">Enviar</v-btn>
                </div>
              </v-form>
          </v-img>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data: () => {
    return {
      
    }
  },

  methods: {
    
  },
};
</script>
<style scoped>
.background-color {
  min-height: 100vh;
  background: linear-gradient(0deg, #47a1f5 0%, #bde0fa 100%);
  display: flex;
  justify-content: center;
}

</style>