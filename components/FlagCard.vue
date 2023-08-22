<script setup>
const props = defineProps({
    country: Object,
})

</script>
<template>
     <NuxtLink  :to="{name:'flag-iata',params:{iata:country.cca2}}">
            <div class="group relative h-[10.5rem] transform overflow-hidden rounded-4xl clip">
                        <div class="absolute inset-0 bg-indigo-50 " >
                            <img fetchpriority="high"  decoding="async" :alt="country.flags.alt"
                                 data-nimg="1"
                                 class="absolute inset-0 h-full w-full object-cover transition duration-300 group-hover:scale-110 border"
                                 style="color:transparent"
                                 sizes="(min-width: 1280px) 17.5rem, (min-width: 1024px) 25vw, (min-width: 768px) 33vw, (min-width: 640px) 50vw, 100vw"
                                 :srcset="country.flags.svg"
                                 :src="country.flags.svg">
                        </div>
                </div>

    <h3 class="mt-8 font-display text-xl font-bold tracking-tight text-slate-900">{{ country.name.common}}</h3>
    <p class="mt-1 text-base tracking-tight text-slate-500"> {{ country.name.common}}</p>
</NuxtLink>
</template>

<style>
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