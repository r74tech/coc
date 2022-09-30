<template>
  <section class="section">

  <div class="container">
    <h1 class="title">
      CoC マニア検索
    </h1>

    <input
      v-model="search"
      type="text"
      class="input "
      placeholder="Search"
    >
    <div class="result-list is-flex is-flex-direction-column is-6" style="gap:1.5em">
      <p v-if="noResults">
        Sorry, no results for {{ search }}
      </p>
      <p v-if="search === ''">
        Try searching manias of the Bible via the input above.
      </p>
      <div
        v-for="(mania, i) in results"
        :key="i"
      >
        <div class="is-size-4">
          {{ mania.name }}マニア
        </div>
        <div>
          {{ mania.description }}
        </div>
      </div>
    </div>
  </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, Ref, ref } from 'vue'
import { useVueFuse } from 'vue-fuse'
import { Mania, manias } from './assets/mania'
export default defineComponent({
  name: 'App',
  setup () {
    const list: Ref<null | Array<Mania>> = ref(null)
    setTimeout(() => {
      list.value = manias
    }, 1000)
    const { search, results, noResults } = useVueFuse(list, {
      keys: [
        { name: 'name', weight: 2 },
        { name: 'description', weight: 1 },
      ],
    })
    return {
      search,
      results,
      noResults,
    }
  },
})
</script>

<style scoped>
</style>