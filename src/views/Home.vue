<template>
  <img alt="Vue logo" src="../assets/logo.png">
  <hr>
  <form class="form-class" v-on:submit.prevent="createContact">
    <div>
      <label for="name">Имя</label>
      <input type="text" id="name" autocomplete="off" v-model="form.name">
    </div>
    <div>
      <label for="lastName">Фамилия</label>
      <input type="text" id="lastName" autocomplete="off" v-model="form.lastName">
    </div>
    <button type="submit" class="btn btn-blue" :disabled="!canCreate">Создать контакт</button>
  </form>

    <div v-if="contacts.length">
      <div class="card-class" v-for="contact in contacts" v-bind:key="contact.id">
        <div class="body">
          <div class="card-body">
            <h2>Имя: {{contact.name}}</h2>
            <p>Фамилия: {{contact.lastName}}</p>
          </div>
          <div class="btn-group">
            <router-link to="/contactInfo" class="btn btn-default">Посмотреть информацию</router-link>
            <button class="btn btn-red" @click="visible=true">Удалить контакт</button>
          </div>
        </div>
      </div>
      <div v-for="contact in contacts" v-bind:key="contact.id">
        <ModalAlert
            v-bind:form="form"
            v-show="visible"
            @close="visible=!visible"
            @click="removeContact(contact.id)"
        />
      </div>
    </div>
    <p v-else>Контактов пока нет</p>

</template>

<script>
import ModalAlert from '../components/ModalAlert'
export default {
  name: 'Home',
  data () {
    return {
      form: {
        name: '',
        lastName: ''
      },
      contacts: [],
      visible: false
    }
  },
  computed: {
    canCreate () {
      return this.form.name.trim() && this.form.lastName.trim()
    }
  },
  methods: {
    createContact () {
      const { ...contact } = this.form
      this.contacts.push({ ...contact, id: Date.now() })
      this.form.name = this.form.lastName = ''
    },
    removeContact (id) {
      this.contacts = this.contacts.filter(contact => contact.id !== id)
    }
  },
  components: {
    ModalAlert
  }
}
</script>

<style>
  .form-class {
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
  .form-class div {
    margin-right: 20px;
  }
  .form-class div label {
    display: block;
    text-align: left
  }
  .form-class input {
    width: 250px;
    height: 35px;
  }
  .btn {
    width: 130px;
    height: 40px;
    margin-top: 18px;
    cursor: pointer;
    border: none;
    border-radius: 3px;
  }
  .btn-blue {
    background: #5564a9;
    color: #fff;
  }
  .btn-red {
    background: #ec2e2e;
    color: #fff;
  }
  .card-class {
    border: 1px solid #ccc;
    padding: 20px;
    margin-top: 30px;
  }
  .btn-group {
    display: flex;
  }
  .btn-default {
    margin-right: 20px;
    text-decoration: none;
    background: #ccc;
    color: #fff;
  }
  .card-body {
    text-align: left;
  }
</style>
