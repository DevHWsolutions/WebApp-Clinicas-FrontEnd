<template>
  <v-app id="inspire">
    <v-app-bar>
      <v-app-bar-nav-icon @click="rail = !rail"></v-app-bar-nav-icon>

      <v-app-bar-title>Menu Principal</v-app-bar-title>
    </v-app-bar>
    <!--Menu del NavigationBar-->
  <v-navigation-drawer :rail="rail" permanent @click="rail = false" class="sidebar">
    <v-list-item
      prepend-avatar="https://randomuser.me/api/portraits/men/80.jpg"
      title="Menú"
      nav
      class="menu-item" 
    >
      <template v-slot:append>
        <v-btn
          variant="text"
          icon="mdi-chevron-left"
          @click.stop="rail = !rail"
        ></v-btn>
      </template>
    </v-list-item>

    <v-divider></v-divider>

    <v-list density="compact" nav>
      <v-list-item
        prepend-icon="mdi-calendar-today"
        title="Agenda"
        value="home"
        class="menu-item" 
      ></v-list-item>
      <v-list-item
        prepend-icon="mdi-folder-account"
        title="Expediente"
        value="account"
        class="menu-item" 
      ></v-list-item>
      <v-list-item
        prepend-icon="mdi-folder-plus"
        title="Nuevo Expediente"
        value="users"
       class="menu-item" 
      ></v-list-item>
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

import Navbar from "../src/components/Navbar.vue";

export default {
  name: "App",
  components: {
    FooterApp, // Registra el componente de pie de página en el componente principal
    Navbar,
  },
  setup() {
    const ActiveItem = ref(true);
    const rail = ref(true);

    // Retorna 'items' desde el bloque 'setup'
    return {
      ActiveItem,
      rail,
    };
  },
};
</script>

<style>
:root{
  --siderbar-bg-color :#2f855a;
  --sidebar-item-hover: #38a169;
  --sidebar-item-active: #fd1f1c;
  
}
 
 /* 
 --sidebar-item-hover: #38a169;
  --sidebar-item-active: #276749;
 */
</style>

<style scoped>

 
.sidebar{
  color: white;
  background-color: var(--sidebar-bg-color);
}
.menu-item:hover {
  background-color: var(--sidebar-item-hover);
}

.menu-item.active {
  background-color: var(--sidebar-item-active);
}


</style>

