<template>
  <div class="list-view">
    <div v-if="hasMemo">
      <list-item
        v-for="memo in filteredMemos"
        :memo="memo"
        @remove="remove"
        @select="select">
      </list-item>
    </div>
    <div v-else>
      There is no memo.
    </div>
  </div>
</template>

<script>
import ListItem from './ListItem'
export default {
  props: {
    memos: Array,
    count: Number,
    sort: String
  },
  computed: {
    hasMemo() {
      return this.filteredMemos && this.filteredMemos.length !== 0
    },
    filteredMemos() {
      let memos = this.memos.concat()
      if (this.sort) {
        switch(this.sort) {
          case 'latest':
            memos.reverse()
        }
      }
      if (this.count) {
        memos = memos.splice(0, this.count)
      }
      return memos
    }
  },
  methods: {
    remove(id) {
      this.$emit('remove', id)
    },
    select(id) {
      this.$emit('select', id)
    }
  },
  components: {
    ListItem
  }
}
</script>
