<template>
  <div id="customers-home" class="section">
    <div class="container">
      <h1 class="is-size-1">{{ page_title }}</h1>
      <hr>
      <div class="columns is-multiline">
        <div class="column is-one-third" v-for="(page,index) in pages" :key="page.slug + '_' + index">
          <router-link :to="'/customers/' + page.slug">
            <div class="box">
              <article class="media">
                <div class="media-left">
                  <figure class="image is-64x64">
                    <img :src="page.fields.customer_logo" alt="">
                  </figure>
                </div>
                <div class="media-content">
                  <div class="content">
                    <h2 class="title is-5">{{ page.fields.headline }}</h2>
                  </div>
                </div>
              </article>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { butter } from '@/buttercms'
  export default {
    name: 'customers-home',
    data() {
      return {
        page_title: 'Customers',
        pages: []
      }
    },
    methods: {
      getPages() {
        butter.page.list('customer_case_study')
          .then((res) => {
            this.pages = res.data.data
          })
      }
    },
    created() {
      this.getPages()
    }
  }
</script>