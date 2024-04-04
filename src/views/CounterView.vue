<!-- ***Using the Pinia store component***
<script setup>
    import { useCounterStore } from '@/stores/counter'
    const counter = useCounterStore()
</script>

<template>
<div class="about">
    <h1>
    <button @click="counter.increment()">Add</button>
    Current Count is: {{ counter.count }}
    </h1>
</div>
</template> -->
 
<script setup>
    //Import the computed object for dynamic calculation of value and watch for changes in template
    import { reactive,computed, watch } from 'vue'
    
    const appTitle = 'My Counter App'
    const counterData = reactive({
        count: 0,
        title: 'My Counter'
    }
    )
    //Methods for increasing and decreasing counter
    const increaseCounter = amount => {
        counterData.count+=amount
    }
    const decreaseCounter = amount => {
        counterData.count-=amount
    }
    //Computed variables in methods can help reduce programming inside the html section
    const oddOrEven = computed(() => {
        return (counterData.count % 2 == 0) ? 'even' : 'odd'
    })
    //watch method
    watch(() => counterData.count, (newCount) => {
        if(newCount==20)
        {
            counterData.title = 'My Counter is getting BIG!!!'
        }
    })
    //Custom component with 'mounted' hook
    //step 2: transfer to store and reuse in this file as component
    const vAutofocus = {
        mounted: (element) => {
            element.focus()
        }
    }
</script>

<template>
    <div class="counter">
        <!-- <h1>{{ counterData.title }}</h1> -->
        <h1><input v-model="counterData.title" type="text" v-autofocus></h1>
        <button @click="decreaseCounter(2)" class="btn">--</button>
        <button @click="decreaseCounter(1)" class="btn">-</button>
        <span>{{ counterData.count }}</span>
        <button @click="increaseCounter(1)" class="btn">+</button>
        <button @click="increaseCounter(2)" class="btn">++</button>
        <!-- Treated as a variable -->
        <p>The counter is {{ oddOrEven }}</p>
    </div>
</template>

<style>
@media (min-width: 1024px) {
.about {
    min-height: 100vh;
    display: flex;
    align-items: center;
}
}
</style>
  