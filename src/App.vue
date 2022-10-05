<template>
  <section class="selected-box">
    <div @click="isVisible= !isVisible" class="select-item">
      <span>Select One</span>
      <svg
        class="dropdown-icon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        width="24"
        height="24"
      >
        <path fill="none" d="M0 0h24v24H0z"/>
        <path d="M13 7.828V20h-2V7.828l-5.364 5.364-1.414-1.414L12 4l7.778 7.778-1.414 1.414L13 7.828z"/>
      </svg>
    </div>
    <div v-if="isVisible" class="dropdown">
      <input v-model="search" type="text" placeholder="Search">
      <div class="options">
        <ul>
          <li>İstanbul</li>
          <li>Ankara</li>
          <li>İzmir</li>
          <li>Bursa</li>
          <li>Diyarbakır</li>
          <li>Eskişehir</li>
        </ul>
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
    }
  },
};
</script>

<style>
  .selected-box {
    max-width: 300px;
    position: relative;
    margin: auto;
  }
  
  .select-item {
    height: 35px;
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
