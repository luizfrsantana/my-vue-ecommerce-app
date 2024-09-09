<template>
    <div>
      <label for="displayForm">New Product?</label>
      <input type="checkbox" v-model="statusForm" @change="handlerDisplayForm" />
  
      <section class="form" :style="{ display: displayForm }">
        <form @submit.prevent="handleSubmit">
          <input
            type="text"
            v-model="name"
            placeholder="Product Name"
            required
          />
          <input
            type="text"
            v-model="img"
            placeholder="Product Image URL"
            required
          />
  
          <DropDownList
            :itens="productCategories"
            :value="category"
            @updateValue="(value) => category = value"
          />
  
          <label for="price"> Price: </label>
          <input
            type="number"
            name="price"
            v-model="price"
            placeholder="Price"
            min="0"
            max="999999"
            step="0.01"
            required
          />
  
          <label for="quantity"> Quantity: </label>
          <input
            type="number"
            name="quantity"
            v-model="quantity"
            placeholder="Quantity"
            min="0"
            required
          />
  
          <label for="rating"> Rating: </label>
          <input
            type="number"
            name="rating"
            v-model="rating"
            placeholder="Rating"
            min="0"
            max="5"
            required
          />
  
          <label for="dateListed"> Date listed: </label>
          <input
            type="date"
            name="dateListed"
            v-model="formattedDate"
            @change="updateDate"
            required
          />
          <br />
          <button type="submit">Add Product</button>
        </form>
      </section>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  import DropDownList from './DropDownList.vue';
  
  export default {
    components: {
      DropDownList
    },
    props: {
      productId: Number,
      addingNewProduct: Function
    },
    setup(props) {
      const name = ref('');
      const img = ref('');
      const category = ref('');
      const price = ref(0.0);
      const quantity = ref(0);
      const rating = ref(0);
      const date = ref(new Date());
      const statusForm = ref(false);
      const displayForm = ref('none');
      
      const productCategories = ref([
        "Electronics",
        "Clothing",
        "Books",
        "Home & Kitchen",
        "Sports & Outdoors",
      ]);
  
      const formattedDate = ref(date.value.toISOString().split("T")[0]);
  
      const handleSubmit = () => {
        const product = {
          id: props.productId,
          name: name.value,
          img: img.value,
          category: category.value,
          price: price.value,
          quantity: quantity.value,
          rating: rating.value,
          date: date.value,
        };
        props.addingNewProduct(product);
        console.log(produts)
      };
  
      const handlerDisplayForm = () => {
        displayForm.value = statusForm.value ? 'block' : 'none';
      };
  
      const updateDate = (event) => {
        date.value = new Date(event.target.value);
      };
  
      return {
        name,
        img,
        category,
        price,
        quantity,
        rating,
        date,
        statusForm,
        displayForm,
        productCategories,
        handleSubmit,
        handlerDisplayForm,
        formattedDate,
        updateDate,
      };
    }
  };
  </script>
  
  <style scoped>
  </style>