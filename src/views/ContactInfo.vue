<template>
  <div>
    <h2>Добавьте новое поле</h2>
    <div>
      <div class="field-group" v-for="(item, index) in items" v-bind:key="item">
        <div class='title'
             contenteditable='true'
             tabindex='0'
             :title='messages.editTitle'
             @paste='updateItem(index)'
             @blur='updateItem(index)'
             @keyup='updateItem(index)'
             @delete='updateItem(index)'>{{ item.title }}</div>
        <input type="text" class="text" tabindex='0' :title='messages.editText' v-model="item.text">
        <button class='btn btn-red' :title='messages.delete' @click="visible=true">Удалить поле</button>
      </div>
      <div v-for="item in items" v-bind:key="item">
        <ModalAlert
            v-show="visible"
            @close="visible=!visible"
            @click="deleteItem(item)"
        />
      </div>
    </div>
    <button type="button" class="btn btn-default" @click="createField">Добавить поле</button>
  </div>
</template>

<script>
import ModalAlert from '../components/ModalAlert'
export default {
  name: 'ContactInfo',
  data () {
    return {
      items: [],
      visible: false,
      messages: {
        delete: 'Delete this item',
        editTitle: 'Edit title',
        editText: 'Edit text'
      }
    }
  },
  methods: {
    createField() {
      this.items.push({
        title: 'Title: ',
        text: ''
      });
    },
    deleteItem(item) {
      let index = this.items.indexOf(item);
      this.items.splice(index, 1);
    },
    updateItem(index) {
      this.items[index].title = this.$el.querySelector('.title').innerText;
      this.items[index].text  = this.$el.querySelector('.text').innerText;
    }
  },
  components: {
    ModalAlert
  }
}
</script>

<style>
  .field-group {
    margin-top: 20px;
    text-align: left;
    border: 1px solid #ddd;
    padding: 20px;
  }
  .field-group input {
    width: 250px;
    height: 35px;
  }
  .title {
    width: 100%;
    margin-right: 10px;
  }
  input, div, button:focus {
    outline: none;
  }
</style>
