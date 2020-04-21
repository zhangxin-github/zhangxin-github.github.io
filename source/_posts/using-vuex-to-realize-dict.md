---
title: 利用vuex实现数据字典
date: 2019-08-20 09:25:46
tags:
---

### vuex定义

```js

state:{
    // 排序类型字典
    messageOrderTypeDict: [],
    // 排序参数字典
    messageOrderParamDict: [],
},
getters: {
    messageOrderParamDict (state) {
        return state.messageOrderParamDict
    },
    messageOrderTypeDict (state) {
        return state.messageOrderTypeDict
    },
},
mutations:{
    SET_MESSAGE_ORDER_PARAM_DICT (state, payload) {
        state.messageOrderParamDict = payload
    },
    SET_MESSAGE_COMMENT_LIST (state, payload) {
        state.messageCommentList = payload
    },
},
actions:{
    // 获取排序方向，排序类型字典
    getMessageOrderDict ({ commit }, payload) {
        http.request(App.getDictionary, payload).then(res => {
            const data = _.get(res, 'data') || {}
            commit('SET_MESSAGE_ORDER_PARAM_DICT', data['order-param'])
            commit('SET_MESSAGE_ORDER_TYPE_DICT', data['order-type'])
        })
    },
}

```


### 页面调用

```js

import { mapGetters } from 'vuex'

computed: {
    ...mapGetters([
        // 排序字典
        'messageOrderTypeDict',
        // 排序字典
        'messageOrderParamDict'
    ])
},
created () {
    this.getMessageOrderDict()
},
methods: {
    getMessageOrderDict () {
        this.$store.dispatch('getMessageOrderDict', ['order-param', 'order-type'])
    },
}

```