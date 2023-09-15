<template>
    <h1>CRUD DE DATOS</h1>
    <div class="container">
        <div class="d-flex justify-content-start mt-5">
            <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#myModal">
                Nuevo producto
            </button>
        </div>

        <table class="table mt-5">
            <thead>
                <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Descripcion</th>
                    <th scope="col">Acciones</th>
                </tr>
            </thead>
            <tbody>
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
    <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Título del modal</h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="Number" class="form-control" placeholder="ID del producto" v-model="newProducto.Id">
                    </div>

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control" placeholder="Descripcion del producto"
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
    <div class="modal fade" id="myModaledit">
        <div class="modal-dialog">

            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Editar producto </h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <div class="input-group input-group-sm mb-3">
                        <input id = "idedit" type="Number" class="form-control" placeholder="ID del producto" v-model="newProducto.Id">
                    </div>

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control" placeholder="Descripcion del producto"
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
export default {
    data() {
        return {
            Productos: [],
            newProducto: { id: "", nombre: '', Descripcion: "" },
            UpdatePorducto: {id:""},
            ide: -1,
            ide2: 0
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

        }
        
        
    }
}
</script>
  
<style scoped>
/* Aquí van los estilos CSS de tu componente */
</style>
  