<template>
  <div id="app">
    <DropdownSelect
      v-model="selectedItem"
      :items="['Broccoli', 'Lettuce', 'Peppers', 'Root vegetables', 'Cucumber', 'Parsley']"
      :searchInputPlaceholderText="'Search'"
      :focusInputOnOpen="true"
    >
    </DropdownSelect>
    <div class="mt-4">
      {{selectedItem}}
    </div>
  </div>
</template>

<script>
import DropdownSelect from './components/DropdownSelect.vue'

export default {
  name: 'App',
  components: {
    DropdownSelect
  },
  data() {
    return {
      selectedItem: ''
    }
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
