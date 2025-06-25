<template>
  <div class="background-color">
    <v-row>
      <v-col>
        <v-card elevation="10" style="max-width: 400px; margin: auto; margin-top: 20vh;">
          <div>
            <h1 class="text-center">Bem-vindo ao Trancity</h1>
            <p class="text-center">Interessado em nossos serviços?</p>
          </div>
          <v-img src="/Transporte-Urbano.jpg" cover>
            <v-form>
                <v-text-field variant="solo" label="nome" required class="mb-3" v-model="nome"></v-text-field>
                <v-text-field variant="solo" label="email" required class="mb-3" v-model="email"></v-text-field>
                <v-text-field variant="solo" label="whatsapp" required class="mb-3" v-model="whatsapp"></v-text-field>
                <div class="right-align">
                  <v-btn color="success" class="mt-2" @click="persistLead" style="margin-left: 38%; margin-bottom: 1vh;">Enviar</v-btn>
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
      nome: null,
      email: null,
      whatsapp: null
    }
  },

  methods: {
    async persistLead() {
      try {
        const response = await fetch('http://localhost:3333/leads/persist', { 
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            nome: this.nome,
            email: this.email,
            whatsapp: this.whatsapp,
          }),
        });
        const data = await response.json();

        if (!response.ok) {
          alert('Erro ao enviar, tente novamente mais tarde.');
          return;
        }
        return data;
      } catch (error) {
        return error;
      }
    }
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