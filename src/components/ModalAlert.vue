<template>
  <div class="modal-backdrop">
    <div class="modal">
      <section class="modal-body">
        <slot name="body" v-bind="form">
          {{`Вы действительно хотите удалить ${form ? 'контакт' : 'поле'}?`}}
        </slot>
      </section>
      <footer class="modal-footer">
        <slot name="footer">
          <button
            type="button"
            class="btn-delete"
            @click="close"
          >
            {{`Удалить ${form ? 'контакт' : 'поле'}`}}
          </button>
        </slot>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modal',
  props: ['form'],
  methods: {
    close () {
      this.$emit('close')
    }
  }
}
</script>

<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: #FFFFFF;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  justify-content: flex-end;
  padding: 20px;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-delete {
  color: white;
  background: #ec2e2e;
  border: 1px solid #4AAE9B;
  border-radius: 2px;
  height: 35px;
}
</style>
