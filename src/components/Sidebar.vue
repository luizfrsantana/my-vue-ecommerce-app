<template>
    <div class="sidebar">
      <span class="link-like" @click="handleHomeClick">Home</span><br />
      <span class="link-like" @click="handleProductClick">Product</span><br />
      <span class="link-like" @click="handleCartClick">Cart</span><br />
  
      <h3>Search Bar</h3>
      <input
        type="text"
        placeholder="Search by name"
        @input="onFilterChange('name', $event.target.value)"
      />
  
      <h3>Filter by:</h3>
      <label for="filterCategory">Category: </label>
      <input
        type="text"
        name="filterCategory"
        @input="onFilterChange('category', $event.target.value)"
      />
  
      <label for="filterPrice">Price:</label>
      <input
        type="number"
        name="filterPrice"
        min="0"
        step="0.01"
        @input="onFilterChange('price', Number($event.target.value))"
      />
  
      <label for="filterQuantity">Quantity: </label>
      <input
        type="number"
        name="filterQuantity"
        min="0"
        @input="onFilterChange('quantity', Number($event.target.value))"
      />
  
      <label for="filterRating">Rating/Stars: </label>
      <input
        type="number"
        name="filterRating"
        min="0"
        max="5"
        @input="onFilterChange('rating', Number($event.target.value))"
      />
  
      <h3>Sort by:</h3>
      <label for="sortPrice">Price: </label>
      <select name="sortPrice" @change="onSortChange('price', $event.target.value)">
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
      <hr />
      <label for="sortQuantity">Quantity: </label>
      <select name="sortQuantity" @change="onSortChange('quantity', $event.target.value)">
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
      <hr />
      <label for="sortRating">Rating/Stars: </label>
      <select name="sortRating" @change="onSortChange('rating', $event.target.value)">
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
      <hr />
      <label for="sortDate">Date Listed/Added: </label>
      <select name="sortDate" @change="onSortChange('date', $event.target.value)">
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
      <hr />
    </div>
  </template>
  
  <script>
  import { useRouter } from 'vue-router';
  
  export default {
    props: {
      onFilterChange: Function,
      onSortChange: Function,
      onHomePage: Function,
      onProductPage: Function,
      onCartPage: Function,
    },
    setup(props) {
       
      const handleHomeClick = () => {
        props.onHomePage();
      };
  
      const handleProductClick = () => {
        props.onProductPage();
      };
  
      const handleCartClick = () => {
        props.onCartPage();
      };
  
      return {
        handleHomeClick,
        handleProductClick,
        handleCartClick,
      };
    },
  };
  </script>
  
  <style scoped>
    .link-like {
        color: blue; 
        text-decoration: underline; 
        cursor: pointer; 
    }

    .link-like:hover {
        color: darkblue; 
        text-decoration: none; 
    }
  </style>
  