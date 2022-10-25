<template>
  <div class="categoria">
    </div>
    <h1>Categorias</h1>
    <form @submit.prevent="agregarCategoria()">
      <div class="input-group mb-3 justify-content-center">
        <div class="input-group-prepend flex-colunm col-4">
          <input type="text" class="form-control col-4" v-model="categoria.nombre" placeholder="Categoria" required
          aria-describedby="button-addon2">
        </div>
      </div>
      <div class="input-group mb-3 justify-content-center">
        <button class="btn btn-success " type="submit">Agregar</button>
      </div>
    </form>
    <div class="col m12 card-panel">
      <table class="table table-bordered ">
        <thead class="table-dark">
          <tr>
            <th scope="col">Codigo</th>
            <th scope="col">Nombre</th>
            <th scope="col">Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(cat, index) in categorias">
            <th>{{cat.id}}</th>
            <td>{{cat.nombre}}</td>
            <td>
              <button @click="actualizarCategoria(id,nombre)" class="btn btn-warning">Actualizar</button>
              <button @click="borrarCategoria(cat.id)" class="btn btn-danger">Borrar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
</template>


<script>
import router from "@/router";
    export default {
        name: 'categoriaView',
        data(){
            return {
                categoria:{
                    nombre:null
                },
                categorias:[]
            }
        },
        methods: {
            agregarCategoria(){
                axios({
                    method: "post",
                    url: "http://localhost:3000/categorias",
                    data: this.categoria
                })
                .then(response => {
                    console.log(response);
                    this.getCategorias()
                })
                .catch(e => console.log(e));
            },
            actualizarCategoria(id, nombre) {
              const actualizarCategoria = (view)=> {
                router.push(Activos.path);
              }
              return{
                sendtoview
              }
            },
            borrarCategoria(categoria_id){
              if(confirm("Está seguro de eliminar la categoria " + categoria_id + "?"))
                axios({
                    method: "delete",
                    url: "http://localhost:3000/categorias/"+categoria_id,
                    data: this.categorias
                })
                .then(response => {
                    console.log(response);
                    this.getCategorias()
                })
                .catch(e => console.log(e));
            },
            getCategorias(){
                axios({
                    method: "get",
                    url: "http://localhost:3000/categorias",
                })
                .then(response => {
                    this.categorias = response.data;
                console.log(response);
                })
                .catch(e => console.log(e));
            },

        },
        computed: {
        },
        mounted(){
            this.getCategorias()
        },
        components: {
        }
    }
</script>
<style>

</style>
