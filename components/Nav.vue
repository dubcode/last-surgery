<template>
  <nav class="nav --row --fs --flex">
    <div class="--ctr">
      <div class="grid-2">

        <div>
          <ul class="--row">
            <li v-for="link in nav_set_1" :key="link.link" class="--row">
              <a :href="link.link" class="--row">{{ link.title }}</a>
            </li>
          </ul>
        </div>

        <div>
          <ul class="--row">
            <li v-for="link in nav_set_2" :key="link.link" class="--row">
              <a :href="link.link" class="--row">{{ link.title }}</a>
            </li>
          </ul>
        </div>

      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data () {
    return {
      nav_set_1: [
        {
          link: '/about',
          title: 'About Us'
        },
        {
          link: '/news',
          title: 'News'
        },
        {
          link: '/who-we-are',
          title: 'Who We Are'
        },
        {
          link: '/objectives',
          title: 'Objectives'
        },
        {
          link: '/partners',
          title: 'Partners'
        },
        {
          link: '/document-library',
          title: 'Document Library'
        },
        {
          link: '/donate',
          title: 'Donate'
        }
      ],
      nav_set_2: [
        {
          link: '/about-malawi',
          title: 'What We Do'
        },
        {
          link: '/surgical-training',
          title: 'Surgical Training Link'
        },
        {
          link: '/visit-reports',
          title: 'Reports On Visits'
        },
        {
          link: '/trauma-life-support',
          title: 'Trauma Life Support'
        },
        {
          link: '/donating-medical-equipment',
          title: 'Donating Medical Equipment'
        },
        {
          link: '/about-malawi',
          title: 'About Malawi'
        }
      ]
    }
  }
}
</script>
