<template>
  <div class="categoria">
    </div>
    <h1>Categorias</h1>
    <form @submit.prevent="agregarCategoria()">
      <div class="input-group mb-3 justify-content-center">
        <div class="input-group-prepend flex-colunm col-4">
          <input type="text" class="form-control col-4" v-model="categoria.nombre" placeholder="Categoria"
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
              <button @click="formActualizar(index)" class="btn btn-warning">Actualizar</button>
              <button @click="borrarCategoria(index)" class="btn btn-danger">Borrar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
</template>


<script>
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
            setearCheckbox(terminado, id) {
                axios({
                    method: "patch",
                    url: "http://localhost:3000/categorias"+id,
                    data: {
                        terminado: !terminado
                    }
                })
                .then(response => {
                console.log(response);
                })
                .catch(e => console.log(e));
            }
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
