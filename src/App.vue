<template>
  <div id="app">
    <div class="demo-container mx-auto">

      <DropdownSelect
        v-model="selectedItem"
        :items="['Broccoli', 'Lettuce', 'Peppers', 'Root vegetables', 'Cucumber', 'Parsley']"
        :searchInputPlaceholderText="'Search'"
        :focusInputOnOpen="true"
      >
      </DropdownSelect>

      <div class="mt-8 ml-4">
        Selected item: <span class="font-bold">{{selectedItem}}</span>
      </div>
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
  padding: 50px 10px;
}

html,
body {
  background-color: #EDF2F7;
}

.demo-container {
  max-width: 256px;
}

</style>
