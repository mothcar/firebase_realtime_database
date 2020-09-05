<template>
  <q-page class="flex flex-center column">
    <div class="">
      <h6 id="bigOne"></h6>
    </div>

    <div class="">
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-gutter-md"
      >
        <q-input
          filled
          v-model="name"
          label="Your name *"
          hint="Name and surname"
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'Please type something']"
        />

        <q-input
          filled
          type="number"
          v-model="age"
          label="Your age *"
          lazy-rules
          :rules="[
            val => val !== null && val !== '' || 'Please type your age',
            val => val > 0 && val < 100 || 'Please type a real age'
          ]"
        />

        <div>
          <q-btn label="Submit" type="submit" color="primary"/>
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
        </div>
      </q-form>

    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  data () {
    return {
      name: null,
      age: null,

    }
  },


  methods: {
    onSubmit () {
      let database = firebase.database()
      let rootRef = database.ref('users')
      var autoId = rootRef.push().key
      
      var name = this.name
      var age = this.age
      // database.ref('/users'+ '0').set({
      //   name: name,
      //   age: age
      // })
      rootRef.child(autoId).set({
        name: name,
        age: age
      })
    },

    onReset () {
      this.name = null
      this.age = null
    }
  }, //methods

  mounted() {
    var bigOne = document.getElementById('bigOne')
    var dbRef = firebase.database().ref().child('text')
    dbRef.on('value', snap => bigOne.innerText = snap.val())
    console.log('Ref : ', dbRef)
  },
}
</script>
