<template>
    <div>
  <b-nav tabs align="right">
    <b-nav-item active>Active</b-nav-item>
    <b-nav-item >Disabled</b-nav-item>
  </b-nav>
</div>
</template>

<script>
export default {
    props: {
        qurrentQuestion: Object,
        next: Function,
        prev: Function
    }
}
</script>