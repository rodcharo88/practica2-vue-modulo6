<template>
    <div class="col-md-4" v-if="dataProductItem.id != itemSelected">
        <div class="relatedProduct" @click="selectedItem(dataProductItem.id)">
            <h5 class="card-title text-center py-3">{{ dataProductItem.nombre }}</h5>
            <img :src="dataProductItem.imagen" :alt="`image-${dataProductItem.id}`" class="w-100">
            <p class="card-text px-3">{{ dataProductItem.descripcion }}</p>
            <div class="producto-relacionado-precio">Precio:{{ dataProductItem.precio }} BOB</div>
            <div>
                <div class="text-center">
                    <div class="color-box" v-for="color in dataProductItem.colores" :key="color" :style="{ background: color }"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    // import ProductComponent from './ProductComponent.vue';
    
    export default {
        name: 'RelatedProductComponent',
        props: {
            dataProductItem: {},
            itemSelected: Number
        },
        methods: {
            selectedItem(id) {
                console.log(id);
                this.$emit('changeProduct', id);
            }
        }
    }
</script>
<style scoped>
.relatedProduct {
    transition: all 300ms;
}

.relatedProduct img {
    height: 400px;
}
.relatedProduct:hover {
    transform: scale(1.03);
    cursor: pointer;
}
</style>