<template>
    <ul>
        <li v-for="country in countries" :key="country">
            <NuxtLink :to="{name:'flag-title',params:{title:country.name.common}}">{{ country.name.common }}</NuxtLink>
            <img class="flag" :src="country.flags.png" :alt="country.flags.alt">
        </li>
    </ul>
</template>
<script setup>
const countries=ref([]);
const getCountries = async () => {
    const url =  'https://restcountries.com/v3.1/all'
    const response = await fetch(url);
    countries.value = await response.json();
  }
  getCountries();
</script>
<style scoped>
.flag {
    display: block;
    width: 20%;
    height: auto;
  }
</style>
