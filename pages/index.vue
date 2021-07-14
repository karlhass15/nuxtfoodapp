<template>
  <main class="conatiner">
    <AppHeader />
    <AppRestaurantInfo />
  </main>
</template>

<script>
import AppHeader from '@/components/AppHeader.vue';
import AppRestaurantInfo from '@/components/AppRestaurantInfo.vue';

export default {
  components: {
    AppRestaurantInfo,
    AppHeader
  },
};

</script>
