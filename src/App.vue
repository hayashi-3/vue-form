<template>
  <div>
  <form name="contact" netlify netlify-honeypot="bot-field" hidden>
  <form v-if="isSubmit === false" @submit.prevent="onSubmit">
    <input type="text" v-model="name" name="name" >
    <input type="email" v-model="email" name="email">
    <textarea v-model="content" name="content"></textarea>

    <button type="submit">送信</button>
  </form>

  <div v-if="isSubmit === true">
    <p>サンクス</p>
  </div>

</div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      name: '',
      email: '',
      content: '',
      isSubmit: false
    }
  },
  methods: {
    onSubmit() {
      const params = new URLSearchParams()

      params.append('form-name', 'contact') // Forms使うのに必要

      params.append('name', this.name)
      params.append('email', this.email)
      params.append('content', this.content)

      axios
        .post('/', params)
        .then(() => {
          this.isSubmit = true
        })
    }
  }
}
</script>
