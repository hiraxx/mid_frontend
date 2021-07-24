<template>
  <div>
    <h1> Books </h1>
       <NavBar/>
    <EditBookModal :book="selectedBook"/>
    <DeleteBookModal :book="selectedBook" @onDeleteEntry="getAll" />
    <div class="container mt-2">
      
        <h1>
          <BookEntryModal class="float-right mb-2" @onAddEntry="getAll"/>
          Books
          </h1>
      <table class="table table-striped">
        <thead class="bg-primary text-light">
          <th>Title</th>
          <th>Author</th>
          <th>Description</th>
          <th>Book No</th>
          <th>Date Published</th>
          <th>&nbsp;</th>
          <th>&nbsp;</th>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id">
            <td>{{book.title}}</td>
            <td>{{book.author}}</td>
            <td>{{book.description}}</td>
            <td>{{book.book_no}}</td>
            <td>{{book.date_published}}</td>
            <td>
              <b-button @click="onEdit(book)" variant="info" size="sm">Edit</b-button>
            </td>
            <td>
              <b-button @click="onDelete(book)" variant="danger" size="sm">Delete</b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      books: [],
      selectedBook: {}
    }
  },
  methods: {
    async getAll(){
      await this.$axios.get('/api/books')
      .then((res)=>{
        if(res.status==200){
          this.books = res.data
        }
      })
    },
    onEdit(selectedBook){
      this.selectedBook = selectedBook
      this.$bvModal.show('editBookModal')
    },
    onDelete(selectedBook){
      this.selectedBook = selectedBook
      this.$bvModal.show('deleteBookModal')
    }
  },
  created(){
    this.getAll()  
  }
}
</script>

<style>

</style>