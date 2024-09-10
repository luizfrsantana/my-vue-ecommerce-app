<template>
  <div id="app">
    <Banner />

    <div class="content">
      <Sidebar clas
        @filterChange="handleFilterChange"
        @sortChange="handleSortChange"
        @productPage="handleProductPage"
        @cartPage="handleCartPage"
        @homePage="handleHomePage"
      />
      <div v-if="currentPage === 'Home'">
        <img src="./assets/img/home.jpg" alt="Home" />
      </div>

      <div class="main-content" v-if="currentPage !== 'Home'">
        
      <ProductPage 
          :productId="products.length + 1"
          :addingNewProduct="addingNewProduct"
        />
      <div class="productlist">


        <Product
          v-for="product in filteredProducts"
          :key="product.id"
          :id="product.id"
          :name="product.name"
          :img="product.img"
          :category="product.category"
          :quantity="product.quantity"
          :price="product.price"
          :rating="product.rating"
          :date="product.date"
          :isInCart="isProductInCart(product.id)"
          @addToCart="addToCart(product, product.price)"
          @removeFromCart="removeFromCart(product.id, product.price)"
          :isCartPage="currentPage === 'cart'"
        />
      </div>
      <div v-if="currentPage === 'cart'">
          <h1>Cart Total Value: {{ cartTotalValue }}</h1>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import Banner from "./components/Banner.vue"
import Sidebar from "./components/Sidebar.vue";
import Product from "./components/Product.vue";
import ProductPage from "./components/ProductPage.vue";

export default {
  components: {
    Banner,
    Sidebar,
    Product,
    ProductPage,
  },
  setup() {
    const products = ref([]);
    const cart = ref([]);
    const cartTotalValue = ref(0);
    const filteredProducts = ref([]);
    const currentPage = ref("");

    const handleProductPage = () => {
      filteredProducts.value = products.value;
      currentPage.value = "ProductPage";
    };

    

    const handleCartPage = () => {
      console.log({ cartTotalValue: cartTotalValue.value });
      filteredProducts.value = cart.value;
      currentPage.value = "cart";
    };

    const handleHomePage = () => {
      filteredProducts.value = [];
      currentPage.value = "Home";
    };

    const addingNewProduct = (product) => {
      const updatedProducts = [...products.value, product];
      products.value = updatedProducts;
      filteredProducts.value = updatedProducts;
    };

    const handleFilterChange = (filter, value) => {
      const itemsToFilter = currentPage.value === "cart" ? cart.value : products.value;
      const filtered = itemsToFilter.filter((product) =>
        String(product[filter])
          .toLowerCase()
          .includes(String(value).toLowerCase())
      );
      filteredProducts.value = filtered;
    };

    const handleSortChange = (sortBy, order) => {
      const sorted = [...filteredProducts.value].sort((a, b) => {
        const compareA = a[sortBy];
        const compareB = b[sortBy];
        if (order === "asc") {
          return compareA > compareB ? 1 : -1;
        } else {
          return compareA < compareB ? 1 : -1;
        }
      });
      filteredProducts.value = sorted;
    };

    const addToCart = (product, price) => {
      cart.value.push(product);
      cartTotalValue.value += price;
    };

    const removeFromCart = (productId, price) => {
      cart.value = cart.value.filter((product) => product.id !== productId);
      cartTotalValue.value -= price;
    };

    const isProductInCart = (productId) => {
      return cart.value.some((product) => product.id === productId);
    };

    onMounted(() => {
      //asdada
    });


    return {
      products,
      cart,
      cartTotalValue,
      filteredProducts,
      currentPage,
      handleProductPage,
      handleCartPage,
      handleHomePage,
      addingNewProduct,
      handleFilterChange,
      handleSortChange,
      addToCart,
      removeFromCart,
      isProductInCart,
    };
  },
};
</script>

<style scoped>
  .App {
    text-align: center;
  }

  .App-logo {
    height: 40vmin;
    pointer-events: none;
  }

  .App-header {
    background-color: #282c34;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: calc(10px + 2vmin);
    color: white;
  }

  .App-link {
    color: #61dafb;
  }

  .content {
    display: flex;
    flex-direction: row;
    width: 100%;
  }

  .sidebar {
  width: 200px;
  padding: 20px;
  border-right: 1px solid #ccc;
  flex-shrink: 0;
}

.main-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 20px;
}

  .productlist {
    flex: 1;
    padding: 20px;
    display: block; 
  }


  .sidebar {
  width: 200px;
  padding: 20px;
  border-right: 1px solid #ccc;
  flex-shrink: 0; 
}
</style>
