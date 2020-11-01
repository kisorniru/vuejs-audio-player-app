<template>
  <div id="app">
    <header>
      <h1>My Audio</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="audio-title">{{ current.title }}</h2>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  
  data () {
    return {
      current: {
        title: 'Audio Title',
      },
    }
  },
  methods: {
    // 
  },
}
</script>

<style>

  /*  */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: sans-serif;
  }

  header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #FFF;
  }


</style>
