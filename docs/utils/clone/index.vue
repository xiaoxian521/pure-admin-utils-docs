<script setup lang="ts">
import { ref } from "vue"
import { clone, hasOwnProp } from "@pureadmin/utils"
import { NButton, NGradientText, NDivider } from "naive-ui"

const obj = { name: 'Tom' }
const arr1 = ref('text')
let copyArr1 = clone(arr1)

const arr2 = ref([0, { age: 18 }])
let copyArr2 = clone(arr2)

const arr3 = ref([1, 2, 3, { name: 'boy' }])
let copyArr3 = clone(arr3, true)

function shallowCopy() {
  copyArr1.value = 'copy-text'
}

function shallowCopyChange() {
  copyArr2.value[0] = 100
}

function deepCopy() {
  copyArr3.value = [0, 1, 2]
}
</script>

<template>
  <naive-theme>
    <n-button @click="shallowCopy"> 浅拷贝（基本数据类型）</n-button>
    <p>
      拷贝数据改变: <n-gradient-text type="info">
        {{ copyArr1 }}
      </n-gradient-text>
      原数据不变: <n-gradient-text type="info">
        {{ arr1 }}
      </n-gradient-text>
    </p>

    <n-button @click="shallowCopyChange"> 浅拷贝（引用数据类型）</n-button>
    <p>
      拷贝数据改变: <n-gradient-text type="info">
        {{ copyArr2 }}
      </n-gradient-text>
      原数据改变: <n-gradient-text type="info">
        {{ arr2 }}
      </n-gradient-text>
    </p>

    <n-button @click="deepCopy"> 深拷贝 </n-button>
    <p>拷贝数据改变: <n-gradient-text type="info">
        {{ copyArr3 }}
      </n-gradient-text>
      原数据不变: <n-gradient-text type="info">
        {{ arr3 }}
      </n-gradient-text>
    </p>

    <n-divider />
    <p>对象 {{ obj }} 中 <n-gradient-text type="info">
        {{ hasOwnProp(obj, 'name') ? '存在' : '不存在' }}
      </n-gradient-text> name 属性</p>
  </naive-theme>
</template>
