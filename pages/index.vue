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
          <a href="#" class="a-button-buy-again">Add a new product</a>
          <a href="#" class="a-button-history margin-right-10"
            >Add a new category</a
          >
          <a href="#" class="a-button-history margin-right-10"
            >Add a new owner</a
          >
        </div>
      </div>
    </div>

    <div class="a-spacing-large"></div>

    <!-- Listing Page -->
    <div class="container-fluid browsing-history">
      <div class="row">
        <div class="col-xs-2 col-lg-2 col-md-3 col-sm-6 br bb">
          <div class="history-box text-center">
            <!-- Product Image -->
            <a href="#" class="a-link-normal">
              <img src="#" alt="img-fluid" />
            </a>

            <div class="spacing-top-base asin-title">
              <span class="a-text-normal">
                <div class="p13n-sc-truncated">Product Title</div>
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
                <span class="p13n-sc-price">$23</span>
              </span>
            </div>

            <!-- Product Actions -->
            <div class="a-row">
              <a href="" class="a-button-history margin-right-10">Update</a>
              <a href="" class="a-button-history margin-right-10">Delete</a>
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
};
</script>
