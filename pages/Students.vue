<template>
  <div>
    <h1>Список студентів</h1>

    <div>
      <!-- Пошук -->
      <input type="text" v-model="searchQuery" @input="search" placeholder="Пошук студента" style="margin-bottom: 10px; color:lightskyblue;">

      <!-- Таблиця зі списком студентів -->
      <table>
        <thead>
        <tr>
          <th>Ім'я</th>
          <th>Прізвище</th>
          <th>Група</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="student in paginatedStudents" :key="student.id">
          <td>{{ student.firstName }}</td>
          <td>{{ student.lastName }}</td>
          <td>{{ student.group }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <!-- Пагінація -->
    <button @click="previousPage" :disabled="currentPage === 1"><</button>
    <span> {{ currentPage }} з {{ totalPages }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPages">></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [], // Список студентів
      searchQuery: '', // Пошуковий запит
      currentPage: 1, // Поточна сторінка
      itemsPerPage: 10, // Кількість елементів на сторінці
      filteredStudents: [] // Відфільтровані студенти
    };
  },
  computed: {
    // Обчислення загальної кількості сторінок
    totalPages() {
      return Math.ceil(this.filteredStudents.length / this.itemsPerPage);
    },
    // Відфільтрований список студентів для поточної сторінки
    paginatedStudents() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.filteredStudents.slice(startIndex, endIndex);
    }
  },
  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    // Фільтрація студентів за пошуковим запитом
    search() {
      this.filteredStudents = this.students.filter(student =>
        student.firstName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.lastName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.group.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      this.currentPage = 1; // При кожному пошуку переходимо на першу сторінку
    }
  },
  mounted() {
    this.students = [
      { id: 1, firstName: 'Василь', lastName: 'Іванов', group: 'Група 3' },
      { id: 2, firstName: 'Наталія', lastName: 'Петрів', group: 'Група 4' },
      { id: 3, firstName: 'Ірина', lastName: 'Павлівна', group: 'Група 3' },
      { id: 4, firstName: 'Юрій', lastName: 'Олександрович', group: 'Група 4' },
      { id: 5, firstName: 'Олексій', lastName: 'Володимирович', group: 'Група 4' },
      { id: 6, firstName: 'Надія', lastName: 'Петрівна', group: 'Група 4' },
      { id: 7, firstName: 'Вікторія', lastName: 'Ігорівна', group: 'Група 3' },
      { id: 8, firstName: 'Олег', lastName: 'Васильович', group: 'Група 4' },
      { id: 9, firstName: 'Микола', lastName: 'Олександрович', group: 'Група 3' },
      { id: 10, firstName: 'Ігор', lastName: 'Ярославович', group: 'Група 4' },
      { id: 11, firstName: 'Марина', lastName: 'Миколаївна', group: 'Група 4' },
      { id: 12, firstName: 'Олена', lastName: 'Михайлівна', group: 'Група 4' },
      { id: 13, firstName: 'Ірина', lastName: 'Михайлівна', group: 'Група 4' },
      { id: 14, firstName: 'Юлія', lastName: 'Михайлівна', group: 'Група 4' },
      { id: 15, firstName: 'Андрій', lastName: 'Володимирович', group: 'Група 4' },
      { id: 16, firstName: 'Тарас', lastName: 'Вікторович', group: 'Група 4' },
      { id: 17, firstName: 'Владислав', lastName: 'Миколаївич', group: 'Група 4' },
      { id: 18, firstName: 'Ігор', lastName: 'Петрович', group: 'Група 4' },
      { id: 19, firstName: 'Марина', lastName: 'Сергіївна', group: 'Група 4' },
      { id: 20, firstName: 'Олександр', lastName: 'Ігорович', group: 'Група 4' },
      { id: 21, firstName: 'Олена', lastName: 'Іванівна', group: 'Група 4' }
    ];
    this.filteredStudents = this.students; // Початково відображаємо всіх студентів
  }
};
</script>

<style>
/* Стилі для таблиці */
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  color: darkblue;
  background-color: #f2f2f2;
}

/* Зміна кольору рядків при наведенні миші */
tr:hover {
  color: olive;
  background-color: #f5f5f5;
}
</style>
