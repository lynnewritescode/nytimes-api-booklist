<template>
  <div class="container">
    <h1>New York Times bestseller's list</h1>
    <ul>
      <li v-for="(book, i) in books" :key="i">
        <a :href="book.amazon_product_url" class="book">
          <img :src="book.book_image" class="thumb" />
          <div class="text">
            <h2 class="title">
              {{ book.title }}
            </h2>
            <p class="author">{{ book.author }}</p>
            <p class="description">{{ book.description }}</p>
            <button class="btn">View on Amazon</button>
          </div>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'BookListing',
  data() {
    return {
      books: []
    };
  },
  mounted() {
    this.fetchBooks();
  },
  methods: {
    async fetchBooks() {
      let context = this;
      axios
        .get(
          'https://api.nytimes.com/svc/books/v3/lists/current/hardcover-fiction.json?api-key=4Z5yWw2xmGTlT9e1JiSlIx378BnpWAkm'
        )
        .then(function(response) {
          context.books = response.data.results.books;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 5%;
}

.book {
  width: 100%;
  display: flex;
  text-align: left;
  color: #1d1d1d;
  padding: 40px 0;
  text-decoration: none;
  border-bottom: 1px solid #eee;

  .thumb {
    width: 100%;
    margin-right: 30px;
    flex-basis: 150px;
    max-width: 150px;
    flex-shrink: 0;
    flex-grow: 0;
  }

  .text {
    flex-basis: calc(100% - 180px);
    max-width: calc(100% - 180px);
    flex-shrink: 0;
    flex-grow: 0;
  }

  .title {
    color: #1d1d1d;
    margin-bottom: 5px;

    &:hover {
      color: #42b983;
    }
  }

  .author {
    margin-top: 0;
    font-weight: 700;
  }
}

.btn {
  border: 0;
  margin-top: 10px;
  color: #fff;
  font-weight: 600;
  padding: 12px 30px;
  border-radius: 3px;
  background: #42b983;
  cursor: pointer;
  text-transform: uppercase;
  transition: background 0.2s ease-in-out;

  &:hover {
    background: darken(#42b983, 5%);
  }
}

a {
  transition: color 0.3s ease-in-out;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
li {
  display: inline-block;
  margin: 0;
  width: 100%;
}
</style>
