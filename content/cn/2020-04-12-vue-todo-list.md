---
title: Vue Todo List
date: '2020-04-12'
slug: vue-todo-list
categories:
  - Developer
  - frontend
  - Vuejs
---

# todolist功能开发 

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue 101</title>
    <script src="./vue.js"></script>
</head>

<body>
<div id="root">
    <div>
        <input v-model="inputValue"/>
        <button @click="handleSubmit">submit</button>
    </div>
    <ul>
        <li v-for="(item, index) of list" :key="index">
            {{item}}
        </li>
    </ul>
</div>

<script>
    new Vue({
        el: "#root",
        data: {
            inputValue: 'hello',
            list: []
        },
        methods: {
            handleSubmit: function () {
                this.list.push(this.inputValue)
                this.inputValue = ''
            }
        }
    })
</script>
</body>
</html>
```

# todolist组件拆分
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue 101</title>
    <script src="./vue.js"></script>
</head>

<body>
<div id="root">
    <div>
        <input v-model="inputValue"/>
        <button @click="handleSubmit">submit</button>
    </div>
    <ul>
        <todo-item v-for="(item, index) of list"
                   :key="index"
                   :content="item"
        ></todo-item>
    </ul>
</div>

<script>
    Vue.component('todo-item',{
        props: ['content'],
        template: '<li>{{content}}</li>'
    })
    //var TodoItem = {
    //    props: ['content'],
    //    template: '<li>{{content}}</li>'
    //}

    new Vue({
        el: "#root",
        //components: {
        //    'todo-item': TodoItem
        //},
        data: {
            inputValue: '',
            list: []
        },
        methods: {
            handleSubmit: function () {
                this.list.push(this.inputValue)
                this.inputValue = ''
            }
        }
    })
</script>
</body>
</html>
```
# 组件与实例的关系
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue 101</title>
    <script src="./vue.js"></script>
</head>

<body>
<div id="root">
    <div>
        <input v-model="inputValue"/>
        <button @click="handleSubmit">submit</button>
    </div>
    <ul>
        <todo-item v-for="(item, index) of list"
                   :key="index"
                   :content="item"
        ></todo-item>
    </ul>
</div>

<script>
    Vue.component('todo-item',{
        props: ['content'],
        template: '<li @click="handleClick">{{content}}</li>',
        methods:{
            handleClick:function () {
                alert('clicked')
            }
        }
    })
    new Vue({
        el: "#root",
        //components: {
        //    'todo-item': TodoItem
        //},
        data: {
            inputValue: '',
            list: []
        },
        methods: {
            handleSubmit: function () {
                this.list.push(this.inputValue)
                this.inputValue = ''
            }
        }
    })
</script>
</body>
</html>
```

# todolist 删除功能

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue 101</title>
    <script src="./vue.js"></script>
</head>

<body>
<div id="root">
    <div>
        <input v-model="inputValue"/>
        <button @click="handleSubmit">submit</button>
    </div>
    <ul>
        <todo-item v-for="(item, index) of list"
                   :key="index"
                   :content="item"
                   :index="index"
                   @delete="handleDelete"
        ></todo-item>
    </ul>
</div>

<script>
    Vue.component('todo-item', {
        props: ['content', 'index'],
        template: '<li @click="handleClick">{{content}}</li>',
        methods: {
            handleClick: function () {
                this.$emit('delete', this.index)
            }
        }
    })
    new Vue({
        el: "#root",
        //components: {
        //    'todo-item': TodoItem
        //},
        data: {
            inputValue: '',
            list: []
        },
        methods: {
            handleSubmit: function () {
                this.list.push(this.inputValue)
                this.inputValue = ''
            },
            handleDelete: function (index) {
                this.list.splice(index, 1)
            }
        }
    })
</script>
</body>
</html>
```
