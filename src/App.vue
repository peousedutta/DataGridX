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
              <button 
                class="font-medium bg-green-300" 
                @click="showReview(product.reviews)">Reviews</button>
            </td>
          </tr>
          <!-- <ReviewPopup /> -->

        </tbody>
      </table>
      <ReviewPopup v-if="showReviewFlag" :reviewList = "reviewList" />
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
      productList : [],
      reviewList : [],
      showReviewFlag : false
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
    },
    showReview(...data){
      this.reviewList.push(data)
      this.showReviewsModal()
      console.log(data);
    },
    showReviewsModal(){
      this.showReviewFlag = true
    }
  }
}
</script>

