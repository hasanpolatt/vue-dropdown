<template>
  <section class="selected-box">
    <div @click="isVisible= !isVisible" class="select-item">
      <span v-if="selectedItem">{{ selectedItem.name }}</span>
      <span v-else>Select One</span>
      <svg
        :class="isVisible ? 'dropdown-icon-2' : ''"
        class="dropdown-icon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        width="24"
        height="24"
      >
        <path fill="none" d="M0 0h24v24H0z"/>
        <path d="M12 10.828l-4.95 4.95-1.414-1.414L12 8l6.364 6.364-1.414 1.414z"/></svg>
    </div>
    <div v-if="isVisible" class="dropdown">
      <input v-model="search" type="text" placeholder="Search">
      <span class="falan" v-if="filter.length === 0">No results found</span>
      <div class="options">
        <ul>
          <li v-for="(user, index) in filter" :key="index" @click="selectItem(user)">{{ user.name }}</li>  
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
import { computed, reactive } from '@vue/reactivity';
import { onMounted, ref } from 'vue';

export default {
  setup() {
    let search = ref(null);
    let userArray = reactive([]);
    const filter = computed(() => {
      if (search.value === "" || search.value === null) {
        return userArray;
      }
      return userArray.filter((user) => {
        return Object.values(user).some((word) => 
          String(word).toLowerCase().includes(search.value.toLowerCase()));
      })
    })

    onMounted(() => {
      fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((json) => {
        console.log(json);
        userArray = json;
      });
    })

    const selectedItem = ref(null);
    const isVisible = ref(false);
    function selectItem(user) {
      this.selectedItem = user;
      this.isVisible = false;
    }
    
    return {
      search,
      selectedItem,
      isVisible,
      userArray,
      selectItem,
      filter,
    };
  }
}
</script>

<style>
  .selected-box {
    max-width: 300px;
    position: relative;
    margin: auto;
  }

  .select-item {
    height: 40px;
    border: 2px solid lightgray;
    border-radius: 5px;
    padding: 5px 10px;
    display: flex;
    align-items: center;
    font-size: 20px;
    justify-content: space-between;
  }
  .dropdown {
    max-width: 300px;
    border: 2px solid lightgray;
    border-radius: 5px;
    position: absolute;
    left: 0;
    right: 0;
    padding: 10px;
  }
  .dropdown-icon {
    transform: rotate(deg);
    transition: all 0.3s;
  }
  .dropdown-icon-2 {
    transform: rotate(180deg);
    transition: all 0.3s;
  }
  input {
    width: 90%;
    border: 2px solid lightgray;
    border-radius: 5px;
    font-size: 16px;
    padding-left: 25px;
  }
  .options {
    width: 100%;
  }
  ul {
    list-style: none;
    text-align: left;
    padding-left: 8px;
    max-height: 180px;
    overflow-y: scroll;
    overflow-x: hidden;
  }
  li {
    width: 100%;
    border-bottom: 1px solid lightgrey;
    padding: 10px;
    background-color: #f3f3f3;
    cursor: pointer;
    font-size: 16px;
  }
</style>
