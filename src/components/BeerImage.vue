<template>
  <div class="img-container">
    <img
      v-for="index in 9"
      :key="index"
      class="beer"
      :alt="currentBeer"
      :src="
        index === currentBeer + 1
          ? getImgUrl('beer_last.png')
          : index === currentBeer + 2
          ? getImgUrl('beer_prelast.png')
          : currentBeer >= index
          ? getImgUrl('beer.gif')
          : getImgUrl('beer.png')
      "
    />
  </div>
</template>

<script>
export default {
  name: "BeerImage",
  props: {
    currentBeer: {
      type: Number,
      required: true,
    },
  },
  data: function () {
    return {
      maxPos: 600,
    };
  },

  methods: {
    getImgUrl(img) {
      var getImage = require.context("../assets/", false, /\.*$/);
      return getImage("./" + img);
    },
  },
};
</script>

<style scoped>
.img-container {
  display: flex;
  justify-content: center;
}

img.beer {
  width: 60px;
}
</style>
