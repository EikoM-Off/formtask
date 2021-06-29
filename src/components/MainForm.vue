<template>
  <div class="context shadow">
    <div class="progress">
      <div class="determinate" style="width: 33%"></div>
    </div>

    <h2 class="center">Персональные данные</h2>
    <div>
            <label class="uplabel" for="surname">Фамилия*</label>
            <input type="text" v-model="surname" id="surname"
            :class="{invalid: ($v.surname.$dirty && !$v.surname.required)}">
            <small
              class="helper-text right invalid"
              v-if="$v.surname.$dirty && !$v.surname.required"
            >Поле не заполнено</small>
            <small
              class="helper-text right invalid"
              v-if="$v.surname.$dirty && !$v.surname.alpha"
            >Фамилия должна состоять из букв</small>

            <label class="uplabel" for="surname">Имя*</label>
            <input type="text" v-model="name" id="name"
            :class="{invalid: ($v.name.$dirty && !$v.name.required)}">
            <small
              class="helper-text right invalid"
              v-if="$v.name.$dirty && !$v.name.required"
            >Поле не заполнено</small>
            <small
              class="helper-text right invalid"
              v-if="$v.name.$dirty && !$v.name.alpha"
            >Имя должно состоять из букв</small>

            <label class="uplabel" for="midname">Отчество</label>
            <input type="text" v-model="midname" id="midname"
            :class="{invalid: ($v.midname.$dirty)}">
            <small
              class="helper-text right invalid"
              v-if="$v.midname.$dirty && !$v.midname.alpha"
            >Отчество должно состоять из букв</small>

            <label class="uplabel" for="birth">Дата рождения*</label>
            <input type="date" v-model="birth" id="birth"
            value="2000-01-01"
            min="1900-01-01" max="2020-12-31"
            :class="{invalid: ($v.birth.$dirty && !$v.birth.required)}">
            <small
              class="helper-text right invalid"
              v-if="$v.birth.$dirty && !$v.birth.required"
            >Поле не заполнено</small>

            <label class="uplabel" for="birth">Телефон*</label>
            <input type="tel" v-model="phone" id="phone" maxlength="12"
            value="+7"
            pattern="\+7\s?[0-9]{10}"
            placeholder="+7"
            :class="{invalid: ($v.phone.$dirty && !$v.phone.required)}">
            <small
              class="helper-text right invalid"
              v-if="$v.phone.$dirty && !$v.phone.required"
            >Поле не заполнено</small>
            <small
              class="helper-text right invalid"
              v-else-if="$v.phone.$dirty && !$v.phone.maxLength"
            >Номер слишком длинный</small>
            <small
              class="helper-text right invalid"
              v-else-if="$v.phone.$dirty && !$v.phone.minLength"
            >Номер слишком короткий</small>
            <small
              class="helper-text right invalid"
              v-else-if="$v.phone.$dirty && !$v.phone.numeric"
            >Номер состоит только из цифр</small>

            <label class="uplabel" for="region">Пол</label>
            <input type="text" v-model="gender" id="gender">

            <label class="uplabel" for="birth">Группа клиентов*</label>
            <input type="text" v-model="customer_group" id="customer_group"
            :class="{invalid: ($v.customer_group.$dirty && !$v.customer_group.required)}">
            <small
              class="helper-text right invalid"
              v-if="$v.customer_group.$dirty && !$v.customer_group.required"
            >Поле не заполнено</small>

    </div>

    <div class="formfooter">
      <button class="btn right" @click="next">Далее</button>
    </div>

  </div>

</template>

<script>
import { required, minLength, maxLength, alpha, numeric } from 'vuelidate/lib/validators'

export default {
  data: () => ({
    surname: '',
    name: '',
    midname: '',
    birth: '',
    phone: '',
    gender: '',
    customer_group: '',
    att_doctor: '',
    send_sms: false
  }),
  validations: {
    surname: { required, alpha }, // принимает только латиницу
    name: { required, alpha },
    midname: { alpha },
    birth: { required },
    phone: { required, minLength: minLength(12), maxLength: maxLength(12), numeric }, // доработать
    customer_group: { required }
  },
  methods: {
    next () {
      if (this.$v.$invalid) {
        this.$v.$touch()
        return
      }
      console.log(this._data)
      this.$emit('updatePersonal', {
        personal: this._data
      })
    }
  }
}
</script>
