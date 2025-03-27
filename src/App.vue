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
          v-for="(product, index) in productList[pageIndex]">
            <td class="px-6 py-4">
              {{ product.sku }}
            </td>
            <td class="px-6 py-4">
              {{ product.brand }}
            </td>
            <td class="px-6 py-4 h-24">
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
          <!-- <ReviewPopup /> -->

        </tbody>
      </table>
      <div id="popup-modal" tabindex="-1" class="hidden overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
    <div class="relative p-4 w-full max-w-md max-h-full">
        <div class="relative bg-white rounded-lg shadow-sm dark:bg-gray-700">
            <button type="button" class="absolute top-3 end-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-hide="popup-modal">
                <span class="sr-only">Close modal</span>
            </button>
            <div class="p-4 md:p-5 text-center">
                <svg class="mx-auto mb-4 text-gray-400 w-12 h-12 dark:text-gray-200" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 11V6m0 8h.01M19 10a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
                </svg>
                <h3 class="mb-5 text-lg font-normal text-gray-500 dark:text-gray-400">Are you sure you want to delete this product?</h3>
                <button data-modal-hide="popup-modal" type="button" class="text-white bg-red-600 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 font-medium rounded-lg text-sm inline-flex items-center px-5 py-2.5 text-center">
                    Yes, I'm sure
                </button>
                <button data-modal-hide="popup-modal" type="button" class="py-2.5 px-5 ms-3 text-sm font-medium text-gray-900 focus:outline-none bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-100 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700">No, cancel</button>
            </div>
        </div>
    </div>
</div>
      <NavBar 
        :dataStreamLength = "dataStreamLength" 
        @pageIndex="getPageIndex"
      />

    </div>

  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import ReviewPopup from './components/ReviewPopup.vue';
export default{
  components : {
    NavBar, ReviewPopup
  },
  mounted(){
    this.getAllProductsData().then(data =>{
      this.productList = data
      this.dataStreamLength = this.productList.length
      console.log(this.dataStreamLength);
    })
  },
  data(){
    return{
      pageIndex: 1,
      dataStreamLength : 1,
      data : [],
      productList : []
    }
  },
  methods: {
    async getAllProductsData(){
      try {
        const res = await fetch('https://dummyjson.com/products')
        console.log(res);
        
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
          result.push(products.slice(i, i + 5))
      }
      console.log(result)
      return result
    },
    getPageIndex(index){
      console.log(index)
      this.pageIndex = index
    }
  }
}
</script>

