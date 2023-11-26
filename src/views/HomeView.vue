<template>
  <div class="home">
    <p>My name is {{ name2 }} and my age is {{ age2 }}</p>
    <p ref="p">My wife name is {{ name }} and her age is {{ age }}</p>
    <button @click="handleClick">Click Me</button>
    <!-- <input type="text" v-model="name2"> -->
    <!-- =================================== -->


    <!-- Refs -->
    <h2>Refs</h2>
    <p>{{ man.name }} - {{ man.age }}</p>
    <button @click="updateMan">Update Man</button>


    <!-- Reactive -->
    <h2>Reactive</h2>
    <p>{{ woman.name }} - {{ woman.age }}</p>
    <button @click="updateWoman">Update Woman</button>


    <h2>Computed Values</h2>
    <input type="text" v-model="search">
    <p>Search term - {{ search }}</p>
    <div v-for="name in matchNames" :key="name">{{ name }}</div>

    <button @click="handleWatch">Stop Watching</button>
  </div>
</template>

<script>
import { computed } from '@vue/reactivity'
import { reactive, ref, watch, watchEffect } from 'vue'

export default {
  name: 'HomeView',
  setup() {

    const p = ref(null)
    // console.log(p, p.value)

    let name = 'Fatema' // not reactive value
    let age = 22

    const name2 = ref('Sadik') // rective value now
    const age2 = ref(29)

    const name3 = reactive('Shahadat Hossain Sadik') // primitive value //we can't use primitive value with reactive

    const handleClick = () => {
      // console.log('click me')
      console.log(p, p.value)
      p.value.classList.add('test')
      // p.value.textContent = 'Text Changed'
      name2.value = 'Shahadat'
    }

    const man = ref({ name: 'Sadik', age: 29 })
    const woman = reactive({ name: 'Fatema', age: 22 })

    const updateMan = () => {
      man.value.age = 28
    }

    const updateWoman = () => {
      woman.age = 21
    }

    const search = ref('')
    const names = ref(['Shahadat','Fatema'])

    const stopWatch = watch(search, () => {
      console.log('watch function ran')
    })

    const stopEffect = watchEffect(() => {
      console.log('watchEffect function ran', search.value)
    })

    const handleWatch = () => {
      stopWatch()
      stopEffect()
    }


    const matchNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value))
    })

    // return { name: name, age: age }
    return { name, age, handleClick, p, name2, age2, man, woman, updateMan, updateWoman, names, search, matchNames, handleClick }
  },
  // data() {
  //   return {
  //     name: 'Shahadat' // reative vale
  //   }
  // }
}
</script>
