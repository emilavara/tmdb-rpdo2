<template>
  <div>
    <router-view/>
    <Footer/>
  </div>
  
</template>

<script>
import Footer from '@/components/Footer.vue'


export default {
  name: 'App',
  components: {
    Footer
  }
}
</script>


<style>
@import './css/grid-system.css';
@import './css/variables.css';
@import './css/animate.min.css'; /* animate.css */

body {
    background: var(--bgColor);
    font-family: 'SF Pro', -apple-system;
    background-size: cover;
    background-repeat: no-repeat;
    margin: 0;
    padding: 0;
    margin-bottom: 200px;
    min-height: 100vh;
}
body::-webkit-scrollbar {
    width: 5px;
}

body::-webkit-scrollbar-track {
    background: var(--bgColor);
    border-radius: 10px;
}

body::-webkit-scrollbar-thumb {
    background: var(--accentColor);
    border-radius: 10px;
}


* {
    box-sizing: border-box;
}

a {
    text-decoration: none;
}

.bg-red {
    background: red;
}

</style>
