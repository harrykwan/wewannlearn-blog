<template>
  <div>
    <Header />
    <Trigobg />
    <div class="whitesection">
      <section v-if="posts" class="w-full max-w-5xl mx-auto postscontent">
        <posts post-type="blog" :amount="100" />
      </section>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'
import Trigobg from '~/components/Trigobg.vue'

export default {
  async asyncData({ $content, error }) {
    let posts
    try {
      posts = await $content('blog').fetch()
    } catch (e) {
      error({ message: 'Blog posts not found' })
    }
    return { posts }
  },
  components: { Header, Footer, Trigobg },
}
</script>
<style scoped>
.whitesection {
  background: white;
  width: 100vw;
  color: black;
  padding-top: 350px;
  padding-bottom: 50px;
}

.postscontent {
  margin-top: -50px;
}
</style>
