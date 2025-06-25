  <template>
    <v-app>
      <v-main>
        <v-container class="py-10">
          <v-row justify="center">
            <v-col cols="12" md="10">
              <v-card elevation="4">
                <v-card-title>
                  <span class="text-h6 font-weight-medium">Leads de usuario</span>
                  <v-spacer />
                </v-card-title>

                <v-data-table
                  :headers="headers"
                  :items="items"
                  class="elevation-1"
                  :items-per-page="5"
                  density="comfortable"
                >
                </v-data-table>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main> 
    </v-app>
  </template>

  <script>
  export default {
    data() {
      return {
        headers: [
          { title: 'Nome', value: 'nome', sortable: true },
          { title: 'Email', value: 'email', sortable: true },
          { title: 'telefone', value: 'whatsapp', sortable: true },
        ],
        items: [],
      }
    },
    async created() {
      await this.getLeads();
    },
    methods: {
      async getLeads() {
        try {
          const request = await fetch('http://localhost:3333/leads', {
            method: 'GET',
            headers: {
              'Content-Type': 'application/json'
            }
          });
          const response = await request.json();
          
          if (!request.ok) {
            alert('Erro ao carregar os leads, tente novamente mais tarde.');
            return;
          }
          this.items = response.data;
        } catch (error) {
          console.error('Erro ao buscar os leads:', error);
        }
      }
    },
  }

  </script>

  <style scoped>
  .v-data-table {
    border-top: 1px solid #e0e0e0;
  }
  </style>
