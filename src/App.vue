<template>
  <div class="containter">


    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
      <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
          <tr>
            <th scope="col" class="px-6 py-3">
              SKU ID
            </th>
            <th scope="col" class="px-6 py-3">
              Brand
            </th>
            <th scope="col" class="px-6 py-3">
              Description
            </th>
            <th scope="col" class="px-6 py-3">
              Category
            </th>
            <th scope="col" class="px-6 py-3">
              Price
            </th>
            <th scope="col" class="px-6 py-3">
              Discount(%)
            </th>
            <th scope="col" class="px-6 py-3">
              Rating
            </th>
            <th scope="col" class="px-6 py-3">
              Return Policy
            </th>
            <th scope="col" class="px-6 py-3">
              Reviews
            </th>
          </tr>
        </thead>
        <tbody>
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 border-gray-200 hover:bg-gray-50 dark:hover:bg-gray-600"
          v-for="(product, index) in productList[0]">
            <td class="px-6 py-4">
              {{ product.sku }}
            </td>
            <td class="px-6 py-4">
              {{ product.brand }}
            </td>
            <td class="px-6 py-4">
              {{ product.description }}
            </td>
            <td class="px-6 py-4">
              {{ product.category }}
            </td>
            <td class="px-6 py-4">
              {{ product.price }}
            </td>
            <td class="px-6 py-4">
              {{ product.discountPercentage }}
            </td>
            <td class="px-6 py-4">
              {{ product.rating }}
            </td>
            <td class="px-6 py-4">
              {{ product.returnPolicy }}
            </td>
            <td class="px-6 py-4">
              <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Reviews</a>
            </td>
          </tr>

        </tbody>
      </table>
      <NavBar />
    </div>

  </div>
</template>

<script>
import { data } from 'autoprefixer';
import NavBar from './components/NavBar.vue';
export default{
  components : {
    NavBar
  },
  mounted(){
    this.getAllProductsData().then(data =>{
      this.productList = data;
      console.log(this.productList);
    })
  },
  data(){
    return{
      data : [],
      productList : []
    }
  },
  methods: {
    async getAllProductsData(){
      try {
        const res = await fetch('https://dummyjson.com/products')
        const data = await res.json()
        console.log(data.products);
        let result = this.chunkArray(data.products)
        return result
      } catch (err) {
        console.log(err)
      }
    },
    async chunkArray(products) {
      let result = [];
      for (let i = 0; i < products.length; i += 5) {
          result.push(products.slice(i, i + 5));
      }
      console.log(result);
      return result;
    }
  }
}
</script>


<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
