<template>
  <div>
    <editor-view @add="add"></editor-view>
  </div>
</template>

<script>
import EditorView from '../components/EditorView'
import store from '../store'
export default {
  methods: {
    add(data) {
      store.actions.addMemo(data)
      // 追加処理のあとに`/items`にナビゲーションする
      this.$router.push({name: 'items'})
    }
  },
  components: {
    EditorView
  }
}
</script>
