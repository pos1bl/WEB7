<style>
p {
  color: red;
  font-weight: bold;
  text-align: center;
}

table {
  display: block;
  width: 100%;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  -ms-overflow-style: -ms-autohiding-scrollbar;
  margin: auto;
  color: #181818;
  border-collapse: separate;
  border-spacing: 0;
}

table th, td {
  padding: 5px 10px;
  border: 1px solid #000;
  color: #181818;
  white-space: nowrap;
  vertical-align: top;
}

body {
  font-family: Arial, Helvetica, sans-serif;
}

* {
  box-sizing: border-box
}

input[type=text], input[type=password], input[type=email], input[type=date] {
  width: 75%;
  padding: 15px;
  margin: 22px 0;
  display: inline-block;
  border: none;
  background: #f1f1f1;
}

label {
  width: 25%;
  padding: 15px;
  margin: 22px 0;
  display: inline-block;
  border: none;
}

.v-select {
  width: 75%;
  margin: 22px 0;
  display: inline-block;
  border: none;
  background: #f1f1f1;
}

input[type=text]:focus, input[type=password]:focus, input[type=email]:focus, input[type=date]:focus {
  background-color: #ddd;
  outline: none;
}

hr {
  border: 1px solid #f1f1f1;
  margin-bottom: 25px;
}

button {
  background-color: #4985fa;
  color: white;
  padding: 14px 20px;
  margin: 0 8px 44px 8px;
  border: none;
  cursor: pointer;
  width: 30%;
  opacity: 0.9;
}

button:hover {
  opacity: 1;
}

.container {
  padding: 16px;
}

h1 {
  text-align: center;
}
</style>

<template>
  <div class="container">
    <h1>Реєстрація</h1>
    <form class="form" id="form" novalidate onsubmit="return false;">
      <div>
        <label for="email">Пошта</label>
        <input id="email" type="email" placeholder="vlad.pos1bl@gmail.com" v-model="form.email">
        <p v-if="v$.form.email.$dirty && v$.form.email.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.email.$dirty && v$.form.email.email.$invalid"> Некоректно введена пошта </p>
        <hr>
        <label for="password">Пароль</label>
        <input id="password" type="password" placeholder="********" v-model="form.password">
        <p v-if="v$.form.password.$dirty && v$.form.password.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.password.$dirty && v$.form.password.minValue.$invalid"> Мінімум 8 символів </p>
        <hr>
        <label for="surname">Прізвище</label>
        <input id="surname" type="text" placeholder="Orlenko" v-model="form.surname">
        <p v-if="v$.form.surname.$dirty && v$.form.surname.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.surname.$dirty && v$.form.surname.alpha.$invalid"> Використовуйте лише літери англійського
          алфавіту</p>
        <hr>
        <label for="name">Ім'я</label>
        <input id="name" type="text" placeholder="Vladyslav" v-model="form.name"/>
        <p v-if="v$.form.name.$dirty && v$.form.name.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.name.$dirty && v$.form.name.alpha.$invalid"> Використовуйте лише літери англійського
          алфавіту </p>
        <hr>
        <label for="fatherName">По-батькові</label>
        <input id="fatherName" type="text" placeholder="Ivanovich" v-model="form.fatherName"/>
        <p v-if="v$.form.fatherName.$dirty && v$.form.fatherName.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.fatherName.$dirty && v$.form.fatherName.alpha.$invalid"> Використовуйте лише літери
          англійського алфавіту </p>
        <hr>
        <label for="date">Дата народження</label>
        <input id="date" type="date" v-model="form.date">
        <p v-if="v$.form.date.$dirty && v$.form.date.required.$invalid"> Пустий інпут </p>
        <p v-if="new Date(Date.parse(form.date)) < new Date(Date.parse('1990-01-01')) ||
                 new Date(Date.parse(form.date)) > new Date(Date.parse('2005-12-31'))"
        > Виберіть дату з 1990-01-01 до 2005-12-31 </p>
        <hr>
        <label for="phoneNumber">Номер телефону</label>
        <input id="phoneNumber" type="text" data-validate-field="phone" v-model="form.phoneNumber"
               v-mask="'38(0##)###-##-##'" placeholder="38(0__)___-__-__">
        <p v-if="v$.form.phoneNumber.$dirty && v$.form.phoneNumber.required.$invalid"> Пустий інпут </p>
        <p v-if="v$.form.phoneNumber.$dirty && v$.form.phoneNumber.minLength.$invalid"> Некоректно введений номер </p>
        <hr>
        <label for="group">Оберіть групу:</label>
        <v-select id="group" class="v-select" :options="groups" v-model="form.group"></v-select>
        <p v-if="v$.form.group.$dirty && v$.form.group.required.$invalid"> Пустий інпут </p>
        <hr>
        <label for="sex">Оберіть стать:</label>
        <v-select id="sex" class="v-select" :options="sexes" v-model="form.sex"></v-select>
        <p v-if="v$.form.sex.$dirty && v$.form.sex.required.$invalid"> Пустий інпут </p>
        <hr>
        <button @click="submit">Додати</button>
        <button @click="deletee">Видалити</button>
        <button @click="copy">Копіювати</button>
      </div>
    </form>
    <div>
      <table>
        <tr>
          <th>Прізвище</th>
          <th>Ім'я</th>
          <th>По-батькові</th>
          <th>Номер телефону</th>
          <th>Пароль</th>
          <th>Дата народження</th>
          <th>Пошта</th>
          <th>Група</th>
          <th>Стать</th>
        </tr>
        <tr v-for="(tr, index) in table">
          <td v-for="td in tr">{{ td }}</td>
          <td><input type="checkbox" v-model="check[index][1]"></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import {email, required, minLength, alpha} from '@vuelidate/validators'
