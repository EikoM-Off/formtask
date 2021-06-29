<template>
  <div id="app" class="container">
    <h1 class="center">Форма</h1>
    <div class="formcontainer">
    <MainForm @updatePersonal="updatePers" v-show="stage == 1"/>
    <AddressForm @updatePersonal="updateAddress" @back="stage--" v-show="stage == 2"/>
    </div>
    <button class="btn" v-if="done" @click="submit_form">Отправить</button>
  </div>
</template>

<script>
import MainForm from '@/components/MainForm'
import AddressForm from '@/components/AddressForm'

export default {
  data: () => ({
    stage: 1,
    done: false,
    personal: [],
    address: []
  }),
  methods: {
    updatePers (data) {
      console.log(data)
      this.personal = data
      this.stage = 2
    },
    updateAddress (data) {
      this.address = data
      this.stage = 3
    },
    submit_form () {
      console.log('submitted')
    }
  },
  components: {
    MainForm, AddressForm
  }
}
</script>

<style lang="scss">
@import './assets/css/index.css';
</style>
