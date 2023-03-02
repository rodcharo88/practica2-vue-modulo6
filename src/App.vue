<template>
  <MenuComponent :data="dataMenu" />
  <ProductComponent :dataProduct="dataProduct" :stylePrice="dataMenu.precioEstilos" />
  
  <div class="container">
      <div class="row">
        <h4>Productos relacionados</h4>
      </div>
      <div class="row">
        <RelatedProductComponent v-on:changeProduct="getProductById" v-for="item in dataProducts" :key="item.id" :dataProductItem="item" :itemSelected="itemSelected" />
      </div>
  </div>

  <FooterComponent :styleFooter="dataMenu" />
</template>

<script>
import MenuComponent from './components/MenuComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import ProductComponent from './components/ProductComponent.vue';
import RelatedProductComponent from './components/RelatedProductComponent.vue';

export default {
  name: 'App',
  components: {
    MenuComponent,
    FooterComponent,
    ProductComponent,
    RelatedProductComponent,
  },
  data() {
    return {
      dataMenu: {},
      dataProducts: [],
      dataProduct: {},
      itemSelected: 1
    }
  },
  methods: {
    async getMenu() {
      const res = await fetch('http://localhost:3000/configuracionPagina');
      const response = await res.json();
      this.dataMenu = response;
    },
    async getProducts() {
      const res = await fetch('http://localhost:3000/producto');
      const response = await res.json();
      this.dataProducts = response;
    },
    async getProductById(id) {
      this.itemSelected = id;
      const res = await fetch(`http://localhost:3000/producto/${id}`);
      const dataProduct = await res.json();
      this.dataProduct = dataProduct;
    }
   
  },
  mounted() {
    this.getMenu();
    this.getProducts();
    this.getProductById(this.itemSelected);
  }
}
</script>

<style>
.color-box {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin: 7px;
  display: inline-block;
  transition: all .3s ease-in;
}

.color-box:hover {
  transform: scale(1.2);
}

.clic {
  cursor: pointer;
}

.quantity button {
  border-radius: 50%;
  display: inline-block;
  width: 30px;
}

.quantity div {
  text-align: center;
  min-width: 30px;
  display: inline-block;
  font-weight: bold;
}

.buy-box {
  margin: 20px;
}

footer {

  text-align: center;
  padding: 30px 10px;
  margin-top: 50px;
  min-height: 100px;
}

.container {
  margin-top: 50px;
}

.producto-relacionado-precio {
  background: orangered;
  color: white;
  text-align: center;
  padding: 10px;
}
</style>
