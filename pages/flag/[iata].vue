<template>
    <div v-if="!!country" class="container text-center text-xl flex justify-center flex-wrap gap-3">
        <h1 class="basis-full
        ">
            Country :
            {{ country.name.common }}
        </h1>
        <div>
            <div>
                <div class="">
                    <div>
                        <div>
                            <img fetchpriority="high" decoding="async" :alt="country.flags.alt" data-nimg="1" class=""
                                style="color:transparent"
                                sizes="(min-width: 1280px) 17.5rem, (min-width: 1024px) 25vw, (min-width: 768px) 33vw, (min-width: 640px) 50vw, 100vw"
                                :srcset="country.flags.svg" :src="country.flags.svg">
                        </div>
                    </div>
                </div>

            </div>

            <h2>
                borders
            </h2>

            <div
                class=" grid grid-cols-1 gap-x-8 gap-y-10 sm:grid-cols-2 sm:gap-y-16 md:grid-cols-3 [&amp;:not(:focus-visible)]:focus:outline-none">
                <div v-for="(border, index) in borders" :key="index" class="clip shadow hover:shadow-lg">
                    <NuxtLink :to="{ name: 'flag-iata', params: { iata: border.cca2 } }">
                        <div class="group relative h-[10.5rem] transform overflow-hidden rounded-4xl clip">
                            <div class="absolute inset-0 bg-indigo-50 ">
                                <img fetchpriority="high" decoding="async" :alt="border.flags.alt" data-nimg="1"
                                    class="absolute inset-0 h-full w-full object-cover transition duration-300 group-hover:scale-110 border"
                                    style="color:transparent"
                                    sizes="(min-width: 1280px) 17.5rem, (min-width: 1024px) 25vw, (min-width: 768px) 33vw, (min-width: 640px) 50vw, 100vw"
                                    :srcset="border.flags.svg" :src="border.flags.svg">
                            </div>
                        </div>

                        <h3 class="mt-8 font-display text-xl font-bold tracking-tight text-slate-900">{{
                            border.name.common }}</h3>
                        <p class="mt-1 text-base tracking-tight text-slate-500"> {{ border.name.common }}</p>
                    </NuxtLink>
                </div>
            </div>

            <!-- {{ border.name.common }} -->
        </div>
    </div>
</template>

<script setup>

const route = useRoute().params.iata;
const country = ref();
const borders = ref([])


const getApiCountry = async (route) => {
    debugger;
    const url = `https://restcountries.com/v3.1/alpha/${route}`
    const response = await fetch(url);
    const countries = await response.json();
    country.value = countries[0];

    if (!!country.value.borders) {
        const borderCodes = country.value.borders.join(',');
        const url = `https://restcountries.com/v3.1/alpha?codes=${borderCodes}`
        const response = await fetch(url);
        borders.value = await response.json();
    }
    console.log("selectedCountry==>", country.value);
}

getApiCountry(route);

</script>

<style>
h1{
    font-size: 22px;
    text-align: center;
    border-bottom: 5px double #333;
    margin: 10px;
    color: green;
    font-weight: bold;
}
h2{
    font-size: 20px;
    text-align: center;
    border-bottom: 5px double #333;
    margin: 10px;
    color: green;
    font-weight: bold;
}
border {
    border-width: 1px;
}
      .rounded-4xl {
          border-radius: 3rem;
      }
      .duration-300 {
          transition-duration: .3s;
      }
      .bg-indigo-50 {
          --tw-bg-opacity: 1;
          background-color: rgb(238 242 255/var(--tw-bg-opacity));
      }
.clip{
    border: 1px solid;
    border-top-right-radius: 50px !important;
    border-top-left-radius: 50px !important;
    border-radius: 15px;
    text-align: center;
}
</style>