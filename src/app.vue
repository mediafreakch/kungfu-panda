<template>
  <app-header></app-header>
  <div id="content" class="row">
    <app-articles-list
      :articles="articles"></app-articles-list>
  </div>
  <app-footer></app-footer>
</template>

<script>
  const layout = require('page~global')
  const header = require('component~header')
  const footer = require('component~footer')
  const articlesList = require('component~articles-list')

  const articlesURL = 'src/data/articles.json'

  module.exports = {
    el: '#app',

    components: {
      'app-header': header,
      'app-footer': footer,
      'app-articles-list': articlesList
    },

    replace: false,

    created: function () {
      this.fetchData()
    },

    data: {
      articles: []
    },

    methods: {
      fetchData: function () {
        // adapted from https://jsfiddle.net/yyx990803/vaj48u3h/
        const xhr = new XMLHttpRequest()
        xhr.open('GET', articlesURL)
        xhr.onload = () => {
          const data = JSON.parse(xhr.responseText)
          this.articles = data.articles
        }
        xhr.send()
      }
    }
  }
</script>
