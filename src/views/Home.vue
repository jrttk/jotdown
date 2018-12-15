<template>
  <div>
    <Header />
    <textarea
      name
      id
      v-model="noteData"
      placeholder="Just jot it down. It will be automatically save to local storage."
    ></textarea>
    <Footer />
  </div>
</template>
<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import autosize from "autosize";

export default {
  components: {
    Header, Footer
  },
  data() {
    return {
      noteData: ""
    };
  },
  async mounted() {
    if (localStorage.noteData) {
      this.noteData = await localStorage.noteData
    }
    let ta = document.querySelector('textarea')
    ta.style.display = 'none'
    await autosize(ta)
    ta.style.display = ''
    await autosize.update(ta)
  },
  watch: {
    noteData(newNoteData) {
      localStorage.noteData = newNoteData;
    }
  }
};
</script>
<style lang="scss" scoped>
textarea {
  width: 100%;
  min-height: 100px;
  height: auto;
  outline: none;
  border: 0;
  font-size: 16px;
  line-height: 1.5;
  resize: none;
}
</style>


