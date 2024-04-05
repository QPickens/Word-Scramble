<template>
  <div>
    <button class="btn btn-primary form-control m-1" @click="$emit ('play-button-click')">Play!</button>
  </div>
</template>
  
  <script>
    export default {
      name: 'PlayButton',
  };
  </script>

  <style scoped></style>