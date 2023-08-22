<template>
    <div class="container m-auto">
    <div class="lg:col-span-6">
        <flag-cards :countries="countries"/>
    </div>
</div>
</template>

<script setup>

const countries=ref([]);

const getApicountries = async (query) => {
    const url = query ? `https://restcountries.com/v3.1/name/${query}` : `https://restcountries.com/v3.1/all`
    const response = await fetch(url);
    countries.value = await response.json();
  }
  getApicountries()
</script>

<style scoped></style>