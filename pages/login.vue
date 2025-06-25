<template>
  <div class="login-background">
    <v-container>
      <v-row justify="center" align="center" class="fill-height">
        <v-col cols="12" sm="8" md="6" lg="4">
          <v-card class="pa-4 mx-auto" max-width="350px">
            <v-card-title class="text-h5 text-center">Login</v-card-title>
            <v-card-text>
              <v-form>
                <v-text-field label="email" required class="mb-3" v-model="email"></v-text-field>
                <v-text-field label="Senha" type="password" required class="mb-3" v-model="password"></v-text-field>
                <div class="right-align">
                  <h3>Esqueceu sua senha?</h3>
                  <v-btn color="primary" class="mt-2" @click="login">Login</v-btn>
                </div>
              </v-form>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      email: '',
      password: '',
    }
  },

  methods: {
    async login() {
      try {
        const response = await fetch('http://localhost:3333/usuario/login', { 
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            login: this.email,
            password: this.password,
          }),
        });
        const data = await response.json();

        if (!response.ok) {
          alert('Erro ao logar, tente novamente mais tarde.');
          return;
        }
        console.log(data.token);
      } catch (error) {
        
      }
      
    }
  },
};
</script>
<style scoped>
.login-background {
  min-height: 100vh;
  background: linear-gradient(135deg, #47a1f5 0%, #bde0fa 100%);
}
.fill-height {
  min-height: 100vh;
}
.right-align {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
</style>