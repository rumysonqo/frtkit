<template>
    <v-container fluid class="ma-0" grid-list-lg>
        <v-layout class="mt-0">
    
        <v-flex xs4 class="pa-0 ma-0">
        <v-select
            v-model="cod_meta"
            :items=ds_meta
            item-text="meta"
            item-value="cod_meta"
            label="Seleccione una meta"
            dense
            outlined
            @change="get_tareas(), kit_por_meta()"
          >
          </v-select>
    
        </v-flex>
    
        <v-flex xs4 class="pa-0 ml-2">
        <v-select
            v-model="cod_tar"
            :items=ds_tarea
            item-text="sub_finalidad"
            item-value="cod_subfin"
            label="Seleccione una tarea"
            outlined
            dense
            @change="kit_por_meta_tarea()"
          >
          </v-select>
    
        </v-flex>
        
        </v-layout>
    
        <v-layout>
        <v-flex  xs12 class="pa-0 ma-0">
        
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
            this.get_metas();
            this.get_tareas();
            //this.kit_por_meta();
            //this.kit_por_meta_tarea();
        },
        
        data(){
            return{
                cadena:'',
                cod_meta:null,
                cod_tar:null,
                search:[],
                ds_prog:[],
                ds_meta:[],
                ds_tarea:[],
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
            async get_metas(){
                try {
                    let datos=await axios.get(url+'metas/')
                    this.ds_meta= await datos.data;    
                } catch (error) {
                    console.log(error);
                }
            },
            async get_tareas(){
                try {
                    let datos=await axios.get(url+'tareas/'+this.cod_meta)
                    this.ds_tarea= await datos.data;    
                } catch (error) {
                    console.log(error);
                }
            },
            
            async kit_por_meta(){
                try{
                let datos=await axios.get(url+'kit_por_meta/'+this.cod_meta)
                console.log(datos.data);
                this.ds_kit=await datos.data 
                }catch(error){
                console.log(error);
                }
          },
          
          async kit_por_meta_tarea(){
            try{
            let datos=await axios.get(url+'kit_por_meta_tarea/'+this.cod_meta+'/'+this.cod_tar)
            console.log(datos.data);
            this.ds_kit=await datos.data 
            }catch(error){
            console.log(error);
            }
          }
        }
    }
    </script>