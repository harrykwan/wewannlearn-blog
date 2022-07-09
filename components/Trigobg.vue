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
  opacity: 0.8;
}

.slash {
  width: 300px;
  top: -150px;
  right: -100px;
}

.opentag {
  left: 250px;
  width: 200px;
  top: 80px;
}

.bubble {
  top: 100px;
  left: -100px;
  width: 450px;
}

.closetag {
  top: 100px;
  right: -90px;
  width: 260px;
}

@media screen and (max-width: 991px) {
  img {
    display: none;
  }
}
</style>
