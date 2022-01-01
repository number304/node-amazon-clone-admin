<template>
  <div class="container-fluid c-section">
    <div class="row">
      <div class="col-sm-3"></div>
      <div class="col-sm-6">
        <div class="a-spacing-top-medium"></div>
        <h2>Add a new owner</h2>
        <form action="">
          <!-- Owner name -->
          <div class="a-spacing-top-medium">
            <label for="">Name</label>
            <input
              type="text"
              class="a-input-text"
              style="width: 100%"
              v-model="name"
            />
          </div>

          <!-- Info about owner -->
          <div class="a-spacing-top-medium">
            <label for="">About</label>
            <input
              type="text"
              class="a-input-text"
              style="width: 100%"
              v-model="about"
            />
          </div>

          <!-- Onwer photo -->
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
                <span class="a-button-text" @click="onAddOwner">Add owner</span>
              </span>
            </span>
          </div>

          <br />

          <ul class="list-group-item">
            <li v-for="owner in owners" :key="owner._id">
              {{ owner.name }}
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
      let response = await $axios.get("http://localhost:3000/api/owner");
      return {
        owners: response.data.owners,
      };
    } catch (err) {
      console.err(err);
    }
  },
  data: () => ({
    name: "",
    about: "",
    selectedFile: null,
    fileName: "",
  }),
  methods: {
    async onAddOwner() {
      try {
        let data = new FormData();
        data.append("name", this.name);
        data.append("about", this.about);
        data.append("photo", this.selectedFile, this.selectedFile.name);

        let response = await this.$axios.post(
          "http://localhost:3000/api/owner",
          data
        );

        console.log(response);
        if (response.data.success) this.$router.push("/");
      } catch (err) {
        console.error(err);
      }
    },
    onFileSelected(event) {
      if (event.target.files[0]) {
        this.selectedFile = event.target.files[0];
        this.fileName = event.target.files[0].name;
      }
    },
  },
};
</script>

<style></style>
