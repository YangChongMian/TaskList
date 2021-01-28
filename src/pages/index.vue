<template>
  <Header />
  <Item>
  </Item>
</template>

<script>
import Header from './components/PageTitle.vue'
import Item from './components/ListItem.vue'
import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    Header,
    Item
  },
  setup(){
    let details = ref('hahahah')
  }
}
</script>
