<template>
  <div id="box" class="wrapper">
    <TransitionGroup name="timers-list">
      <Timer v-for="index in countComponents" :key="index"/>
      <AddButton @click="addElement()" :key="'addBtn'"/>
    </TransitionGroup>
  </div>
</template>

<script>
import { Timer, AddButton } from './components';
export default {
  name: 'App',
  components: {
    Timer, AddButton
  },
  data() {
    return {
      countComponents: 1
    }
  },
  methods: {
    addElement(){
      this.countComponents+=1
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/styles/main.scss';
</style>


