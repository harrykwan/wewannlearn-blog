<template>
  <div class="row" v-if="posts.length > 0">
    <div class="col-12 toppost">
      <nuxt-link :to="`${posts[0].slug}`" class="postlist">
        <template v-if="postType === 'projects'">
          <img v-if="posts[0].cover" class="cover-image" :src="posts[0].cover" />
          <span class="flex-1">
            <h6 class="inline-block py-1 px-2 mr-1 bg-gray text-white text-sm font-medium rounded-sm">
              {{ posts[0].category }}
            </h6>
            <h3 class="card-title">{{ posts[0].title }}</h3>
            <p class="mt-2">{{ posts[0].description }}</p>
          </span>
        </template>

        <template v-else>
          <span class="w-full">
            <img v-if="posts[0].cover" class="cover-image big-cover" :src="posts[0].cover" />
            <span class="big-cover-words">
              <span class="flex justify-between align-baseline">
                <h3 class="card-title big-cover-title">
                  {{ posts[0].title }} <br />
                  <button class="big-readmore">Read More</button>
                </h3>
                <!-- <h6
                  v-if="posts[0].createdAt"
                  class="self-start inline-block mt-0 py-1 px-2 bg-gray text-white text-base font-medium rounded-sm whitespace-no-wrap"
                >
                  {{ formatDate(posts[0].createdAt) }}
                </h6> -->
              </span>
              <!-- <p class="mt-2">{{ posts[0].description }}</p> -->
            </span>
          </span>
        </template>
      </nuxt-link>
    </div>
    <div class="smallposts row">
      <div class="col-6 col-md-4" v-for="(post, index) in posts" :key="index">
        <nuxt-link :to="`${post.slug}`" class="postlist">
          <template v-if="postType === 'projects'">
            <img v-if="post.cover" class="cover-image" :src="post.cover" />
            <span class="flex-1">
              <h6 class="inline-block py-1 px-2 mr-1 bg-gray text-white text-sm font-medium rounded-sm">
                {{ post.category }}
              </h6>
              <h3 class="card-title">{{ post.title }}</h3>
              <p class="mt-2">{{ post.description }}</p>
            </span>
          </template>

          <template v-else>
            <span class="w-full">
              <img v-if="post.cover" class="cover-image small-cover" :src="post.cover" />
              <span class="flex justify-between align-baseline">
                <span v-if="post.tags">{{ post.tags }}</span>
                <h3 class="card-title small-title">{{ post.title }}</h3>
                <!-- <h6
                  v-if="post.createdAt"
                  class="self-start inline-block mt-0 py-1 px-2 bg-gray text-white text-base font-medium rounded-sm whitespace-no-wrap"
                >
                  {{ formatDate(post.createdAt) }}
                </h6> -->
              </span>
              <p class="small-description">{{ post.description }}</p>
              <button class="small-readmore">Read More</button>
            </span>
          </template>
        </nuxt-link>
      </div>
    </div>
  </div>
  <div v-else-if="loading" class="cards">
    <div v-for="placeholder in placeholderClasses" :key="placeholder.id" class="card">
      <content-placeholders :rounded="true" :class="placeholder">
        <content-placeholders-heading />
      </content-placeholders>
    </div>
  </div>
  <p v-else class="max-w-5xl mx-auto">
    {{ amount > 1 ? 'Posts not found' : 'Post not found' }}
  </p>
</template>

<script>
export default {
  name: 'Posts',
  props: {
    postType: {
      type: String,
      default: 'blog',
      validator: (val) => ['blog', 'projects'].includes(val),
    },
    amount: {
      // ? https://content.nuxtjs.org/fetching#limitn
      type: Number,
      default: 10,
      validator: (val) => val >= 0 && val < 1000,
    },
    sortBy: {
      // ? https://content.nuxtjs.org/fetching#sortbykey-direction
      type: Object,
      default: () => ({
        key: 'slug',
        direction: 'desc', // you probably want 'asc' here
      }),
      validator: (obj) => typeof obj.key === 'string' && typeof obj.direction === 'string',
    },
  },
  data() {
    return {
      posts: [],
      loading: true,
    }
  },
  computed: {
    placeholderClasses() {
      const classes = ['w-full', 'w-2/3', 'w-5/6']
      return [...Array.from({ length: this.amount }, (v, i) => classes[i % classes.length])] // repeats classes after one another
    },
  },
  async mounted() {
    this.loading = true
    this.posts = await this.fetchPosts()
    this.loading = false
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    },
    async fetchPosts(postType = this.postType, amount = this.amount, sortBy = this.sortBy) {
      return this.$content(postType)
        .sortBy(sortBy.key, sortBy.direction)
        .limit(amount)
        .fetch()
        .catch((err) => console.error(err) || [])
    },
  },
}
</script>

<style scoped>
.postlist {
}

.toppost {
  margin-top: -430px;
}

.big-cover {
  margin-bottom: 60px;
  max-height: 540px;
  height: auto;
}

.big-cover-words {
  position: absolute !important;
  top: 0;
  background: rgba(0, 0, 0, 0.34);
  color: white;
  max-width: 1024px;
  width: 100%;
  height: 100%;
  max-height: 540px;
}

.smallposts {
  max-width: 1054px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
}

.big-cover-title {
  bottom: 30px;
  position: absolute;
  margin-left: 30px;
  font-size: 35px;
  font-weight: bold;
}

.small-cover {
  height: 170px;
  object-fit: cover;
}

.small-hashtag {
}

.small-title {
  margin-top: 10px;
  font-size: 20px;
  color: #fd5e34;
  font-weight: bold;
}

.big-readmore {
  background: #fd5e34;
  color: white;
  font-size: 18px;
  padding: 8px 15px;
  border-radius: 20px;
  margin-top: 15px;
}

.small-readmore {
  background: #007bff;
  color: white;
  padding: 5px 18px;
  border-radius: 20px;
  margin-top: 20px;
}

@media screen and (max-width: 991px) {
  .smallposts {
    margin-top: -200px;
    width: 95vw;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }
  .big-cover {
    /* height: auto; */
    height: 200px;
    object-fit: cover;
    width: 95%;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }

  .big-cover-words {
    height: 200px;
    width: 95vw;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }

  .small-cover {
    /* height: auto; */
    height: 100px;
    object-fit: cover;
    width: 45vw;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }

  .big-cover-title {
    font-size: 20px;
    bottom: 0px;
    margin-left: 15px;
  }

  .small-title {
    font-size: 15px;
  }

  .big-readmore {
    font-size: 13px;
    padding: 8px 15px;
    border-radius: 20px;
    margin-top: 10px;
  }

  .small-readmore {
    font-size: 12px;
    padding: 5px 10px;
    border-radius: 20px;
    margin-top: 12px;
  }
}
</style>
