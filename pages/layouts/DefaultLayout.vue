<template>
  <v-card>
    <v-layout>
      <v-app-bar color="blue" prominent>
        <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />

        <div class="text-h6 text-white font-weight-bold mx-auto" @click="navigateTo('/')">Trancity</div>

        <v-btn icon variant="text" @click="login">
          <v-icon color="white">mdi-account</v-icon>
        </v-btn>
      </v-app-bar>

      <v-navigation-drawer
        v-model="drawer"
        :location="$vuetify.display.mobile ? 'bottom' : undefined"
        temporary
        color="blue"
      >

        <v-list density="compact" nav>
          <v-list-item to="/" prepend-icon="mdi-home" title="Home" value="home" />
        </v-list>
      </v-navigation-drawer>

      <!-- Main Content Area -->
      <v-main style="height: 100dvh;">
        <slot />
      </v-main>
    </v-layout>
  </v-card>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useDisplay } from 'vuetify'

const drawer = ref(false)
const router = useRouter()
const { mobile } = useDisplay()

const login = () => {
  router.push('/login')
}
</script>

<style scoped>
.text-white {
  color: white;
}
</style>
