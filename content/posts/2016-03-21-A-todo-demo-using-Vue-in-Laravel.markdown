---
layout: post
title:  "A todo demo using Vue in Laravel"
date:   2016-03-21
categories: [' web development']
tags: ['vue', 'laravel']
---

#### html

```html
<div id="app">
  <ul>
    <li><a v-link="'tasks'">tasks</a></li>
    <li><a v-link="'about'">about</a></li>
  </ul>

  <router-view></router-view>
</div>

<script src="js/main.js"></script>
```

#### main.js

```js
import tasks from './components/tasks.vue';

const Vue = require('vue');
const VueRouter = require('vue-router');

Vue.use(VueRouter);
Vue.use(require('vue-resource'));
Vue.http.headers.common['X-CSRF-TOKEN'] = document.getElementById('csrf_token').getAttribute('content');

const router = new VueRouter();

router.map({
  '/tasks': {
    component: tasks
  },

  '/about': {
    component: {
      template: `
        <div>
          <h3>About Page</h3>
          <p>This is the about page</p>
        </div>
      `
    }
  }
});

router.start({}, '#app');
```

#### tasks.vue

```html
<template>
  <h3>My Tasks <span v-show="list.length">({{ list.length }})</span></h3>
  <div class="form-group">
    <label for="">Add Task</label>
    <input v-model="task" @keyup.enter="postTask(task)" type="text" class="form-control">
  </div>
  <ul class="list-group">
    <li v-for="task in list" class="list-group-item">
      {{ task.body }}
      <strong @click="deleteTask(task)">x</strong>
    </li>
  </ul>
</template>

<script>
  export default {
    data() {
      return {
        task: '',
        list: [],
        resource: this.$resource('/api/tasks{/id}')
      };
    },

    created() {
      this.getTasks();
    },

    methods: {
      getTasks() {
        this.resource.get().then(tasks => {
          this.list = tasks.data;
        });
      },

      postTask(task) {
        if (!task.trim()) return;
        this.resource.save({
          body: task
        }).then(() => {
          this.getTasks();
          this.task = '';
        });
      },

      deleteTask(task) {
        this.resource.delete({
          id: task.id
        }).then(() => {
          this.list.$remove(task);
        });
      }
    }
  };
</script>
```
