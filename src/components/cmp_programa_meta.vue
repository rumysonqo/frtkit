<template>
    <v-container fluid class="ma-0" grid-list-lg>
        <v-layout>
        
    
        <v-flex xs4 class="pa-0">
        <v-select
            v-model="cod_prg"
            :items=ds_prog
            item-text="programa"
            item-value="cod_programa"
            label="Seleccione un programa"
            outlined
            dense
            @change="get_prog_metas()"
          >
          </v-select>
    
        </v-flex>
    
        <v-flex xs4 class="pa-0 ml-2">
        <v-select
            v-model="cod_meta"
            :items=ds_meta
            item-text="meta"
            item-value="cod_meta"
            label="Seleccione una meta"
            outlined
            dense
            @change="kit_por_programa_meta()"
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
              <v-text-field v-model="search" outlined dense filled append-icon="mdi-magnify" label="Item a Buscar" single-line hide-details>
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
    name:'cmp_programa_meta',
    mounted(){
        this.get_programas();
        this.get_prog_metas();
        //this.kit_por_programa();
        //this.kit_por_programa_meta_cadena();
    },
    
    data(){
        return{
            cadena:'',
            cod_prg:null,
            cod_meta:null,
            search:[],
            ds_prog:[],
            ds_meta:[],
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
        async get_prog_metas(){
            try {
                let datos=await axios.get(url+'prog_metas/'+this.cod_prg)
                this.ds_meta= await datos.data;    
            } catch (error) {
                console.log(error);
            }
        },

        async kit_por_programa(){
            try{
            let datos=await axios.get(url+'kit_por_programa/'+this.cod_prg)
            console.log(datos.data);
            this.ds_kit=await datos.data 
            }catch(error){
            console.log(error);
            }
        },

        async kit_por_programa_meta(){
            try{
                let datos=await axios.get(url+'kit_por_programa_meta/'+this.cod_prg+'/'+this.cod_meta)
                console.log(datos.data);
                this.ds_kit=await datos.data 
            }catch(error){
                console.log(error);
            }
        },
        
    }
}
</script>