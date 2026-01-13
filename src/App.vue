<template>
  <div>
      <NavBar />
  <div class = "container-fluid">
    <About />
    <Projects />
    <Tools />
    <Contacts />
  </div>
  </div>
</template>

<script setup>
  import  NavBar from './components/NavBar.vue';
  import About from './components/About.vue';
  import Projects from './components/Projects.vue';
  import Tools from './components/Tools.vue';
  import Contacts from './components/Contacts.vue';
</script>