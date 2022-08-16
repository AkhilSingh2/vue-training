<template>
<div>
    <div> 
        <slot name="header" :headingValue="headingValue"></slot>
    </div>
    <input ref="inputBox" v-model="headingValue">
    <button @click="destroyWatch()">
        <slot ></slot>
    </button>

</div>
</template>

<script>
import MyMixin from './myMixin'
export default {
props:{
    heading: {
        type: [String,Number],
        required: true
    },

},
mixins: [MyMixin],
computed: {
    headingValue: {
        get(){
            return this.heading
        },
        set(value) {
            this.$emit('headingChanged',value)
        }
    }
},
created(){
    this.destroyWatch = this.$watch('inputValue', (newValue, oldValue) => {
        console.log(newValue, 'newVal')
        console.log(oldValue, 'oldVal')
    })
    console.log(this.newHeading)
},
data() {
    return {
        childHeading: this.heading,
        inputValue: '',
        newHeading: 'heading old'
    }
},
methods:{
    changeHeading(){
        this.$emit('headingChanged','New Page heading')
    },
    destroyWatch() {
        this.destroyWatch()
    }
}
}
</script>

<style>

</style>