<template>
  <div>
    <button class="btn btn-success float-right">
      New Asset
    </button>
    <h5>Books View</h5>

    <hr>

    <form action="" @submit.prevent="onSave">

      <b-form-group label="Book Title">
        <b-form-input v-model="book.title"></b-form-input>
      </b-form-group>
       <b-form-group label="Author">
        <b-form-input v-model="book.author"></b-form-input>
      </b-form-group>
       <b-form-group label="Description">
        <b-form-input v-model="book.Description"></b-form-input>
      </b-form-group>
       <b-form-group label="Book No.">
        <b-form-input v-model="book.no"></b-form-input>
      </b-form-group>
       <b-form-group label="Date Published">
        <b-form-input type="date" v-model="book.publish"></b-form-input>
      </b-form-group>
      <b-form-group>
        <button class="btn btn-primary" type="submit">Save Changes</button>
      </b-form-group>

    </form>
  </div>
</template>

<script>
export default {
  props: {
    book: {}
  },
  methods: {
    async onSave() {
      try {
      if(!this.book.id) {
       await this.$axios.post('/books', this.book)
      }else {
       await this.$axios.put('/books/' + this.books.id, this.book)
      }

      this.$emit('saved');
    }catch(err) {
      alert(err.response.data.message)
      }
    }
  }
}

</script>