<template>
  <div class="home">
    <ChatWindow/>
  </div>
</template>

<script>
// @ is an alias to /src

import ChatWindow from './ChatWindow.vue'

export default {
  name: 'Home',
  components: {
    ChatWindow
  }
}
</script>
