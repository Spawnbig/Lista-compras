<template>
<header>
  <b-card class="text-center pt-4 pb-4">
    <div>
      <h1 class="fw-bold">Lista de compras</h1>
    </div>
  </b-card>
</header>

<main>
  <section class="text-center container-md">
    <header><h3 class="fs-4 mt-5">Agregar elemento a lista</h3></header>
    <article >
      <b-form @reset="onReset">
        <div class="container-sm">
          <div class="row mt-5">
            <div class="col-6">
              <b-form-input
              id="type-text"
              v-model="nombreProducto"
              placeholder="Nombre producto" 
              ></b-form-input>
            </div>
            <div class="col">
              <b-form-input 
              id="type-number"
              v-model="cantidad"
              placeholder="Cantidad"
              ></b-form-input>
            </div>
            <div class="col-1">
              <b-button v-on:click="addData()" variant="success">Agregar</b-button>
            </div>
            <div class="col-1">
              <b-button type="reset" variant="danger">Reset</b-button>
          </div>
         </div>
        </div>
      </b-form>
    </article>
    <article>
      <b-card
      class="mt-5" 
      title="Listado de compras">

      <b-list-group horizontal class="d-flex justify-content-between align-items-center">
        <b-list-group-item class="border-0">Nombre Producto</b-list-group-item>
        <b-list-group-item class="border-0 pe-5 me-4">Cantidad</b-list-group-item>
        <b-list-group-item class="border-0">Eliminar</b-list-group-item>
      </b-list-group>

      <div v-if="render">
        <b-list-group horizontal class="d-flex justify-content-between text-left" v-for="c in compras" :key="c.id">
          <b-list-group-item class="border-0" >{{c.nombre}}</b-list-group-item>
          <b-list-group-item class="border-0">{{c.cantidad}}</b-list-group-item>
          <b-list-group-item class="border-0">
            <b-button variant="danger" @click="deleteElement(c.id)">X</b-button>
          </b-list-group-item>
        </b-list-group>
      </div>
      </b-card>
    </article>
  </section>
</main>
</template>

<script>


export default {
  data(){
    return{
      nombreProducto: null,
      cantidad: null,
      compras:[],
      render:false
    }
  },
  methods:{
    addData(){
      if(this.nombreProducto != null && this.cantidad != null && !isNaN(this.cantidad) && this.cantidad > 0){
        
        let compra = {
          id: this.compras.length+1,
          nombre : this.nombreProducto,
          cantidad : this.cantidad
        }
        this.compras.push(compra)
        this.render = true;
        console.log(this.compras)
      }
    },
    deleteElement(id){
      this.compras.splice(id-1,this.compras.length)
    }
  }
}
</script>

<style>

</style>
