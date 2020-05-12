<template>
  <div id="app">
    <DropdownSelect
      :items="['Broccoli', 'Lettuce', 'Peppers', 'Root vegetables', 'Cucumber', 'Parsley']"
    >
    </DropdownSelect>
  </div>
</template>

<script>
import DropdownSelect from './components/DropdownSelect.vue'

export default {
  name: 'App',
  components: {
    DropdownSelect
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;600&display=swap');

#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 50px;
}

html,
body {
  background-color: #EDF2F7;
}

</style>
