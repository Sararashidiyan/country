<template>
    <div v-if="!!selectedCountry">
      {{ selectedCountry.name.common }}
      <img class="flag" :src="selectedCountry.flags.png" :alt="selectedCountry.flags.alt">
      <ul>
        <li v-for="border in borders" :key="border">
          <NuxtLink :to="{name:'flag-title',params:{title:border.name.common}}">{{ border.name.common }}</NuxtLink>

        </li>
      </ul>
    
      <!-- <NuxtLink :to="{name:'flag-title',params:{title:country.name.common}}">{{ country.name.common }}</NuxtLink> -->
       <!-- {{ selectedCountry.name.common }} -->
      <!--<img class="flag" :src="selectedCountry.flags.png" :alt="selectedCountry.flags.alt"> -->
    
    </div>
    <!-- {{ selectedCountry }} -->
</template>
<script setup>
const route=useRoute();
const selectedCountries=ref('');
const selectedCountry=ref('');
const borders=ref([]);

const getSelectedCountry = async (title) => {
    const url =  `https://restcountries.com/v3.1/name/${title}?fullText=true`
    const response = await fetch(url);
    selectedCountries.value = await response.json();
    selectedCountry.value = selectedCountries.value[0];
    
    if(!!selectedCountry.value.borders)
    {
     const borderCodes=selectedCountry.value.borders.join(','); 
      const url =  `https://restcountries.com/v3.1/alpha?codes=${borderCodes}`
    const response = await fetch(url);
    borders.value = await response.json();
    }
     

  }
  
  if(!!route.params.title)
{
    debugger;
    getSelectedCountry(route.params.title);
}

</script>
