<template>
  <div class="carousel carousel-slider" indicators="true">
    <div class="headline">
      <h1>ABOUT PAGE</h1>
      </div>
    <!-- <a v-for="i in 5" :key="i" class="carousel-item" href="#one!"><img src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fi1.ytimg.com%2Fvi%2FPB5FosTwM8s%2Fmaxresdefault.jpg"></a>
    <a class="carousel-item" href="#two!"><img src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fi1.ytimg.com%2Fvi%2FPB5FosTwM8s%2Fmaxresdefault.jpg"></a>
    <a class="carousel-item" href="#three!"><img src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fi1.ytimg.com%2Fvi%2FPB5FosTwM8s%2Fmaxresdefault.jpg"></a>
    <a class="carousel-item" href="#four!"><img src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fi1.ytimg.com%2Fvi%2FPB5FosTwM8s%2Fmaxresdefault.jpg"></a>
    <a class="carousel-item" href="#five!"><img src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fi1.ytimg.com%2Fvi%2FPB5FosTwM8s%2Fmaxresdefault.jpg"></a>
  -->
  </div>
</template>

<script>
export default {
  mounted() {
    var elems = document.querySelectorAll('.carousel');
    this.$M.Carousel.init(elems);

    setTimeout(this.$M.Carousel.init(elems), 1000)
    
  }
  
}
</script>

<style lang="css">

.headline{
  text-align: center;
}

</style>