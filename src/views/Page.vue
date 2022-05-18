<template>
      <main class="main">
    <div class="container">
      <article class="counter">
        <header-page></header-page>
        <my-form ></my-form>

      </article>
    </div>
  </main>
</template>
<script>
import { defineComponent } from '@vue/composition-api'
// import { Options } from 'vue-class-component'
import MyForm from '@/components/Form.vue'

import HeaderPage from '@/components/Header.vue'
// import { Result } from '@/components/Result.vue'

export default defineComponent({
  name: 'main-page',
  components: { MyForm, HeaderPage }
})
</script>
