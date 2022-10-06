<template>
  <section class="selected-box">
    <div @click="isVisible= !isVisible" class="select-item" >
      <span v-if="selectedItem">{{ selectedItem.name }}</span>
      <input class="search" v-model="search" placeholder="Select One">
      <svg
        :class="isVisible ? 'dropdown-icon-2' : ''"
        class="dropdown-icon"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="17"
      >
        <path fill="none" d="M0 0h24v24H0z"/>
        <path d="M12 10.828l-4.95 4.95-1.414-1.414L12 8l6.364 6.364-1.414 1.414z"/>
      </svg>
      <span class="message" v-if="isVisible && filter.length === 0">No results found</span>
      <div v-if="isVisible">
        <div class="options">
          <ul>
            <li @click="selectItem(user)" v-for="(user, index) in filter" :key="`user-${index}`">{{ user.name }}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      selectedItem: null,
      isVisible: false,
      userArray: [],
    }
  },
  computed: {
    filter() {
      if (this.search === "") return this.userArray;
      return this.userArray.filter((user) =>
        Object.values(user).some((word) =>
          String(word).toLowerCase().includes(this.search.toLowerCase())
        )
      );
    },
  },
  created() {
    fetch("https://jsonplaceholder.typicode.com/users")
    .then((res) => res.json())
    .then((json) => {
      this.userArray = json;
    });
  },
  methods: {
    selectItem(user) {
      this.selectedItem = user;
      this.isVisible = false;
    }
  }
};
</script>

<style>
  .selected-box {
    max-width: 350px;
    margin: auto;
  }

  .select-item {
    border: 2px solid lightgray;
    border-radius: 5px;
  }

  .search {
    max-width: 250px;
    border: 10px solid transparent;
  }

  textarea:focus, input:focus{
    outline: none;
  }

  .dropdown-icon {
    transform: rotate(0deg);
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
    margin-top: 10px;
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

  li:hover {
    background: #a5a4a4;
    color: #fff;
    font-weight: bolder;
  }

  .message {
    margin-left: 35px;
  }
</style>
