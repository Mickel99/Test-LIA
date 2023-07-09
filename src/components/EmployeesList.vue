<template>
    <div class="employee-list">
      <ul class="employee-list__wrapper">
        <li v-for="employee in employees" :key="employee.id" class="employee-list__item">
          <div class="employee-list__avatar">
            <img :src="employee.avatar" alt="Profile picture" />
          </div>
          <div class="employee-list__info">
            <span class="employee-list__name">{{ employee.first_name }} {{ employee.last_name }}</span>
            <div class="employee-list__contact">
              <a :href="'mailto:' + employee.email">Contact</a>
            </div>
          </div>
        </li>
      </ul>
      <div class="pagination">
        <button class="pagination__button" v-for="pageNumber in totalPages" :key="pageNumber" @click="fetchEmployees(pageNumber)">
          {{ pageNumber }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        employees: [],
        totalPages: 0,
      };
    },
    mounted() {
      this.fetchEmployees(1);
    },
    methods: {
      fetchEmployees(page) {
        axios.get(`https://reqres.in/api/users?page=${page}`)
          .then(response => {
            this.employees = response.data.data;
            this.totalPages = response.data.total_pages;
          })
          .catch(error => {
            console.error(error);
          });
      },
    },
  };
  </script>
  
  <style src="./employee-list.css" scoped></style>
  