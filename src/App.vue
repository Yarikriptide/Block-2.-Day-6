<template>
  <div>
    <!-- Таблиця зі списком студентів -->
    <table class="student-table">
      <thead>
        <tr>
          <th class="table-header">ПІБ</th>
          <th class="table-header">Група</th>
          <th class="table-header">Оцінка</th>
          <th class="table-header">Практика</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="student in students" :key="student._id">
          <td class="table-cell">
            <router-link :to="'/student-info/' + student._id">{{ student.name }}</router-link>
          </td>
          <td class="table-cell">
            {{ student.group }}
          </td>
          <td class="table-cell">
            {{ student.mark }}
          </td>
          <td class="table-cell">
            {{ student.isDonePr ? 'Завершена' : 'Не завершена' }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.student-table {
  width: 100%;
  border-collapse: collapse;
  font-family: Arial, sans-serif;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Тінь */
}

.table-header {
  background: linear-gradient(to bottom, #800080, #4b0082); /* Пурпурний градієнт */
  color: #fff; /* Колір тексту */
  padding: 12px;
  text-align: center;
  border: 1px solid #e1e1e1;
  font-weight: bold;
}

.table-cell {
  padding: 12px;
  text-align: center;
  border: 1px solid #e1e1e1;
  background: linear-gradient(to bottom, #ffffff, #f9f9f9); /* Градієнт для ячейок */
  color: #000; /* Колір тексту */
}

.student-table tbody tr:nth-child(odd) {
  background-color: #f9f9f9;
}

.student-table tbody tr:nth-child(even) {
  background-color: #ffffff;
}

.student-table tbody tr:hover {
  background-color: #d4e9f9;
  transition: background-color 0.3s;
}
</style>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      apiBaseUrl: 'http://34.82.81.113:3000',
      students: [],
    };
  },
  created() {
    this.fetchStudents();
  },
  methods: {
    async fetchStudents() {
      try {
        const response = await axios.get(`${this.apiBaseUrl}/students`);
        this.students = response.data;
      } catch (error) {
        console.error('Помилка при завантаженні студентів:', error);
      }
    },
  },
}
</script>
