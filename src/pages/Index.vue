<template>
  <q-page class="flex flex-center">
    <div class="">
      <h1 >title</h1>
      <h6 id="bigOne"></h6>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  methods: {

  },

  mounted() {
    var bigOne = document.getElementById('bigOne')
    var dbRef = firebase.database().ref().child('text')
    dbRef.on('value', snap => bigOne.innerText = snap.val())
    console.log('Ref : ', dbRef)
  },
}
</script>
