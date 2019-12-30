<template>
  <!--wrapper-->
  <div class="--row">

    <!--header break-->
    <div class="--row">
      <div class="--ctr">
        <div class="--row --hr">
          <nuxt-link to="/about" class="t1 --m1">
            About us
          </nuxt-link>
        </div>
      </div>
    </div>
    <!--header break-->

    <!--row1-->
    <div class="--row">
      <div class="--ctr">
        <!--grid-->
        <div class="grid-2">
          <!--row1-->
          <!--col1-->
          <div>
            <nuxt-link to="/who-we-are" class="t4 --m1">
              Who We Are
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/who-we-are">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l1.jpg"
                  alt="Who We Are"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col1-->

          <!--col2-->
          <div>
            <nuxt-link to="/our-objectives" class="t4 --m1">
              Our Objectives
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/our-objectives">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l2.jpg"
                  alt="Our Objectives"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col2-->
          <!--row2-->
        </div>
        <!--grid-->
      </div>
    </div>
    <!--row1-->

    <!--header break-->
    <div class="--row">
      <div class="--ctr">
        <div class="--row --hr">
          <nuxt-link to="/what-we-do" class="t1 --m1">
            What We Do
          </nuxt-link>
        </div>
      </div>
    </div>
    <!--header break-->

    <!--row2-->
    <div class="--row">
      <div class="--ctr">
        <!--grid-->
        <div class="grid-2">
          <!--row1-->
          <!--col1-->
          <div>
            <nuxt-link to="/surgical-training" class="t4 --m1">
              Surgical Training Link
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/surgical-training">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l3.jpg"
                  alt="Surgical Training Link"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col1-->

          <!--col2-->
          <div>
            <nuxt-link to="/visit-reports" class="t4 --m1">
              Reports On Visits
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/visit-reports">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l4.jpg"
                  alt="Reports On Visits"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col2-->

          <!--col3-->
          <div>
            <nuxt-link to="/trauma-life-support" class="t4 --m1">
              Trauma Life Support
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/trauma-life-support">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l5.jpg"
                  alt="Trauma Life Support"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col3-->

          <!--col4-->
          <div>
            <nuxt-link to="/donating-medical-equipment" class="t4 --m1">
              Donating Medical Equipment
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/donating-medical-equipment">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l6.jpg"
                  alt="Donating Medical Equipment"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col4-->

          <!--row2-->
        </div>
        <!--grid-->
      </div>
    </div>
    <!--row2-->

    <!--row3-->
    <div class="--row">
      <div class="--ctr">
        <!--grid-->
        <div class="grid-2">
          <!--row1-->
          <!--col1-->
          <div>
            <nuxt-link to="/about-malawi" class="t4 --m1">
              About Malawi
            </nuxt-link>
            <div class="--row --m1">
              <nuxt-link to="/about-malawi">
                <img
                  width="400"
                  height="300"
                  src="~assets/images/l7.jpg"
                  alt="About Malawi"
                >
              </nuxt-link>
            </div>
          </div>
          <!--col1-->

          <!--col2-->
          <div>
            <div class="--row --hr">
              <nuxt-link to="/news" class="t1 --m1">
                Latest News
              </nuxt-link>
            </div>
            <div class="--row" v-for="post in displayedPosts" :key="post.id">
              <router-link :to="{ path: '/news/'+ post.id +'/' + post.slug}" class="t2 --m2" v-html="post.title.rendered" />
              <p v-html="post.excerpt.rendered" />
              <p>
                <router-link :to="{ path: '/news/'+ post.id +'/' + post.slug}" class="rm">Read More</router-link>
              </p>
            </div>
          </div>
          <!--col2-->

          <!--row2-->
        </div>
        <!--grid-->
      </div>
    </div>
    <!--row3-->

  </div>
  <!--wrapper-->
</template>

<script>
import axios from 'axios'
export default {
  layout: 'default',

  head: {
    title: 'LAST Surgery | Links In Africa For Surgical Training',
    bodyAttrs: { class: 'home' }
  },
  data () {
    return {
      posts: [],
      // global variable set for consistent URL in main js
      page: 1,
      perPage: 1,
      pages: []
    }
  },
  // initial state methods
  methods: {
    // get posts
    getPosts () {
      axios
        .get(process.env.baseUrl + 'posts?per_page=1&categories=3')
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
  .videoWrapper,
  .imgWrapper {
    position: relative;
    padding-bottom: 56.25%; /* 16:9 */
    padding-top: 25px;
    height: 0;
  }
  .videoWrapper iframe,
  .imgWrapper img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>
