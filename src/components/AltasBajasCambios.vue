<template>
<header class="header"></header>

        <div @mousemove="onMousemoveA"
        :class="{ 'gray-bg': x < 5, 'blue-bg': x >= 5 }"
  class="BGAN gray-bg" style="border-top: 5px solid #666666;border-bottom: 5px solid #666666">

    <h1 :class="{'hiddenA-text': x < 5, 'visible-text': x >= 5}">Productos ACME</h1>
    <p :class="{'hiddenA-text': x < 5, 'hiddenB-text': x >= 5}">.</p>

</div>



    <div class="container" style="Background-color: #363636;">
        <div class="d-flex justify-content-start mt-5">
            <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#myModal">
                Nuevo producto
            </button>
        </div>

        <table class="table mt-5">
            <thead>
                <tr>
                    <th class="TXWc" scope="col">ID</th>
                    <th class="TXWc" scope="col">Nombre</th>
                    <th class="TXWc" scope="col">Descripcion</th>
                    <th class="TXWc" scope="col">Acciones</th>
                </tr>
            </thead>
            <tbody class="TB">
                <tr v-for="(producto, index) in Productos" :key="index">
                    <td>{{ producto.id }}</td>
                    <td>{{ producto.nombre }}</td>
                    <td>{{ producto.Desc }}</td>
                    <td class="">
                        <button type="button" class="btn btn-warning" data-toggle="modal" data-target="#myModaledit"  @click="llenar(index)">
                            Editar
                        </button>
                        <button type="button" class="btn btn-danger ml-2" data-toggle="modal" data-target="#myModal"
                        @click="DeleteProducto(producto.id)">
                            Eliminar
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

    <!-- ventana modal -->

    <!-- Esta es tu ventana modal -->
    <div class="modal fade BGTf" id="myModal" >
        <div class="modal-dialog">
            <div class="modal-content BGTo">
                <div class="modal-header">
                    <h5 class="modal-title TXWc">Agrega un Producto</h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="Number" class="form-control BGTl TXWl" placeholder="ID del producto" v-model="newProducto.Id">
                    </div>

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTl TXWl" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTl TXWl" placeholder="Descripcion del producto"
                            v-model="newProducto.Descripcion">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" data-dismiss="modal" @click="AddProducto()">Guardar
                        datos</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Esta es tu ventana modal para Editar -->
    <div class="modal fade BGTf" id="myModaledit">
        <div class="modal-dialog">
            <div class="modal-content BGTo">
                <div class="modal-header">
                    <h5 class="modal-title TXWc">Editando un Producto </h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <div class="input-group input-group-sm mb-3">
                        <input id = "idedit" type="Number" class="form-control BGTl TXWl" placeholder="ID del producto" v-model="newProducto.Id">
                    </div>

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTl TXWl" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTl TXWl" placeholder="Descripcion del producto"
                            v-model="newProducto.Descripcion">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" data-dismiss="modal" @click="UupdateProducto()">Guardar
                        datos</button>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import { ref } from 'vue';
//import image from '@/assets/ARA.jpg';
export default {
    data() {
        return {
            Productos: [],
            newProducto: { id: "", nombre: '', Descripcion: "" },
            UpdatePorducto: {id:""},
            ide: -1,
            ide2: 0,
            x: ref(0)            
        };
    },
    methods: {
        //añadir un producto
        AddProducto() {
            const nuevoProducto = {
                id: this.newProducto.Id,
                nombre: this.newProducto.Nombre,
                Desc: this.newProducto.Descripcion
            };

            this.Productos.push(nuevoProducto);

            //se limpian los campos
            this.newProducto.Id = "";
            this.newProducto.Nombre = "";
            this.newProducto.Descripcion = "";
        },
        DeleteProducto() {

        },
        UupdateProducto( ) {
            const prodact={
                id: this.newProducto.Id,
                nombre: this.newProducto.Nombre,
                Desc: this.newProducto.Descripcion
            }
            
            this.Productos[this.ide2]= prodact;
            
            
            this.newProducto.Id = "";
            this.newProducto.Nombre = "";
            this.newProducto.Descripcion = "";
            

        },
        llenar(ide){
            this.ide2 = ide;
            var prod = this.Productos[ide];
            this.newProducto.Id = prod.id;
            this.newProducto.Nombre = prod.nombre;
            this.newProducto.Descripcion = prod.Desc;

        },        
        onMousemoveA(e) {
            this.x = e.clientX;
        }
        
    }
}
</script>
  
<style scoped>
/* Aquí van los estilos CSS de tu componente */
.BGAN:hover {
    transition: 5s background-color ease;
}
.gray-bg, .blue-bg {
  background-color: hsl(0, 0%, 35%);
  background-image: url(~@/assets/BGIm01.jpg);
  background-size:cover;
  background-position:0cm;  
  transition: background-color 5s ease;
}
.blue-bg {
  background-color: hsla(209, 100%, 50%, 0.575);  

}

.hiddenA-text {
  color: hsla(0, 0%, 0%, 0);
  text-align:center;
  font-weight: bold;
  font-size: 10px;
  transition: color 2s ease,font-size 5s ease; /* Transición suave de la opacidad */  
}
.hiddenB-text {
  color: hsla(0, 0%, 0%, 0);
  text-align:right;
  font-size: 100px;
  transition: color 2s ease,font-size 5s ease; /* Transición suave de la opacidad */  
}

.visible-text{
    color: hsl(0, 0%, 100%);
    font-weight: bold;
    font-size:35px;
    transition: color 5s ease,font-size 5s ease;    
    text-align:center;
}

.header {
  margin-top: 0;
  padding-top: 0;
}

.TXWc{
    color: hsl(0, 0%, 100%);
    font-weight: bold;
    font-size:12px;
}

.TXWl{
    color: hsl(0, 0%, 100%);    
    font-size:12px;
}

.TB{
    Background-color: #363636;
    color: hsl(0, 0%, 100%);
    font-weight: bold;
    font-size:10px;
    text-align: center;
}

.BGTf{
    Background-color: #36363686;
}

.BGTo{
    Background-color: #363636;
}

.BGTl{
    Background-color: #464646;
}
input::placeholder{
    color: hsl(0, 0%, 100%);    
    font-size:12px;
}
</style>
  