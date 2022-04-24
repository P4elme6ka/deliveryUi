<template>
  <div class="columns is-centered is-multiline cont">
    <div class="card column is-one-quarter" v-for="product in products" :key="product.Id">
      <VmProducts :product="product"></VmProducts>
    </div>
    <div class="section" v-if="products.length === 0">
      <p>{{ noProductLabel }}</p>
    </div>
  </div>
</template>

<script>
import VmProducts from '../Products';
import { getByTitle } from '@/assets/filters';

export default {
  name: 'productsList',

  components: { VmProducts },

  data () {
    return {
      id: '',
      noProductLabel: 'No product found',
      productsFiltered: []
    };
  },

  computed: {
    products () {
      if (this.$store.state.userInfo.hasSearched) {
        return this.getProductByTitle();
      } else {
        return this.$store.state.products;
      }
    }
  },

  methods: {
    getProductByTitle () {
      let listOfProducts = this.$store.state.products,
          titleSearched = this.$store.state.userInfo.productTitleSearched;

      return this.productsFiltered = getByTitle(listOfProducts, titleSearched);
    }
  }

};
</script>

<style lang="scss" scoped>
  .card {
    margin: 10px;
    border: 1px lightgray solid;
    -webkit-box-shadow: 4px 4px 9px 0 rgba(34, 60, 80, 0.31);
    -moz-box-shadow: 4px 4px 9px 0 rgba(34, 60, 80, 0.31);
    box-shadow: 4px 4px 9px 0 rgba(34, 60, 80, 0.31);
  }
  .cont{
    margin-top: 10px;
    margin-bottom: 10px;
  }
</style>
