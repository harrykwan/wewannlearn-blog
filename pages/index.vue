<template>
  <div>
    <Header />
    <Trigobg />
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <posts post-type="blog" :amount="100" />
    </section>
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
