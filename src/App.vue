<template>
<div class="app">
  <Header/>
  <Todos/>
</div>
</template>

<script>
import Header from "@/components/Header";
import Todos from "@/components/Todos";



export default {
  name: 'App',
  components:
{Header,Todos}

}
</script>

<style>

</style>
