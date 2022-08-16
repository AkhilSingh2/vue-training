<template>
  <div id="app">
    <!-- <new-component :allNames="names" />
    <Table /> -->
    <component-new :heading="heading" @headingChanged="heading = $event" ref="childComponent">
      <template #header="slotProps">
        {{ slotProps.headingValue }}
      </template>
    </component-new>
    <button @click="printRefValue()">Print Ref</button>
  </div>
</template>

<script>
import New from './components/New.vue'
import Table from './components/Table.vue'
import Component from './components/component.vue'
export default {
  name: 'App',
  components: {
    'new-component': New,
    Table,
    'component-new': Component
  },
  mounted(){
    
  },
  data() {
    return {
      names: ['Akhil', 'Vishal'],
      heading: 'Page Heading'
    }
  },
  methods: {
    printRefValue(){
      console.log('refs Value',this.$refs.childComponent.headingValue)
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
