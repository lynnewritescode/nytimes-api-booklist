<template>
  <div class="home">
    <BookListing />
  </div>
</template>

<script>
// @ is an alias to /src
import BookListing from '@/components/BookListing.vue';

export default {
  name: 'Home',
  components: {
    BookListing
  }
};
</script>
