<template>
  <main>
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-3"></div>
        <div class="col-sm-6">
          <div class="a-section">
            <div class="a-spacing-top-medium"></div>
            <h2 style="text-align: center">Update {{ product.title }}</h2>
            <form action="">
              <!-- Category dropdown -->
              <div class="a-spacing-top-medium">
                <label for="category-dropdown">Category</label>
                <select
                  name="category-dropdown"
                  id=""
                  class="a-select-option"
                  v-model="categoryID"
                >
                  <option
                    v-for="category in categories"
                    :key="category._id"
                    :value="category._id"
                  >
                    {{ category.type }}
                  </option>
                </select>
              </div>

              <!-- Owner dropdown -->
              <div class="a-spacing-top-medium">
                <label for="owner-dropdown">Owner</label>
                <select
                  name="owner-dropdown"
                  id=""
                  class="a-select-option"
                  v-model="ownerID"
                >
                  <option
                    v-for="owner in owners"
                    :key="owner._id"
                    :value="owner._id"
                  >
                    {{ owner.name }}
                  </option>
                </select>
              </div>

              <!-- Product title -->
              <div class="a-spacing-top-medium">
                <label for="">Title</label>
                <input
                  type="text"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="title"
                  :placeholder="product.title"
                />
              </div>

              <!-- Product price -->
              <div class="a-spacing-top-medium">
                <label for="">Price</label>
                <input
                  type="number"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="price"
                  :placeholder="product.price"
                />
              </div>

              <!-- Product quantity in stock -->
              <div class="a-spacing-top-medium">
                <label for="">Stock Quantity</label>
                <input
                  type="number"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="stockQuantity"
                  :placeholder="product.stockQuantity"
                />
              </div>

              <!-- Product description -->
              <div class="a-spacing-top-medium">
                <label for="">Description</label>
                <textarea
                  name=""
                  id=""
                  style="width: 100%"
                  rows="5"
                  :placeholder="product.description"
                  v-model="description"
                ></textarea>
              </div>

              <!-- Product photo -->
              <div class="a-spacing-top-medium">
                <label for="" style="margin-bottom: 0px">Add Photo</label>
                <div class="a-row a-spacing-top-medium">
                  <label for="product-file" class="choosefile-button">
                    <i class="fal fa-plus"></i>
                    <input
                      type="file"
                      name="product-file"
                      id="product-file"
                      @change="onFileSelected"
                    />
                    <p style="margin-top: -70px">{{ fileName }}</p>
                  </label>
                </div>
              </div>

              <hr />

              <div
                style="display: flex; justify-content: space-between"
                class="a-spacing-top-large"
              >
                <!-- Cancel button -->
                <nuxt-link to="/" class="a-button-history margin-right-10"
                  >Cancel</nuxt-link
                >
                <!-- Save button -->
                <span class="a-button-register">
                  <span class="a-button-inner">
                    <span class="a-button-text" @click="onUpdateProduct"
                      >Update product</span
                    >
                  </span>
                </span>
              </div>

              <div style="margin-bottom: 30px"></div>
            </form>
          </div>
        </div>
        <div class="col-sm-3"></div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    try {
      let categories = $axios.get("http://localhost:3000/api/category");
      let owners = $axios.get("http://localhost:3000/api/owner");
      let product = $axios.get(
        `http://localhost:3000/api/product/${params.id}`
      );

      const [categoryResponse, ownerResponse, productResponse] =
        await Promise.all([categories, owners, product]);

      return {
        categories: categoryResponse.data.categories,
        owners: ownerResponse.data.owners,
        product: productResponse.data.product,
      };
    } catch (err) {
      console.error(err);
    }
  },
  created() {
    this.categoryID = this.categories.find(
      (category) => category._id === this.product.category
    )._id;
    this.ownerID = this.owners.find(
      (owner) => owner._id === this.product.owner
    )._id;
  },
  data: () => ({
    categoryID: null,
    ownerID: null,
    title: "",
    price: null,
    description: "",
    selectedFile: null,
    stockQuantity: null,
    fileName: "",
  }),
  methods: {
    onFileSelected(event) {
      if (event.target.files[0]) {
        this.selectedFile = event.target?.files[0];
        console.log(this.selectedFile);
        this.fileName = event.target?.files[0].name;
      }
    },
    async onUpdateProduct() {
      let data = new FormData();
      data.append("title", this.title || this.product.title);
      data.append("price", this.price || this.product.price);
      data.append(
        "stockQuantity",
        this.stockQuantity || this.product.stockQuantity
      );
      data.append("description", this.description || this.product.description);
      data.append("ownerID", this.ownerID || this.product.owner);
      data.append("categoryID", this.categoryID || this.product.category);
      if (this.selectedFile)
        data.append("photo", this.selectedFile, this.selectedFile.name);
      else data.append("photo", this.product.photo);

      let response = await this.$axios.put(
        `http://localhost:3000/api/product/${this.$route.params.id}`,
        data
      );

      console.log(response);

      if (response.data.success) this.$router.push("/");
    },
  },
};
</script>

<style></style>
