<template>
  <div class="popup" v-if="toggle" @click.self="close">
    <div class="popup__body">
      <button class="btn__close" @click="close"><img src="../../assets/img/close.svg" alt="close"></button>
      <div class="wrap-form">
        <div v-if="thanks" class="thanks">Спасибо!</div>
        <div class="errors" v-if="errors.length != 0">
          <div class="errors__item" v-for="item in errors">{{ item }}</div>
        </div>
        <form action="" class="form">
          <input
              v-model.trim="email"
              type="email"
              class="form__text"
              placeholder="Введите email"
          >
          <button class="btn__send" @click.prevent="send">Отправить</button>
        </form>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    props: ['toggle'],
    emit: ['close'],
    data() {
      return {
        thanks: false,
        email: '',
        errors: []
      }
    },
    methods: {
      close() {
        this.$emit('close')
      },
      async send() {
        this.errors = [];
        console.log(this.email)
        if (!this.email) {
          this.errors.push('Укажите электронную почту.');
        } else if (!this.validEmail(this.email)) {
          this.errors.push('Укажите корректный адрес электронной почты.');
        }


        await setTimeout(() => {
          if (!this.errors.length) {
            this.thanks = true
            setTimeout(() => {
              this.$emit('close')
              this.thanks = false
              this.email = ''
            }, 2000)
          }
        }, 1000)

      },
      validEmail(email) {
        let re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(email);
      }
    }
  }
</script>

<style scoped>

</style>