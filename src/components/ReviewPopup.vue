<template>
    <div id="popup-modal" tabindex="-1"
        class="overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
        <div class="relative p-4 w-full max-w-md max-h-full">
            <div class="relative bg-white rounded-lg shadow-sm dark:bg-gray-700">
                <button type="button"
                    class="absolute top-3 end-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                    data-modal-hide="popup-modal">
                    <span class="sr-only">Close modal</span>
                </button>
                <div class="p-4 md:p-5 text-center">
                    <h3 class="mb-5 text-lg font-normal text-gray-500 dark:text-gray-400">Check Reviews</h3>
                </div>
                <div v-for="(review, index) in cleanReviewsData" :key="index">\
                    <div>Date : {{ review.date }}</div>
                    <div>Comment : {{ review.comment }}</div>
                    <div>Rating : {{ review.rating }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { list } from 'postcss';


export default{
    props: {
        reviewList: [String, Number],
    },
    data() {
        return {
            cleanReviewsData : []
        }
    },
    mounted(){
        console.log('mounted - ',this.reviewList);
        
        this.resolveReviewsPromise(this.reviewList)
                .then(data => {
                    this.cleanReviewsData = data
                    console.log(data);
                })
    },
    methods:{
        async resolveReviewsPromise(data){return data},
    }

}

</script>