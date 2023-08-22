<script setup>
const props=defineProps({
    countries:Array
})
</script>

<template>
    <div class=" grid grid-cols-1 gap-x-8 gap-y-10 sm:grid-cols-2 sm:gap-y-16 md:grid-cols-6 [&amp;:not(:focus-visible)]:focus:outline-none">
        <div v-for="(country,index) in countries" :key="index" class="clip shadow hover:shadow-lg">

            <FlagCard :country="country"/>
        </div>
    </div>
</template>


<style scoped lang="postcss">
border {
    border-width: 1px;
}

.clip{
    border: 1px solid;
    border-top-right-radius: 50px !important;
    border-top-left-radius: 50px !important;
    border-radius: 15px;
    text-align: center;
}

</style>