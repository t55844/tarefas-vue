<script >
import BookNote from './components/bookNote.vue'

export default {
  components: {
    BookNote
  }
}
sessionStorage.setItem('taskList', JSON.stringify([]))
</script>

<template >
  <div class="bg-slate-400 h-screen flex justify-around items-center ">
    <BookNote />
  </div>
</template>
