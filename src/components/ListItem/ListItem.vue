<template>
  <div 
    id="wrapper">
    <ListItemNav/>
    <ul  
      class="listItemUl">
      <li
        v-for="(item, index) in items"  
        :key="index"  
      >
        <div 
          id="list-item-container">
          <list-item-image 
            :image="item.photos[0].url"/>
          <list-item-content 
            :item="item"
            :name="item.name" 
            :description="item.description" 
            :price="item.price"/>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import ListItemNav from './ListItemNav.vue';
import ListItemImage from './ListItemImage';
import ListItemContent from './ListItemContent';

export default {
  name: 'ListItem',
  components: {
    ListItemNav,
    ListItemImage,
    ListItemContent,
  },
  data: function() {
    if (this.$store.state.menuSelected == 'Food') {
      return {
        items: this.$store.state.foodOptions,
        menuTitle: this.$store.state.menuSelected,
      };
    } else if (this.$store.state.menuSelected == 'Drinks') {
      return {
        items: this.$store.state.drinksOptions,
        menuTitle: this.$store.state.menuSelected,
      };
    } else if (
      this.$store.state.menuSelected == 'Desserts'
    ) {
      return {
        items: this.$store.state.dessertsOptions,
        menuTitle: this.$store.state.menuSelected,
      };
    }
  },
  beforeCreate() {
    if (!this.$store.state.customer.id) {
      this.$router.push('/');
    }
  },
  methods: {
    goCheckout() {
      this.$router.push('/Cart');
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
#list-item-container {
  display: flex;
  position: relative;
  text-align: center;
  margin: 0 auto;
  width: 95%;
}
.listItemUl {
  overflow: scroll;
  margin-top: 12px;
  height: 1000px;
}
</style>
