<template>
  <q-page padding>
  </q-page>
     <q-table
      title="Treats"
      :rows="posts"
      :columns="columns"
      row-key="name"
    />
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import { api } from 'boot/axios'

export default defineComponent({
  name: 'IndexPage',
  setup () {
    const posts = ref([])
    const columns = [
      { name: 'id', field: 'id', label: 'Id', sortable: true, align: 'left' },
      { name: 'title', field: 'title', label: 'Título', sortable: true, align: 'left' },
      { name: 'author', field: 'author', label: 'Autor', sortable: true, align: 'left' }
    ]

    onMounted(() => {
      getPosts()
    })

    const getPosts = async () => {
      try {
        const response = await api.get('http://localhost:3000/posts')
        console.log(response)
      } catch (error) {
        console.error(error)
      }
    }

    return {
      posts,
      columns
    }
  }
})
</script>