import vSelect from "vue-select";
import 'vue-select/dist/vue-select.css'
import {mask} from 'vue-the-mask'


export default {
  setup() {
    return {v$: useVuelidate()}
  },

  props: {},
  components: {
    vSelect,
  },
  directives: {
    mask
  },
  data() {
    return {
      groups: [
        'ІА-11',
        'ІА-12',
        'ІА-13',
        'ІА-14',
      ],
      sexes: [
        'Хлопець',
        'Дівчина',
        'Інше'
      ],
      check: [],
      table: [],
      form: {
        surname: '',
        name: '',
        fatherName: '',
        phoneNumber: '',
        password: '',
        date: '',
        email: '',
        group: '',
        sex: ''
      },
    }
  },
  validations: {
    form: {
      surname: {required, alpha},
      name: {required, alpha},
      fatherName: {required, alpha},
      password: {required, minValue: minLength(8)},
      sex: {required},
      date: {required},
      group: {required},
      email: {required, email},
      phoneNumber: {required, minLength: minLength(16)}
    }
  },
  methods: {
    submit() {
      if (this.v$.form.$invalid || new Date(Date.parse(this.form.date)) < new Date(Date.parse('1990-01-01')) ||
          new Date(Date.parse(this.form.date)) > new Date(Date.parse('2022-12-31'))) {
        this.v$.form.$touch()
      } else {
        this.add()
      }
    },

    add() {
      this.table.push([])
      for (let input in this.form) {
        let formInput = this.form[input];
        this.table[this.table.length - 1].push(formInput);
      }
      this.check.push([this.table.length - 1, false]);
      this.v$.$reset()
    },

    deletee() {
      for (let i = 0; i < this.check.length; i++) {
        if (this.check [i][1] === true) {
          this.table.splice(i, 1);
          this.check.splice(i, 1);
          i--;
        }
      }
    },
    copy() {
      for (let i = 0; i < this.check.length; i++) {
        if (this.check[i][1] === true) {
          this.check[i][1] = false;
          this.check.push([this.table.push(this.table[i]) - 1, false]);
        }
      }
    },
  },
}
</script>