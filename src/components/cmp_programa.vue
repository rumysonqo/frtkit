<template>
    <v-container fluid class="ma-0" grid-list-lg>
        <v-layout>
        <v-flex xs4 class="pa-0 ma-0">
        <v-select
            v-model="cod_prg"
            :items=ds_prog
            item-text="programa"
            item-value="cod_programa"
            label="Seleccione un programa"
            outlined
            dense
            @change="kit_por_programa()"
          >
          </v-select>
    
        </v-flex>

        <v-flex xs4 class="pa-0 ml-2">
            <v-text-field v-model='cadena'
                v-on:keyup.enter='kit_por_programa'
                label="busqueda por item/familia"
                placeholder="texto a buscar"
                dense
                filled
                outlined
                append-icon="mdi-magnify"
                >
            </v-text-field>
        
            </v-flex>
        
        </v-layout>
    
        <v-layout>
        <v-flex  xs12 class="pa-0 ma-0">
        
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
        name:'cmp_programa',
        mounted(){
            this.get_programas();
            this.kit_por_programa();
        },
        
        data(){
            return{
                cadena:'',
                cod_prg:1,
                ds_prog:[],
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
            async get_programas(){
                try {
                    let datos=await axios.get(url+'programas')
                    this.ds_prog= await datos.data;    
                } catch (error) {
                    console.log(error);
                }
            },
            
            async kit_por_programa(){
                if(this.cadena===''){
                    try{
                    let datos=await axios.get(url+'kit_por_programa/'+this.cod_prg)
                    console.log(datos.data);
                    this.ds_kit=await datos.data 
                    }catch(error){
                    console.log(error);
                    }
                }else{
                    try{
                    let datos=await axios.get(url+'kit_por_programa_cadena/'+this.cod_prg+'/'+this.cadena)
                    console.log(datos.data);
                    this.ds_kit=await datos.data 
                    }catch(error){
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
