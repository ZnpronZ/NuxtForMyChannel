<template>
  <div class="ct">
    <event-alert />
    <div class="banner">
      <div class="thumbnail-banner"></div>
    </div>
    <div class="popular-decks">
      <h3 class="text_center my_3">3 Popular Decks For You</h3>
      <div class="r">
        <div class="c_4">
          <div class="card">
            Deck 1
          </div>
        </div>
        <div class="c_4">
          <div class="card">
            Deck 1
          </div>
        </div>
        <div class="c_4">
          <div class="card">
            Deck 1
          </div>
        </div>
      </div>
    </div>
  </div>
  <!--  <Tutorial />-->
</template>

<style lang="scss">
.banner {
  height: 220px;
  margin-top: 3rem;

  .thumbnail-banner {
    height: inherit;
    background: url('https://www.shutterstock.com/image-vector/horizontal-internet-banner-about-learning-260nw-1603435279.jpg') center center;
    background-size: cover;
  }
}
</style>
<script>
export default {
  name: 'IndexPage',
}
</script>
