<script lang="ts">
import PouchDB from 'pouchdb'

export default {
  data() {
    return {
      datas: [],
      databaseReference: null
    }
  },

  methods: {
    inc() {},

    initDatabase() {
      const db = new PouchDB('http://localhost:5984/database')
      if (db) {
        this.databaseReference = db
        this.fetchData()
        return
      } else {
        console.log('invalide')
      }
    },

    fetchData() {
      this.databaseReference.db
        .allDocs({
          include_docs: true,
          attachments: true
        })
        .then(function (result) {
          // handle result
        })
        .catch(function (err) {
          console.log(err)
        })
    }
  },

  mounted() {
    this.initDatabase()
  }
}
</script>

<template>
  <h1>InfraDon2</h1>
  <p>Counter: {{ datas }}</p>
  <button type="button" role="button" @click="inc">+1</button>
</template>
