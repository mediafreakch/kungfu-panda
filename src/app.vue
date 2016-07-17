<template>
  <app-header></app-header>
  <div id="content" class="row">
    <app-search-bar :search-query.sync="searchQuery"></app-search-bar>
    <app-articles-list
      :articles="articles"
      :filter-query="searchQuery"></app-articles-list>
  </div>
  <app-footer></app-footer>
</template>

<script>
  const layout = require('page~global')
  const header = require('component~header')
  const footer = require('component~footer')
  const articlesList = require('component~articles-list')
  const searchBar = require('component~search-bar')

  const articlesURL = 'src/data/articles.json'

  module.exports = {
    el: '#app',

    components: {
      'app-header': header,
      'app-footer': footer,
      'app-articles-list': articlesList,
      'app-search-bar': searchBar
    },

    replace: false,

    created: function () {
      this.fetchData()
    },

    data: {
      articles: [],
      searchQuery: ''
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
