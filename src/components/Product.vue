<template>
    <div class="product">
      <div class="header">
        <img :src="img" :alt="name" />
      </div>
      <div class="footer">
        <h4>{{ name }}</h4>
        <h5>Category: {{ category }}</h5>
        <h5>Price: {{ price }}</h5>
        <h5>Rating: 
          <div v-for="star in renderRating()" :key="star" class="star-container">
            <img class="star" src="../assets/img/star.png" alt="Star" />
          </div>
        </h5>
        <button @click="handleButtonClick">
          {{ isInCart ? 'Remove from Cart' : 'Add to Cart' }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Product",
    props: {
      id: {
        type: Number,
        required: true,
      },
      name: {
        type: String,
        required: true,
      },
      img: {
        type: String,
        required: true,
      },
      category: {
        type: String,
        required: true,
      },
      price: {
        type: Number,
        required: true,
      },
      quantity: {
        type: Number,
        required: true,
      },
      rating: {
        type: Number,
        required: true,
      },
      date: {
        type: String,
        required: true,
      },
      isInCart: {
        type: Boolean,
        required: true,
      },
      onAddToCart: {
        type: Function,
        required: true,
      },
      onRemoveFromCart: {
        type: Function,
        required: true,
      },
      isCartPage: {
        type: Boolean,
        required: true,
      },
    },
    methods: {
      handleButtonClick() {
        if (this.isInCart) {
          this.onRemoveFromCart(this.id);
        } else {
          this.onAddToCart({
            id: this.id,
            name: this.name,
            img: this.img,
            category: this.category,
            quantity: this.quantity,
            price: this.price,
            rating: this.rating,
            date: this.date,
          });
        }
      },
      renderRating() {
        return Array.from({ length: this.rating }, (_, index) => index + 1);
      },
    },
  };
  </script>
  
  <style scoped>
    .product {
        display: inline-block;
        width: 280px;
    }

    .product .header {
        background-color:  #efa040;
        border-radius: 10px 10px 0px 0px;
    }
    .product img {
        width: 250px;
    }

    .product .footer {
        background: #e9f3b08e;
        box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.08);
        border-radius: 0px 0px 10px 10px;
        padding-top: 15px;
        padding-bottom: 5px;
    }

    .product .footer h4 {
        color: #6278F7;
        font-size: 18px;
        line-height: 22px;
        font-weight: bold;
        margin-bottom: 4px;
    }

    .product .footer h5 {
        font-size: 18px;
        line-height: 22px;
        color: #212121;
        padding: 0 8px;
    }


    .product .star {
        display: inline-block;
        width: 20px; 
        height: 20px; 
        margin-right: 2px;
    }
  </style>
  