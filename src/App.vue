<template>
  <multi-select />
</template>

<script>
import MultiSelect from './components/MultiSelect.vue'

export default {
  name: 'App',
  components: {
    MultiSelect,
  },
}
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap');
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Lato', sans-serif;
}
</style>
