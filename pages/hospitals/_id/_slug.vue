<template>
  <div class="--row">
    <div class="directory__thumb">
      <h4 class="t2 --m2" v-html="this.title" />
        <img :src="this.thumb" :alt="this.title" class="--m3"/>
    </div>
    <div class="directory__excerpt" v-html="this.content" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  layout: 'layout-one',

  // meta
  head () {
    return {
      title: this.title,
      bodyAttrs: { class: 'single' }
    }
  },

  // post data
  data () {
    return {
      id: this.$route.params.id,
      // global variable set for consistent URL in main js
      posts: [],
      post: '',
      title: '',
      thumb: '',
      content: '',
      date: '',
      categoryId: '',
      tags: '',
      isActive: 'isActive',
      location: '',
      hospitalType: '',
      beds: '',
      facilities: '',
      comments: '',
      specialities: '',
      transportation: '',
      accommodation: '',
      stay: '',
      visa: '',
      other: '',
      contact: '',
      landline: '',
      mobile: '',
      email: '',
      website: ''
    }
  },
  // post methods
  methods: {
  // get single post
    getSingle () {
      this.id = this.$route.params.id
      axios.get(process.env.baseUrl + 'posts/' + this.id + '?_embed', {
      })
        .then((response) => {
          this.title = response.data.title.rendered
          this.content = response.data.content.rendered
          this.thumb = response.data.images.medium
          this.tags = response.data.tags
          this.date = response.data.date
          this.categoryId = response.data.categories[0]
          this.location = response.data.acf.location
          this.hospitalType = response.data.acf.hospital_type
          this.beds = response.data.acf.number_of_beds
          this.facilities = response.data.acf.hospital_facilities
          this.comments = response.data.acf.additional_comments
          this.specialities = response.data.acf.specialities_required
          this.transportation = response.data.acf.transportation
          this.accommodation = response.data.acf.accommodation
          this.stay = response.data.acf.length_of_stay
          this.visa = response.data.acf.visa_requirements
          this.other = response.data.acf.other_info
          this.contact = response.data.acf.contact_name
          this.landline = response.data.acf.landline
          this.mobile = response.data.acf.mobile
          this.email = response.data.acf.email
          this.website = response.data.acf.website
        })
        .catch((response) => {
          console.log(response)
        })
    }
  },
  mounted () {
    this.getSingle()
  }
}
</script>

<style scoped>
.directory {
  display: grid;
  grid-gap: 2em;
  grid-template-columns: 0.6fr 1.4fr;
  grid-template-rows: 1fr;
  grid-template-areas: "thumb excerpt";
}
.directory__excerpt {grid-area: excerpt; }
.directory__excerpt p {
  text-align: left;
}
.directory__thumb { grid-area: thumb; }
.directory__thumb img {
  max-width: 768px;
}
</style>
