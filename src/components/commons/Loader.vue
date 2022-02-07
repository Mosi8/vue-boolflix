<template>
  <div class="text-center">
      <span><i class="loading fas fa-spinner"></i></span>
  </div>
</template>

<script>
export default {
    name: 'Loader',
}
</script>

<style lang="scss" scoped>

.loading {
    animation: giro 0.2s linear infinite;
    color: #fff;
    font-size: 100px;
    margin-top: 200px;
}

@keyframes giro {
    0%{
        transform: rotate(-1turn);
    }
}

</style>