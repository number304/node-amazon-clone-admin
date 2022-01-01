<template>
  <div class="container-fluid c-section">
    <div class="row">
      <div class="col-sm-3"></div>
      <div class="col-sm-6">
        <div class="a-spacing-top-medium"></div>
        <h2>Add a new category</h2>
        <form action="">
          <div class="a-spacing-top-medium">
            <label for="">Type</label>
            <input
              type="text"
              class="a-input-text"
              style="width: 100%"
              v-model="type"
            />
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
                <span class="a-button-text" @click="onAddCategory"
                  >Add category</span
                >
              </span>
            </span>
          </div>

          <br />

          <ul class="list-group-item">
            <li v-for="category in categories" :key="category._id">
              {{ category.type }}
            </li>
          </ul>
        </form>
      </div>
      <div class="col-sm-3"></div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      let response = await $axios.get("http://localhost:3000/api/category");
      return {
        categories: response.data.categories,
      };
    } catch (err) {
      console.error(err);
    }
  },
  data: () => ({
    type: "",
  }),
  methods: {
    async onAddCategory() {
      try {
        let data = { type: this.type };
        let response = await this.$axios.post(
          "http://localhost:3000/api/category",
          data
        );

        console.log(response);

        if (response.data.success) this.$router.push("/");
      } catch (err) {
        console.error(err);
      }
    },
  },
};
</script>

<style></style>
