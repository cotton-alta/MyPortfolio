<template>
  <div>
    <editList :items="items"/>
  </div>
</template>

<script>
import editList from "~/components/layouts/editList.vue"

export default {
  middleware({ store, redirect }) {
    if(!store.getters["isAuthenticated"]) {
      redirect('/')
    }
  },
  async asyncData({ app }) {
    let items = await app.$axios.$get("/api/articles")
    if(items != null) {
      items = items.reverse()
    }
    return { items }
  },
  components: {
    editList
  }
}
</script>