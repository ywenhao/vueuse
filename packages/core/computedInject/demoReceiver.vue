<script lang="ts">
import type { InjectionKey, Ref } from 'vue'
import { ref as deepRef, defineComponent } from 'vue'
import { computedInject } from './index'

type OptionsRef = Ref<{ key: number, value: string }[]>

export const ArrayKey: InjectionKey<OptionsRef> = Symbol('array')

export default defineComponent({
  name: 'DemoProvider',
  setup() {
    const computedArr = computedInject(ArrayKey, (source) => {
      if (!source)
        return deepRef([]) as OptionsRef
      const arr = [...source.value]
      arr.unshift({ key: 0, value: 'all' })
      return arr
    })

    return {
      computedArr,
    }
  },
})
</script>

<template>
  <div>
    <div text-primary font-bold mb-2>
      Computed Array
    </div>
    <pre>{{ computedArr }}</pre>
  </div>
</template>
