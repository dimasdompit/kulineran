<template>
  <div class="hero">
    <!-- DESKTOP -->
    <div class="d-none d-md-block">
      <div class="row mt-5">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong><br />in Your Gadget
              </h2>
              <p>Come on, choose and order your favorite food.</p>
              <router-link class="btn btn-lg btn-success" to="/foods">
                <b-icon-arrow-right class="mr-2" />Order
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/hero.png" alt="Hero-Image" width="100%" />
        </div>
      </div>
    </div>

    <!-- MOBILE -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-5">
        <div class="col-md-6">
          <img src="../assets/images/hero.png" alt="Hero-Image" width="100%" />
        </div>
        <div class="col-md-6 mt-4">
          <div class="d-flex w-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong><br />in Your Gadget
              </h2>
              <p>Come on, choose and order your favorite food.</p>
              <router-link class="btn btn-lg btn-success" to="/foods">
                <b-icon-arrow-right class="mr-2" />Order
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Hero'
}
</script>

<style></style>
