<template>
<HeaderNavBar />
<MainContainer />
<FooterBar />
</template>

<script>
import HeaderNavBar from './components/HeaderNavBar.vue';
import FooterBar from './components/FooterBar.vue';
import MainContainer from './components/MainContainer.vue';
export default {
  name: 'App',
  components: { 
    HeaderNavBar, 
    FooterBar, 
    MainContainer 
  },
};
</script>

<style>
header, 
footer{
  background-color: #3f7cad;
}
</style>
