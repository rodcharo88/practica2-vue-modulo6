<template>
    <div class="container">

        <div class="row">
            <h3>{{ dataProduct.nombre }}</h3>
        </div>
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 ">
                <img :src="dataProduct.imagen" :alt="`image-${ dataProduct.id }`" class="w-100">
            </div>
            <div class="col-12 col-sm-6  col-md-8">
                <h6>{{ dataProduct.descripcion }}</h6>
                <div class="p-3 mb-2 text-white" :style="stylePrice">
                    Precio: {{ dataProduct.precio }} BOB
                </div>
                <h5>Color</h5>
                <div>
                    <div class="color-box clic" @click="colorStorage(color)" v-for="color in dataProduct.colores" :key="color" :style="{ background: color }"></div>
                </div>
                <h5>Cantidad</h5>
                <div class="quantity">
                    <button @click="decrease">-</button> <div>{{ cantidad }}</div> <button @click="add">+</button>
                </div>
                <div class="buy-box">
                    <button type="button" class="btn btn-primary" :class="verify(cantidad, color) ? 'disabled' : ''" @click="comprar">Comprar</button>
                </div>

            </div>
        </div>
</div>
</template>
<script>
export default {
    name: 'ProductComponent',
    props: {
        dataProduct: {},
        stylePrice: {}
    },
    data() {
        return {
            productId: 0,
            cantidad:0,
            color: ""
        }
    },
    methods: {
        add() {
            return this.cantidad ++;
        },
        decrease() {
            if (this.cantidad > 0) {
                return this.cantidad --;
            }
        },
        colorStorage(color) {
            console.log(color);   
            return this.color = color;
        },
        verify(cantidad, color) {
            console.log(cantidad, color)
            if(this.cantidad <= 0 || this.color == "") {
                return true
            }
            return false;
        },
        comprar() {
            alert(`Id = ${ this.dataProduct.id } \nCantidad = ${ this.cantidad } \nColor = ${ this.color }`)
        }
    }
}
</script>