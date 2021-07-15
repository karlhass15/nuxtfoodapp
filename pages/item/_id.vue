<template>
  <main class="container">
    <section 
      class="image" 
      :style="`background: url(/${currentItem.img}) no-repeat center center`"
    ></section>

    <section class="details">
      <h1>{{ currentItem.item }}</h1>
      <h3>{{ currentItem.price.toFixed(2) }}</h3>

      <div class="quantity">
        <input type="number" min="1" v-model="count" />
        <button class="primary">Add to Cart - {{ currentItem.price.toFixed(2) }}</button>
      </div>

      <fieldset v-if="currentItem.addOns">
        <legend>
          <h3>Add Ons</h3>
        </legend>
        <div v-for="addon in currentItem.addOns" :key="addon">
          <input 
            type="checkbox"
            name="addon"
            :id="addon"
            :value="addon"
            v-model="itemAddons"
          />
          <label :for="addon">{{ addon }}</label>
        </div>
      </fieldset>
    </section>  

    <section class="options">
      <h3>Description</h3> 
      <p >{{ currentItem.description }}</p>
    </section>
  </main>

  <!-- {
  "description": "Dumplings filled with pork, crab meat and broth.",
  "item": "Soup Dumplings",
  "img": "dimsum-soup.jpg",
  "id": "3a6da02c-2354-4eb8-af07-f9f2d26fa7c2",
  "price": 9.99,
  "addOns": [
    "mango pudding",
    "none",
    "steamed sesame ball",
    "sweet tofu"
  ]
} -->

 
</template>

<script>
import { mapState } from 'vuex';


export default {
  data() {
    return {
      id: this.$route.params.id,
      count: 1,
      itemOptions: "",
      itemAddons: [],
      itemSizeAndCost: []
    };
  }, 
  computed: {
    ...mapState(["fooddata"]),
    currentItem() {
      // more efficient than forEach because we can break rather than .filter
      let result;

      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id === this.id) {
            result = this.fooddata[i].menu[j];
            break;
          }
        }
      }
      return result;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 1000px;
  margin: 100px auto;
  display: grid;
  grid-template-columns: 400px 1fr;
  grid-template-rows: 400px 1fr;
  grid-column-gap: 60px;
  grid-row-gap: 60px;
  line-height: 2;
}

.image {
  grid-area: 1 / 1 / 2 / 2;
  background-size: cover;
}
.details {
  grid-area: 1 / 2 / 2 / 3;
  position: relative;
}
.options {
  grid-area: 2 / 1 / 3 / 2;
}
</style>