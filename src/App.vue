<template>
  <div>
      <Navbar />
  <div class = "container-fluid">
    <About />
    <Projects />
    <Tools />
    <Contacts />
  </div>
  </div>
</template>

<script setup>
  import  Navbar from './components/Navbar.vue';
  import About from './components/About.vue';
  import Projects from './components/Projects.vue';
  import Tools from './components/Tools.vue';
  import Contacts from './components/Contacts.vue';
</script>