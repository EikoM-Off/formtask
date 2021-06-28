<template>
  <div class="context">
            <label class="uplabel" for="index">Индекс</label>
            <input type="text" v-model="index" id="index">

            <label class="uplabel" for="country">Страна</label>
            <input type="text" v-model="country" id="country">

            <label class="uplabel" for="region">Регион</label>
            <input type="text" v-model="region" id="region">

            <label class="uplabel" for="city">Город</label>
            <input type="text" v-model="city" id="city"
            :class="{invalid: ($v.city.$dirty && !$v.city.required)}">
            <small
              class="helper-text invalid"
              v-if="$v.city.$dirty && !$v.city.required"
            >Поле не заполнено</small>

            <label class="uplabel" for="street">Улица</label>
            <input type="text" v-model="street" id="street">

            <label class="uplabel" for="house">Дом</label>
            <input type="text" v-model="house" id="house">

    <button class="btn" @click="next">Далее</button>
  </div>

</template>

<script>
import { required } from 'vuelidate/lib/validators'

export default {
  data: () => ({
    index: '',
    country: '',
    region: '',
    city: '',
    street: '',
    house: ''
  }),
  validations: {
    city: { required }
  },
  methods: {
    next () {
      if (this.$v.$invalid) {
        this.$v.$touch()
      }
    }
  }
}
</script>
