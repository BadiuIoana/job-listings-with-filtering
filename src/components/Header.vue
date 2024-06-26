
<template>
  <div class="blue-pattern-bg"></div>
</template>

<style scoped>
.blue-pattern-bg {
  background-image: url(../assets/images/bg-header-mobile.svg);

  background-color: var(--dark-cyan);
  background-size: cover;
  background-repeat: no-repeat;
  height: 10em;
  width: 100%;
}

@media (min-width: 1440px) {
  .blue-pattern-bg {
    background-image: url(../assets/images/bg-header-desktop.svg);
  }
}
</style>