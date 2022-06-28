<!-- <script setup lang="ts">
  import { createFilterWrapper, debounceFilter } from '@vueuse/core'
  import {ref, watch} from 'vue'
  import type { Ref } from 'vue'
  
  type MaybeRef<T> = T | Ref<T>
  type FunctionArgs<Args extends any[] = any[], Return = void> = (...args: Args) => Return
  
  const source = ref(0)
  
  const callback = () => console.log('changed!')
  
  // 手写一个防抖
  const debouncedFn = (ms:MaybeRef<number>, fn:FunctionArgs) => {
    return createFilterWrapper(debounceFilter(ms),  fn)
  }
  
  const watchCallback = debouncedFn(500, callback)
  
  watch(
    source,
    () => {
      watchCallback()
    },
  )
  
  const clickedFn = () => {
    source.value++
  }
  
</script>

<template>
  <div>{{source}}</div>
  <button @click="clickedFn">
    点击按钮
  </button>
</template> -->


<!-- <script setup lang="ts">
import { useDebounceFn } from '@vueuse/core'
import {ref, watch} from 'vue'

const source = ref(0)
const callback = () => console.log('changed!')
const watchCallback = useDebounceFn(callback, 500)

watch(
  source,
  () => {
    watchCallback()
  },
)

const clickedFn = () => {
  source.value++
}

</script>

<template>
 <div>{{source}}</div>
  <button @click="clickedFn">
    点击按钮
  </button>
</template> -->

<script setup lang="ts">
  import { debounceFilter, watchWithFilter } from '@vueuse/core'
  import {ref} from 'vue'
  
  const source = ref(0)
  
  watchWithFilter(
    source,
    () => { console.log('changed!') }, // callback will be called in 500ms debounced manner
    {
      eventFilter: debounceFilter(500), // throttledFilter, pausabledFilter or custom filters
    },
  )
  
  const clickedFn = () => {
    source.value++
  }
  
</script>

<template>
  <div>{{source}}</div>
  <button @click="clickedFn">
    点击按钮
  </button>
</template>