<template>
  <main>
    <div class="a-spacing-large"></div>
    <div class="container-fluid browsing-history">
      <div class="row">
        <div class="col-sm-8 col-8">
          <h1 class="a-size-large a-spacing-none a-text-normal">
            All products
          </h1>
          <div class="a-spacing-large"></div>
          <!-- Post Buttons -->
          <nuxt-link to="/products" class="a-button-buy-again"
            >Add a new product</nuxt-link
          >
          <nuxt-link to="/category" class="a-button-history margin-right-10"
            >Add a new category</nuxt-link
          >
          <nuxt-link to="/owner" class="a-button-history margin-right-10"
            >Add a new owner</nuxt-link
          >
        </div>
      </div>
    </div>

    <div class="a-spacing-large"></div>

    <!-- Listing Page -->
    <div class="container-fluid browsing-history">
      <div class="row">
        <div
          v-for="(product, index) in products"
          :key="product._id"
          class="col-xs-2 col-lg-2 col-md-3 col-sm-6 br bb"
        >
          <div class="history-box text-center">
            <!-- Product Image -->
            <a href="#" class="a-link-normal">
              <img
                :src="product.photo"
                alt="img-fluid"
                style="object-fit: cover"
                width="140"
              />
            </a>

            <div class="spacing-top-base asin-title">
              <span class="a-text-normal">
                <div class="p13n-sc-truncated">{{ product.title }}</div>
              </span>
            </div>

            <!-- Product Rating -->
            <div class="a-row">
              <a href="#">
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
              </a>
              <span class="a-letter-space"></span>
              <span class="a-color-tertiary a-size-small asin-reviews"
                >(1732)</span
              >
            </div>

            <!-- Product Price -->
            <div class="a-row">
              <span class="a-size-base a-color-price">
                <span class="p13n-sc-price">${{ product.price }}</span>
              </span>
            </div>

            <!-- Product Actions -->
            <div class="a-row">
              <nuxt-link
                :to="`/products/${product._id}`"
                class="a-button-history margin-right-10"
                >Update</nuxt-link
              >
              <button
                class="a-button-history margin-right-10"
                @click="onDeleteProduct(product._id, index)"
              >
                Delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "IndexPage",
  async asyncData({ $axios }) {
    try {
      let response = await $axios.get("http://localhost:3000/api/product");
      return {
        products: response.data.products,
      };
    } catch (err) {
      console.error(err);
    }
  },
  methods: {
    async onDeleteProduct(id, index) {
      try {
        let response = await this.$axios.delete(
          `http://localhost:3000/api/product/${id}`
        );

        if (response.data.success) this.products.splice(index, 1);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
