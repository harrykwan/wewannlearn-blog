<template>
  <div>
    <Header />
    <Trigobg />
    <div class="whitesection">
      <section v-if="post" class="postscontent toppost">
        <img v-if="post.cover" class="cover-image big-cover" :src="post.cover" />

        <div style="background: grey; width: 100%; height: 100px; margin-bottom: 30px; margin-top: 30px"></div>
        <div class="row">
          <div class="col-sm-9">
            <nav @click="$router.go(-1)" class="backbutton" aria-label="go back">← Back to Blog</nav>
            <article>
              <h5
                v-if="post.createdAt"
                class="inline-block py-1 px-2 my-2 bg-gray text-white text-sm font-medium rounded-sm whitespace-no-wrap"
              >
                {{ formatDate(post.createdAt) }}
              </h5>
              <h1 class="">{{ post.title }}</h1>
              <p class="mt-1 mb-4 text-primary-600 dark:text-primary-400">{{ post.description }}</p>
              <nuxt-content :document="post" />
            </article>
          </div>
          <div class="col-sm-3"><div style="background: grey; min-height: 100px; width: 100%; height: 100%"></div></div>
        </div>
        <div style="text-align: center">
          <video class="coursevideo">
            <source :src="post.coursevideo" />
            Your browser does not support the video tag.
          </video>
          <a :href="post.joinlesson"><button class="joinlessonbutton">Join The Lesson Now</button></a>
        </div>
      </section>
    </div>
    <Footer />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post
    try {
      post = await $content('blog', params.blog).fetch()
    } catch (e) {
      error({ message: 'Blog post not found' })
    }
    return { post }
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    },
  },
}
</script>

<style scoped>
.postscontent {
  margin-top: -50px;
  max-width: 1024px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
}

.whitesection {
  background: white;
  width: 100vw;
  color: black;
  padding-top: 350px;
  padding-bottom: 50px;
}

.big-cover {
  /* margin-bottom: 60px; */
  width: 100%;
  max-height: 540px;
  height: auto;
  z-index: 99;
  position: relative;
}

.toppost {
  margin-top: -500px;
}

.backbutton:hover {
  cursor: pointer;
}

.joinlessonbutton {
  background: #007bff;
  border-radius: 20px;
  color: white;
  padding: 5px 20px;
  margin-top: 20px;
}

.coursevideo {
  width: 800px;
  background: #fd5e34;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
}

@media screen and (max-width: 991px) {
  .big-cover {
    /* height: auto; */
    /* height: 200px; */
    object-fit: cover;
  }

  .postscontent {
    /* padding: 0px 50px; */
    width: 90%;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>
