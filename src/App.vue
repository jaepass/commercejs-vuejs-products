<template>
  <div>
    <Hero :merchant="merchant" />
    <ProductsList :products="products"/>
  </div>
</template>

<script>
import Hero from './components/Hero';
import ProductsList from './components/ProductsList';

export default {
  name: 'app',
  components: {
    Hero,
    ProductsList,
  },
  data() {
    return {
      merchant: {},
      products: [],
    }
  },
  created() {
    this.fetchMerchantDetails();
    this.fetchProducts();
  },
  methods: {
    /**
     * Fetch merchant details
     * https://commercejs.com/docs/api/?javascript--cjs#get-merchant-details
     */
    fetchMerchantDetails() {
      this.$commerce.merchants.about().then((merchant) => {
        this.merchant = merchant;
      }).catch((error) => {
        console.log('There was an error fetch the merchant details', error)
      });
    },
    /**
     * Fetch products data from Chec and stores in the products data object.
     * https://commercejs.com/docs/sdk/products
     */
    fetchProducts() {
      this.$commerce.products.list().then((products) => {
        this.products = products.data;
      }).catch((error) => {
        console.log('There is an error fetching products', error);
      });
    },
  },
};
</script>
