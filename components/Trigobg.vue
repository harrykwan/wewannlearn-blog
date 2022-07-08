<template>
  <div>
    <img class="slash" src="~/assets/img/bg/slash.png" />
    <img class="opentag" src="~/assets/img/bg/opentag.png" />
    <img class="closetag" src="~/assets/img/bg/closetag.png" />
    <img class="bubble" src="~/assets/img/bg/bubble.png" />
  </div>
</template>

<style scoped>
.slash,
.opentag,
.closetag,
.bubble {
  position: absolute;
  z-index: 0;
  opacity: 0.5;
}

.slash {
  width: 500px;
  top: -200px;
  right: 0;
}

.opentag {
  left: -100px;
  width: 400px;
  top: 250px;
}

.bubble {
  top: 400px;
  left: 100px;
  width: 450px;
}

.closetag {
  left: calc(50vw + 300px);
  width: 600px;
}

@media screen and (max-width: 991px) {
  img {
    display: none;
  }
}
</style>
