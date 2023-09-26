<template>
  <v-app id="inspire">
    <v-app-bar>
      <v-app-bar-nav-icon
        @click="OpcionesVisibles = !OpcionesVisibles"
      ></v-app-bar-nav-icon>

      <v-app-bar-title>Menu Principal</v-app-bar-title>
    </v-app-bar>
    <!--Menu del NavigationBar-->
    <v-navigation-drawer v-model="OpcionesVisibles" temporary
    class="bg-deep-purple"
        theme="dark"
        permanent
        
    >
   
        <v-list v-model:opened="open">
          <v-list-item prepend-icon="mdi-home" title="Home"></v-list-item>

          <v-list-group value="Users">
            <template v-slot:activator="{ props }">
              <v-list-item
                v-bind="props"
                prepend-icon="mdi-account-circle"
                title="Users"
              ></v-list-item>
            </template>

            <v-list-group value="Admin">
              <template v-slot:activator="{ props }">
                <v-list-item v-bind="props" title="Admin"></v-list-item>
              </template>

              <v-list-item
                v-for="([title, icon], i) in admins"
                :key="i"
                :title="title"
                :prepend-icon="icon"
                :value="title"
              ></v-list-item>
            </v-list-group>

            <v-list-group value="Actions">
              <template v-slot:activator="{ props }">
                <v-list-item v-bind="props" title="Actions"></v-list-item>
              </template>

              <v-list-item
                v-for="([title, icon], i) in cruds"
                :key="i"
                :value="title"
                :title="title"
                :prepend-icon="icon"
              ></v-list-item>
            </v-list-group>
          </v-list-group>
        </v-list>
   
    </v-navigation-drawer>
    <!--/Menu del NavigationBar-->

    
    

    <v-main class="bg-grey-lighten-2">
      <v-container>
        <v-row>
          <template v-for="n in 4" :key="n">
            <v-col class="mt-2" cols="12">
              <strong>Category {{ n }}</strong>
            </v-col>

            <v-col v-for="j in 6" :key="`${n}${j}`" cols="6" md="2">
              <v-sheet height="150"></v-sheet>
            </v-col>
          </template>
        </v-row>
      </v-container>
      <FooterApp></FooterApp>
    </v-main>
  </v-app>
</template>

<script>
import { ref } from "vue";
// Components
import FooterApp from "../src/components/Footer.vue";

import  Navbar from "../src/components/Navbar.vue";

export default {
  name: "App",
  components: {
    FooterApp, // Registra el componente de pie de página en el componente principal
    Navbar
  },
  setup() {
    const OpcionesVisibles = ref(true);
    const open = ref(["Users"]);
    const admins = ref([
      ["Management", "mdi-account-multiple-outline"],
      ["Settings", "mdi-cog-outline"],
    ]);
    const cruds = ref([
      ["Create", "mdi-plus-outline"],
      ["Read", "mdi-file-outline"],
      ["Update", "mdi-update"],
      ["Delete", "mdi-delete"],
    ]);

    // Retorna 'items' desde el bloque 'setup'
    return {
      open,
      admins,
      cruds,
      OpcionesVisibles,
    };
  },
};
</script>
