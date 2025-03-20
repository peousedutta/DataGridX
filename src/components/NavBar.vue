<template>
    <div>
        <nav class="flex items-center flex-column flex-wrap md:flex-row justify-between pt-4"
            aria-label="Table navigation">
            
            <ul class="inline-flex -space-x-px rtl:space-x-reverse text-sm h-8">
                <li>
                    <div class="flex items-center justify-center px-3 h-8">Pages -></div> 
                </li>
                <li v-for="(listNumber, index) in dataStreamLength - 1" :key="index">
                    <a 
                        href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
                        @click="sendPageIndex(listNumber)"
                        >
                        {{ listNumber }}</a>
                </li>
                <!-- <li>
                    <a href="#" aria-current="page"
                        class="flex items-center justify-center px-3 h-8 text-blue-600 border border-gray-300 bg-blue-50 hover:bg-blue-100 hover:text-blue-700 dark:border-gray-700 dark:bg-gray-700 dark:text-white">3</a>
                </li> -->
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
    props : {
        dataStreamLength: Number
    },
    methods: {
        sendPageIndex(index){
            this.$emit("pageIndex", index)
        }
    },
}
</script>