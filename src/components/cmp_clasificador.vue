<template>
    <v-container fluid class="ma-0" grid-list-lg>
        <v-layout>
        <v-flex xs6 class="mt-0 mb-0">
        <v-select
            v-model="cod_clf"
            :items=ds_clf
            item-text="clasificador"
            item-value="cod_clasificador"
            label="Seleccione un clasificador"
            outlined
            dense
            @change="kit_por_clasificador()"
          >
          </v-select>
    
        </v-flex>
        
        </v-layout>
    
        <v-layout>
        <v-flex  xs12 class="mt-0">
        
          <v-data-table
          :headers="headers"
          :items="ds_kit"
          :search="search"
          class="elevation-5"
          :footer-props="{
          'items-per-page-options': [10, 20, 30, 40, 50]}"
          :items-per-page="30"
          >
            <template v-slot:top>
                <v-col cols="4" sm="4">
                <v-text-field v-model="search" outlined dense filled append-icon="mdi-magnify" label="Buscar" single-line hide-details>
                </v-text-field>
                </v-col>
            </template>
          </v-data-table>
        
        </v-flex>
      </v-layout>
      </v-container>  
    
        
    </template>
    
    <script>
    import axios from "axios";
    let url='http://localhost:8000/api/';
    export default {
        name:'cmp-Inicio',
        mounted(){
            this.get_clasificador();
            //this.kit_por_clasificador();
        },
        
        data(){
            return{
                cadena:'',
                cod_clf:null,
                search:[],
                ds_clf:[],
                ds_kit:[],
                headers:[{
                text:'CODIGO',
                align:'start',
                value:'cod_item_fam',
                class:'deep-purple accent-4 white--text',
                },
                {
                text:'ITEM/FAMILIA',
                align:'start',
                value:'nom_item_fam',
                class:'deep-purple accent-4 white--text',
                
                },
                {
                text:'NIVEL',
                align:'center',
                filterable: false,
                value:'nivel',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'TIPO',
                align:'center',
                filterable: false,
                value:'tipo_bien',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'TIPO DE CALCULO',
                align:'center',
                filterable: false,
                value:'tipo_calculo',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'PROGRAMA',
                align:'start',
                filterable: false,
                value:'programa',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'META',
                align:'start',
                filterable: false,
                value:'meta',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'SUB FINALIDAD',
                align:'start',
                filterable: false,
                value:'sub_finalidad',
                class:'deep-purple accent-4 white--text'
                },
                {
                text:'CLASIFICADOR',
                align:'start',
                filterable: false,
                value:'clasificador',
                class:'deep-purple accent-4 white--text'
                }]
                
            }
        },
        methods:{
            async get_clasificador(){
                try {
                    let datos=await axios.get(url+'clasificador')
                    this.ds_clf= await datos.data;    
                } catch (error) {
                    console.log(error);
                }
            },
            
            async kit_por_clasificador(){
                try{
                let datos=await axios.get(url+'kit_por_clasificador/'+this.cod_clf)
                console.log(datos.data);
                this.ds_kit=await datos.data 
                }catch(error){
                console.log(error);
                }
            
            
          }
        }
    }
    </script>