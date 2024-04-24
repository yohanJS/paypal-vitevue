<script setup>

</script>

<template>
  <nav class="navbar navbar-expand-md bg-light fixed-top p-0 lg-shadow border-bottom shadow-sm">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">
      <img src="../assets/me2.png" alt="Bootstrap" width="50" height="50">
    </a>
    <button class="navbar-toggler" type="button" aria-label="toggler-icon" data-bs-toggle="offcanvas" data-bs-target="#offcanvasNavbar" aria-controls="offcanvasNavbar">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasNavbar" aria-labelledby="offcanvasNavbarLabel">
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="offcanvasNavbarLabel">
          <img src="../assets/me2.png" alt="Bootstrap" width="50" height="50">
        </h5>
        <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body">
        <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link" href="#services">Services</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#about">About Us</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#footer">Contact Us</a>
          </li> -->
        </ul>
      </div>
    </div>
  </div>
</nav>
</template>

<style scoped></style>
