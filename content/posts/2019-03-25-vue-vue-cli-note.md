---
layout: post
title: 'Vue - Vue cli note'
date: 2019-03-25
comments: true
categories:
---
## Vue - Vue cli note

[https://cli.vuejs.org/](https://cli.vuejs.org/)

### vuetify

```shell
vue create <project folder name>

cd <project folder name>

vue add vuetify

npm run serve
```

### Use SPA

App.vue

```html
<template>
  <router-view></router-view>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data () {
    return {
    }
  }
}
</script>

```
