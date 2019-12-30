<template>
  <div class="--row">

    <!--header break-->
        <div class="--row --hr --m3">
          <nuxt-link to="/document-library" class="t1 partner_btn">
            Document Library
          </nuxt-link>
        </div>
    <!--header break-->

    <div class="--row" v-for="post in displayedPosts" :key="post.id">
      <a class="dl --row" :href="post.acf.link_url" target="_blank">
        <h4 class="t2 --m2" v-html="post.title.rendered" />
        <p><b>Author:</b> {{ post.acf.author }} <b>year:</b> {{ post.acf.year }}</p>
        <div class="--hr --m1" />
      </a>
    </div>
    <!--
    <div class="pager">
        <div class="pager__ctr">
        <button type="button" v-if="page != 1" @click="page--"> prev </button>
        <button type="button" v-for="pageNumber in pages.slice(page-1, page+5)" :key="pageNumber" @click="page = pageNumber"> {{pageNumber}} </button>
        <button type="button" @click="page++" v-if="page < pages.length"> next </button>
        </div>
    </div>
    -->
</div>
</template>

<script>
import axios from 'axios'
export default {
  layout: 'layout-one',
  data () {
    return {
      posts: [],
      // global variable set for consistent URL in main js
      page: 1,
      perPage: 20,
      pages: []
    }
  },
  head () {
    return {
      title: this.title + ' | LAST Surgery',
      bodyAttrs: { class: 'page' }
    }
  },
  // initial state methods
  methods: {
    // get posts
    getPosts () {
      axios
        .get(process.env.baseUrl + 'posts?per_page=100&categories=10')
        .then((response) => {
          this.posts = response.data
        })
        .catch((response) => {
          console.log(response)
        })
    },
    // set pages
    setPages () {
      const numberOfPages = Math.ceil(this.posts.length / this.perPage)
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index)
      }
    },
    // paginate
    paginate (posts) {
      const page = this.page
      const perPage = this.perPage
      const from = page * perPage - perPage
      const to = page * perPage
      return posts.slice(from, to)
    }
  },
  // created
  created () {
    this.getPosts()
  },
  // watch
  watch: {
    posts () {
      this.setPages()
    }
  },
  // computed
  computed: {
    displayedPosts () {
      return this.paginate(this.posts)
    }
  }
}
</script>

<style scoped>
.dl{
  text-decoration: none;
}
.partner_btn {
  opacity: 1;
  transition: all ease 0.3s;
}
.sponsor_btn {
  transform: translateX(-4px);
  transition: all ease 0.3s;
}
</style>
