<template>
    <header class="header"></header>

    <div @mousemove="onMousemoveA" :class="{ 'gray-bg': x < 5, 'blue-bg': x >= 5 }" class="BGAN gray-bg"
        style="border-top: 5px solid #666666;border-bottom: 5px solid #666666">

        <h1 :class="{ 'hiddenA-text': x < 5, 'visible-text': x >= 5 }">Caja Plantas Huerticas</h1>
        <p :class="{ 'hiddenA-text': x < 5, 'hiddenB-text': x >= 5 }">.</p>

    </div>



    <div class="container" style="Background-color: #363636;">
        <div class="d-flex justify-content-start mt-5">
            <button type="button" class="BotonP BotonAgregar TxtBlancoB" data-toggle="modal" data-target="#myModal">
                Nuevo producto
            </button>
        </div>

        <table class="table mt-5">
            <thead>
                <tr>
                    <th class="TxtBlancoB" scope="col">ID</th>
                    <th class="TxtBlancoB" scope="col">Nombre</th>
                    <th class="TxtBlancoB" scope="col">Descripcion</th>
                    <th class="TxtBlancoB" scope="col">Acciones</th>                    
                </tr>
            </thead>
            <tbody class="TxtBlancoB">
                <tr v-for="(producto, index) in Productos" :key="index">
                    <td>{{ producto.id }}</td>
                    <td>{{ producto.nombre }}</td>
                    <td>{{ producto.Desc }}</td>
                    <td class="">
                        <button type="button" class="BotonP BotonAviso TxtBlancoB" data-toggle="modal" data-target="#myModaledit"
                            @click="llenar(index)">
                            Editar
                        </button>
                        <button type="button" class="BotonP BotonEliminar TxtBlancoB" data-toggle="modal"
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
    <div class="modal fade BGVtnModalFade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content BGVtnModalPrincipal">
                <div class="modal-header">
                    <h5 class="modal-title TxtBlancoB">Agrega un Producto</h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <!-- <div class="input-group input-group-sm mb-3">
                        <input type="Number" class="form-control BGTl TXWl" placeholder="ID del producto"
                            v-model="newProducto.Id">
                    </div> -->

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTextHolder TxtBlancoN" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTextHolder TxtBlancoN" placeholder="Descripcion del producto"
                            v-model="newProducto.Descripcion">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="BotonP BotonConfirmacion TxtBlancoB" data-dismiss="modal" @click="AddProducto()">Guardar
                        datos</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Esta es tu ventana modal para Editar -->
    <div class="modal fade BGVtnModalFade" id="myModaledit">
        <div class="modal-dialog">
            <div class="modal-content BGVtnModalPrincipal">
                <div class="modal-header">
                    <h5 class="modal-title TxtBlancoB">Editando un Producto d</h5>
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                </div>
                <div class="modal-body">
                    <!-- id -->
                    <!--
                    <div class="input-group input-group-sm mb-3">
                        <input id="idedit" type="Number" class="form-control BGTl TXWl" placeholder="ID del producto"  
                            v-model="newProducto.Id">
                    </div>
                    -->

                    <!-- Nombre-->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTextHolder TxtBlancoN" placeholder="Nombre del producto"
                            v-model="newProducto.Nombre">
                    </div>

                    <!-- Descripcion -->
                    <div class="input-group input-group-sm mb-3">
                        <input type="text" class="form-control BGTextHolder TxtBlancoN" placeholder="Descripcion del producto"
                            v-model="newProducto.Descripcion">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="BotonP BotonConfirmacion TxtBlancoB" data-dismiss="modal" @click="UupdateProducto()">Guardar
                        datos</button>
                </div>
            </div>
        </div>

    </div>
    <!-- Mensaje de error cuando hay id duplicado, solo se muestra si no está vacío -->
    <div v-if="mensajeError" class="alert alert-danger mt-3">
        {{ mensajeError }}
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
            UpdatePorducto: { id: "" },
            ide: -1,
            ide2: 0,
            x: ref(0),
            mensajeError: ''
        };
    },
    methods: {
        //añadir un producto
        AddProducto() {
            //primero se verifica si Productos esta vacio. 
            if(this.Productos.length === 0){
                if ( this.newProducto.Nombre != '' && this.newProducto.Descripcion != '') {

                    const nuevoProducto = {
                    id: 1,
                    nombre: this.newProducto.Nombre,
                    Desc: this.newProducto.Descripcion
                    
                };

                this.Productos.push(nuevoProducto);
                this.newProducto.Nombre = "";
                this.newProducto.Descripcion = "";
                }else{
                    this.mensajeError = "Ningún campo puede estár vacío ";
                    
                }
                
            }else{
                let arr = this.Productos[this.Productos.length -1];
                console.log('arr',arr);
                let lastID = arr.id+1; 
                console.log(this.newProducto, 'nuevo', this.newProducto.id);

                if ( this.newProducto.Nombre != '' && this.newProducto.Descripcion != '') {
                    const nuevoProducto = {
                    id: lastID,
                    nombre: this.newProducto.Nombre,
                    Desc: this.newProducto.Descripcion
                    
                };
                console.log(nuevoProducto);
                this.Productos.push(nuevoProducto);

                this.newProducto.Nombre = "";
                this.newProducto.Descripcion = "";
                }else{
                    this.mensajeError = "Ningún campo puede estár vacío";
                    console.log('ll0', this.newProducto.id, this.newProducto.Nombre, this.newProducto.Descripcion);
                }
            }
        },
        DeleteProducto(productId) {  
            // Buscar en el arreglo
            const index = this.Productos.findIndex(producto => producto.id === productId);

            // Si se encontró el producto, mostrar un mensaje
            if (index !== -1) {
                const confirmacion = window.confirm("¿Seguro deseas eliminar este producto?");

                if (confirmacion) { 
                    // Si el usuario confirma, eliminar el producto del arreglo 
                    this.Productos.splice(index, 1);   
                } 
            } 
        },
        UupdateProducto() { 
            if (this.newProducto.Id != '' && this.newProducto.Nombre != '' && this.newProducto.Descripcion != '') {
                const prodact = {
                    id: this.newProducto.Id,
                    nombre: this.newProducto.Nombre,
                    Desc: this.newProducto.Descripcion
                }

                const newProductId = this.newProducto.Id;
                const productoExiste = this.Productos.findIndex(product => product.id === newProductId); // Se busca si el Id existe

                if (productoExiste === -1 || newProductId==this.Productos[this.ide2].id) {           //Si no existe se agrega el producto
                    this.Productos[this.ide2] = prodact;

                    // this.ordenarProductos;

                    //se limpian los campos
                    this.newProducto.Id = "";
                    this.newProducto.Nombre = "";
                    this.newProducto.Descripcion = "";
                    this.mensajeError = '';
                } else {        //Si existe se muestra el mensaje
                    this.mensajeError = "Un producto con este id ya existe";
                }
            }else{
                this.mensajeError = "Ningún campo puede estar vacío";
            }
        },
        
        llenar(ide) {
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

/*Estilos para la animacion del banner*/
.BGAN:hover {
    transition: 5s background-color ease;
}

.gray-bg,
.blue-bg {
    background-color: hsl(0, 0%, 35%);
    background-image: url(~@/assets/BGIm01.jpg);
    background-size: cover;
    background-position: 0cm;
    transition: background-color 5s ease;
}

.blue-bg {
    background-color: hsla(209, 100%, 50%, 0.575);
}

.hiddenA-text {
    color: hsla(0, 0%, 0%, 0);
    text-align: center;
    font-weight: bold;
    font-size: 10px;
    transition: color 2s ease, font-size 5s ease;
}

.hiddenB-text {
    color: hsla(0, 0%, 0%, 0);
    text-align: right;
    font-size: 100px;
    transition: color 2s ease, font-size 5s ease;
}

.visible-text {
    color: hsl(0, 0%, 100%);
    font-weight: bold;
    font-size: 35px;
    transition: color 5s ease, font-size 5s ease;
    text-align: center;
}

.header {
    margin-top: 0;
    padding-top: 0;
}

/*Estilos para el texto*/

.TxtBlancoB {
    color: hsl(0, 0%, 100%);
    font-weight: bold;
    font-size: 12px;
}

.TxtBlancoN {
    color: hsl(0, 0%, 100%);
    font-size: 12px;
}

input::placeholder {
    color: hsl(0, 0%, 100%);
    font-size: 12px;
}

/*Estilos para el color de fondo de la ventana modal*/
.BGVtnModalFade {
    Background-color: #36363686;
}

.BGVtnModalPrincipal {
    Background-color: #3a3a3a;
}

.BGTextHolder {
    Background-color: #464646;
}

/*Estilos para los Botones*/


/*Boton Master-Class*/
.BotonP{
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;    
    transition: background-color 0.6s ease;  
    position: relative;
    overflow: hidden;
    text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.9);
}

/*Animacion del Boton*/
.BotonP::before {
    content: "";
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent); 
    transition: left 0.3s;     
}

.BotonP:hover::before {
    left: 100%;
}

.BotonP:hover {
    background-color: #666666; 
}

/*Fondos para los Botones*/

.BotonAgregar{
    background-color: rgb(0, 88, 100);
}

.BotonConfirmacion{
background-color: rgb(0, 100, 0);
}

.BotonAviso{
    background-color: rgb(255, 209, 58);    
}


.BotonEliminar{
    background-color: rgb(255, 50, 50);
}
</style>

  