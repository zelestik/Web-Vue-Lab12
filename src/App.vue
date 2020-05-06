<template>
  <div id="app">
    <h1>Записная книжка</h1>
    <phone_book></phone_book>
  </div>
</template>

<script>
import phone_book from "@/components/phone_book";
export default {
  name: 'App',
  components:{
    phone_book: phone_book
  }
}
</script>

