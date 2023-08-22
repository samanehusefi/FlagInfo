<template>
    <div>
        <h1>
            Country :
            {{ selectedCountry.name.common }}
        </h1>
        <div>
            <div
                class=" grid grid-cols-1 gap-x-8 gap-y-10 sm:grid-cols-2 sm:gap-y-16 md:grid-cols-6 [&amp;:not(:focus-visible)]:focus:outline-none">
                <div class="clip shadow hover:shadow-lg">
                    <div class="group relative h-[10.5rem] transform overflow-hidden rounded-4xl clip">
                        <div class="absolute inset-0 bg-indigo-50 ">
                            <img fetchpriority="high" decoding="async" :alt="selectedCountry.flags.alt" data-nimg="1"
                                class="absolute inset-0 h-full w-full object-cover transition duration-300 group-hover:scale-110 border"
                                style="color:transparent"
                                sizes="(min-width: 1280px) 17.5rem, (min-width: 1024px) 25vw, (min-width: 768px) 33vw, (min-width: 640px) 50vw, 100vw"
                                :srcset="selectedCountry.flags.svg" :src="selectedCountry.flags.svg">
                        </div>
                    </div>
                </div>
            </div>
            <div v-for="(country) in borders">
                {{ country.name.common }}
            </div>
        </div>
    </div>
</template>

<script setup>

// const selectedCountry = ref(JSON.parse(localStorage.getItem("SelectedCountry")));


const route = useRoute().params.iata;

const selectedCountry = ref();
const borders = ref([])


const getSelectedCountry = async (route) => {
    const url = `https://restcountries.com/v3.1/cca2/${route}`
    const response = await fetch(url);
    const selectedCountries = await response.json();
    selectedCountry.value = selectedCountries.value[0];

    if (!!selectedCountry.value.borders) {
        const borderCodes = selectedCountry.value.borders.join(',');
        const url = `https://restcountries.com/v3.1/cca2?codes=${borderCodes}`
        const response = await fetch(url);
        borders.value = await response.json();
    }

    getSelectedCountry()
}

</script>

<style lang="scss" scoped></style>