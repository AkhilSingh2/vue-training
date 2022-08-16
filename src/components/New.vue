<template>
  <div>
      <div @click="fullNameRender()"> Print full name</div>
      <div>
          {{ firstName}}
      </div>
      <div>
          {{lastName}}
      </div>
      <div>
          {{ fullName}}
      </div>
  </div>
</template>

<script>
export default {
    props:['allNames'],
    data(){ 
        return {
            firstName: 'Akhil',
            lastName: 'Singh',
            fullName: ''
        }
    },
    methods:{
        fullNameRender() {
            this.firstName = 'Akhilendra'
        }
    },
    computed:{
        makeFullName() {
            return this.firstName + this.lastName
        }
    },
    watch: {
        firstName() {
            this.fullName = this.firstName + this.lastName
        },
        lastName() {
            this.fullName = this.firstName + this.lastName
        }
    },
    beforeCreate(){
        console.log('before Create')
        // console.log(this.allNames)
    },
    created() {
        console.log('created')
        console.log(this.allNames)
    },
    beforeMount(){
        console.log('before mMount')
        console.log(this.allNames)
    },
    mounted(){
        console.log('mounted')
    }

}
</script>

<style>

</style>