<template>
  <div>
    <label>Город:</label>
    <select v-model="selectedCity" @change="updateShopSelectOptions">
      <option value="">Выберите город</option>
      <option v-for="option in cityOptions" :key="option" :value="option">{{ option }}</option>
    </select>

    <label>Цех:</label>
    <select v-model="selectedShop" @change="updateEmployeeSelectOptions">
      <option value="">Выберите цех</option>
      <option v-for="option in shopOptions" :key="option" :value="option">{{ option }}</option>
    </select>

    <label>Сотрудник:</label>
    <select v-model="selectedEmployee">
      <option value="">Выберите сотрудника</option>
      <option v-for="option in employeeOptions" :key="option" :value="option">{{ option }}</option>
    </select>

    <label>Бригада:</label>
    <select v-model="selectedTeam">
      <option value="">Выберите бригаду</option>
      <option v-for="option in teamOptions" :key="option" :value="option">{{ option }}</option>
    </select>

    <label>Смена:</label>
    <select v-model="selectedShift">
      <option value="">Выберите смену</option>
      <option v-for="option in shiftOptions" :key="option" :value="option">{{ option }}</option>
    </select>

    <button class='btn' @click="saveCookie('myCookie', optionsObject, 1)" >Save Cookie</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedCity: '',
      selectedShop: '',
      selectedEmployee: '',
      selectedTeam: '',
      selectedShift: '',
      cityOptions: ['Almaty', 'Astana', 'Shymkent'],
      teamOptions: ['Бригада №1', 'Бригада №2', 'Бригада №3'],
      shiftOptions: ['Первая', 'Вторая'],
      shopOptions: [],
      employeeOptions: []
    };
  },
  computed: {
    optionsObject() {
      return {
        "Город": this.selectedCity,
        "Цех": this.selectedShop,
        "Сотрудник": this.selectedEmployee,
        "Бригада": this.selectedTeam,
        "Смена": this.selectedShift,
      };
    },
  },
  methods: {
    updateShopSelectOptions() {
      setTimeout(() => {
        switch (this.selectedCity) {
          case 'Almaty':
            this.shopOptions = ['Цех #1 Almaty', 'Цех #2 Almaty'];
            break;
          case 'Astana':
            this.shopOptions = ['Цех #1 Astana', 'Цех #2 Astana'];
            break;
          case 'Shymkent':
            this.shopOptions = ['Цех #1 Shymkent', 'Цех #2 Shymkent'];
            break;
          default:
            this.shopOptions = [];
            break;
        }
        this.selectedShop = '';
        this.selectedEmployee = '';
      }, 0);
    },
    updateEmployeeSelectOptions() {
      setTimeout(() => {
        switch (this.selectedShop) {
          case 'Цех #1 Almaty':
            this.employeeOptions = ["Marat", "Kanat", "Bauirjan"];
            break;
          case 'Цех #2 Almaty':
            this.employeeOptions = ["Kaisar", "Bekzat"];
            break;
          case 'Цех #1 Astana':
            this.employeeOptions = ["Aibek", "Zhandos", "Sauran"];
            break;
          case 'Цех #2 Astana':
            this.employeeOptions = ["Kirill", "Shinar"];
            break;
          case 'Цех #1 Shymkent':
            this.employeeOptions = ["Lyazzat", "Ilias", "Erbol"];
            break;
          case 'Цех #2 Shymkent':
            this.employeeOptions = ["Askar", "Serik"];
            break;
          default:
            this.employeeOptions = [];
            break;
        }
        this.selectedEmployee = '';
      }, 0);
    },
    saveCookie(name, obj, days) {
      let jsonData = JSON.stringify(obj);
      const expireDate = new Date();
      expireDate.setTime(expireDate.getTime() + days * 24 * 60 * 60 * 1000);
      const expires = "expires=" + expireDate.toUTCString();
      document.cookie = name + "=" + encodeURIComponent(jsonData) + ";" + expires + ";path=/";
      console.log(document.cookie);
    }
  },
};
</script>

<style>
label{
  margin: 0 5px 0 20px
}

select {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.btn {
  margin: 10px 30px; 
  padding: 5px;
}
</style>
