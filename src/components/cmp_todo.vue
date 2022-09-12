<template>
    <v-container fluid class="ma-0" grid-list-lg>
        <v-layout>
        <v-flex xs3 class="mb-0 pa-0">
        <v-text-field v-model='cadena'
            v-on:keyup.enter='bus_todo'
            label="Ingrese cadena de busqueda"
            placeholder="texto a buscar"
            outlined
            filled
            dense
            >
        </v-text-field>
    
        </v-flex>
        </v-layout>
    
        <v-layout>
        <v-flex  xs12 class="mt-0 pa-0">
          <v-data-table
          :headers="headers"
          :items="ds_kit"
          class="elevation-5"
          :footer-props="{
          'items-per-page-options': [10, 20, 30, 40, 50]}"
          :items-per-page="30"
          >
          </v-data-table>
        
        </v-flex>
      </v-layout>
      </v-container>  
    
        
    </template>
    
    <script>
    import axios from "axios";
    let url='http://localhost:8000/api/';
    export default {
        name:'cmp_todo',
        mounted(){
            this.ver_todo();
        },
        data(){
            return{
                cadena:'',
                ds_kit:[],
                headers:[{
                text:'CODIGO',
                align:'start',
                value:'cod_item_fam',
                class:'blue darken-3 white--text',
                },
                {
                text:'ITEM/FAMILIA',
                align:'start',
                value:'nom_item_fam',
                class:'blue darken-3 white--text',
                
                },
                {
                text:'NIVEL',
                align:'center',
                filterable: false,
                value:'nivel',
                class:'blue darken-3 white--text'
                },
                {
                text:'TIPO',
                align:'center',
                filterable: false,
                value:'tipo_bien',
                class:'blue darken-3 white--text'
                },
                {
                text:'TIPO DE CALCULO',
                align:'center',
                filterable: false,
                value:'tipo_calculo',
                class:'blue darken-3 white--text'
                },
                {
                text:'PROGRAMA',
                align:'start',
                filterable: false,
                value:'programa',
                class:'blue darken-3 white--text'
                },
                {
                text:'META',
                align:'start',
                filterable: false,
                value:'meta',
                class:'blue darken-3 white--text'
                },
                {
                text:'SUB FINALIDAD',
                align:'start',
                filterable: false,
                value:'sub_finalidad',
                class:'blue darken-3 white--text'
                },
                {
                text:'CLASIFICADOR',
                align:'start',
                filterable: false,
                value:'clasificador',
                class:'blue darken-3 white--text'
                }]
                
            }
        },
        methods:{
            async ver_todo(){
              try {
                let datos=await axios.get(url+"mostrar_todo")
                this.ds_kit= await datos.data;    
              } catch (error) {
                console.log(error);
              }
            },
    
            async bus_todo(){
                if(this.cadena!=""){
                    try {
                    let datos=await axios.get(url+"buscar_todo/"+this.cadena)
                    this.ds_kit= await datos.data;    
                    } catch (error) {
                        console.log(error);
                    }
                }else{
                    try {
                        let datos=await axios.get(url+"mostrar_todo")
                        this.ds_kit= await datos.data;    
                    } catch (error) {
                        console.log(error);
                    }     
                }
                
              
            }
        }
    }
    </script>

<style>
    tbody tr:nth-of-type(odd) {
        /* 'teal lighten-5' basides on material design color */
        background-color: #b0ecfb;
    }
    
    tbody tr:nth-of-type(even) {
        /* 'deep-orange lighten-5' basides on material design color */
        background-color: #fefefe;
    }
</style>
    