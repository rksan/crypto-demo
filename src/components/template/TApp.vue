<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg navbar-dark">
      <div class="container-fluid">
        <a class="navbar-brand fs-1" href="#">Crypto Demo</a>

        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <i class="bi bi-list"></i>
        </button>

        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a
                class="nav-link"
                href="https://github.com/rksan/crypto-demo"
                target="_blank"
              >
                <i class="bi bi-github"></i>
                github
                <i class="bi bi-box-arrow-up-right"></i>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <slot></slot>
  </div>
</template>

<style scoped>
.list-group,
.list-group-item {
  background-color: inherit;
  color: inherit;
}
</style>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "t-app",
});
</script>
