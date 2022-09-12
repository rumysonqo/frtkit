<template>
    <v-container>
    <v-app-bar
    app
    color="primary"
    dark
    >
    <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    <v-toolbar-title>KITS SIGA-PPR 2022</v-toolbar-title>

    </v-app-bar>

    <v-navigation-drawer
    v-model="drawer"
    app
    temporary
    class="blue darken-3"
    >
    <v-layout class="text-center">
      <h1 class="white--text">Opciones</h1>
    </v-layout>
    <v-list
    nav
    dense
    >
    <v-list-item-group
        v-model="group"
        active-class="blue darken-4--text text--accent-4"
    >

      <v-list-item>
        
          <v-list-item-title class="white--text">
            <router-link style="text-decoration: none; color: inherit;" to="/">
              <v-btn color="blue darken-4--text" elevation="5" block dark>
              Inicio
            </v-btn>
            </router-link>
          </v-list-item-title>
        
      </v-list-item>

      <v-list-item>
          <v-list-item-title class="white--text">
            <router-link style="text-decoration: none; color: inherit;" to="/por_programa">
              <v-btn color="blue darken-4--text" elevation="5" block dark>
              Por Programa
              </v-btn>
            </router-link>
          </v-list-item-title>
      </v-list-item>

      <v-list-item>
        <v-list-item-title class="white--text">
          <router-link style="text-decoration: none; color: inherit;" to="/por_programa_meta">
            <v-btn color="blue darken-4--text" elevation="5" block dark>
            Por Prog./Meta
            </v-btn>
          </router-link>
        </v-list-item-title>
      </v-list-item>

      <v-list-item>
        <v-list-item-title class="white--text">
          <router-link style="text-decoration: none; color: inherit;" to="/por_meta_tarea">
            <v-btn color="blue darken-4--text" elevation="5" block dark>
            Por Meta/Tarea
            </v-btn>
          </router-link>
        </v-list-item-title>
      </v-list-item>

      <v-list-item>
        <v-list-item-title class="white--text">
          <router-link style="text-decoration: none; color: inherit;" to="/por_clasificador">
            <v-btn color="blue darken-4--text" elevation="5" block dark>
            Por Clasificador
            </v-btn>
          </router-link>
        </v-list-item-title>
      </v-list-item>

      <v-list-item>
        <v-list-item-title class="white--text">
          <router-link style="text-decoration: none; color: inherit;" to="/por_meta_clasificador">
            <v-btn color="blue darken-4--text" elevation="5" block dark>
            Por Meta/Clasif.
            </v-btn>
          </router-link>
        </v-list-item-title>
      </v-list-item>

        
    </v-list-item-group>
    </v-list>
    </v-navigation-drawer>
</v-container>
</template>

<script>
    export default {
      name: 'cmp_menu',
    
      data: () => ({
        //
        drawer: false,
        group: null,
      }),
      watch: {
          group () {
            this.drawer = false
          },
        },
    };
</script>
    