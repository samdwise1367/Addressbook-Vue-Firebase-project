<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Addressbook with Vue and Firebase</h1>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Contact Lists</h3>
      </div>
    </div>

      <div class="panel panel-default">
        <div class="panel-heading"></div>
          <h3> Add Contact</h3>
      </div>

      <div class="panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="addContact">
          <div class="form-group">
            <label for="firstname">Firstname:</label>
            <input type="text" id="firstname" class="form-control" v-model="newContact.firstname">
          </div>

          <div class="form-group">
            <label for="lastname">Lastname:</label>
            <input type="text" id="lastname" class="form-control" v-model="newContact.lastname">
          </div>

          <div class="form-group">
            <label for="age">Age:</label>
            <input type="text" id="age" class="form-control" v-model="newContact.age">
          </div>

          <div class="form-group">
            <label for="website">Website:</label>
            <input type="text" id="website" class="form-control" v-model="newContact.website">
          </div>
          <input type="submit" class="btn btn-primary" value="Add Contact" v-on:submit.prevent="addContact">

        </form>
      </div>

      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Firstname</th>
              <th>Lastname</th>
              <th>Age</th>
              <th>Website</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="contact in contacts">
              <td>{{contact.firstname}}</td>
              <td>{{contact.lastname}}</td>
              <td>{{contact.age}}</td>
               <td>{{contact.website}}</td>
             
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    
  </div>
</template>

<script>
import Firebase from 'firebase'

let config = {
    apiKey: "AIzaSyBxar6nMLQNhgG8dts9vEU0sSaPNRipqR0",
    authDomain: "adressbook-36210.firebaseapp.com",
    databaseURL: "https://adressbook-36210.firebaseio.com",
    projectId: "adressbook-36210",
    storageBucket: "adressbook-36210.appspot.com",
    messagingSenderId: "545212149499"
}

let app = Firebase.initializeApp(config);
let db = app.database();

let contactRef = db.ref('contacts');

export default {
  name: 'app',
  firebase:{
    contacts: contactRef

  },
  data(){
    return{
      newContact :{
        firstname:'',
        lastname:'',
        age:'',
        website:''
      }
    }
  },
  methods:{
    addContact: function(){
      if(this.newContact.firstname =='' || this.newContact.lastname =='' || this.newContact.age =='' || this.newContact.website ==''){
        alert("Field cannot be empty");
      }else{
        contactRef.push(this.newContact);
        this.newContact.firstname ='';
        this.newContact.last ='';
        this.newContact.age ='';
        this.newContact.website ='';
      }
      
      
    }
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
