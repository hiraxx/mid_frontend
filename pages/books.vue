<template>
  <div>
     <NavBar />
    <div class='container'>
    <h1> Books </h1>
    <div class="row">
      <div class="col-6">
        <h5>List of Books</h5>
        <ul class="list group">
          <li class="list-group-item list-group-item-action" v-for="books in books" :key="books.id">
            {{books.name}} <span class="float-right">{{books.value}}</span>
          </li>
        </ul>
      </div>
      <div class="col-4">
        <BooksView :book="selectedBook" @saved="onSave" />
      </div>
    </div>
  </div>
</div>

</template>
      
<script>
  export default {
    data() {
      return {
        books: [],
        selectedBook: {}

      }
    },
    methods: {
      async getMyBooks() {
        await this.$axios.get('/Books' )
        .then((res)=>{
          if(res.status==200) {
            this.books = res.data
          }
        })
      },
      onSave() {
        this.getMyBooks()
      }
    },
    created() {
      this.getMyBooks()
      
    }
  }
      </script>