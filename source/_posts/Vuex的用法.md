---
title: Vuex的用法
date: 2018-08-27 11:13:10
tags: 总结
categories: 编程
---

```js
main.js
import Vue from 'vue'
import App form './App'
import router from './router'
import store from './store'

new Vue({
    el: '#app',
    router,
    store,
    template: '<App/>',
    components: { App }
})
```

```vue
App.vue
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
```

```js
store.js
import Vue from 'vue'
import Vuex from 'vuex'
import app from './modules/app'
import user from './modules/user'
import vehicle from './modules/vehicle'
import getters from './getters'

Vue.use(Vuex)

const store = new Vuex.Store({
  modules: {
    app,
    user,
    vehicle,
  },
  getters
})

export default store

```

上文中的store中，modules使用store中的模块，方便数据分类管理。

```js
vehicle.js
import { taskOrderDetail } from '@/api/vehicle'
const vehicle = {
  // namespaced: true,
  state: {
    // 数据
    requestCode:null,
  },
  mutations: {
    // 同步修改数据
    SET_REQUESTCODE: (state, value) => {
   	  state.requestCode = value
	},
    SET_VEHICLELISTDETAIL: (state, vehicleListDetail) => {
      state.vehicleListDetail = vehicleListDetail
    }
  },
  actions: {
    // 异步修改数据，比如api请求
    setVehicleListDetail({ commit, state }) {
      return new Promise((resolve, reject) => {
        taskOrderDetail({ requestCode: state.request }).then(response => {
          commit('SET_VEHICLELISTDETAIL', response.data)
          resolve(response)
        }).catch(error => {
          reject(error)
        })
      })
    }
  }
export default vehicle
```

vue组件中如何引用store中的数据

```js
xx.vue
import { mapState } from 'vuex'

export default {
    // ...
    computed: {
        ...mapState({
            vehicleListDetail: state => state.vehicle.vehicleListDetail,
            requestCode: state => state.vehicle.requestCode
        })
    }
}
```

