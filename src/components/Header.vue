<template>
    <div>
  <b-nav tabs align="right">
    <b-nav-item active>{{Math.min(Math.max(parseInt(index), 0), 10)}}/{{questions.length}}</b-nav-item>
    <!-- <b-nav-item >qorrect questions {{this.countcorrect}}</b-nav-item> -->
  </b-nav>
</div>
</template>

<script>

export default {

    props: {
        qurrentQuestion: Object,
        next: Function,
        prev: Function,
        index: null,
        questions: Array,
        
    },
    date() {
      return {
        
      }
    }
}
</script>