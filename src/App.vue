<template>
  <section class="selected-box">
    <div class="select-item">
      <span>Select One</span>
    </div>
    <div class="dropdown">
      <input v-model="searchQuery" type="text" placeholder="Search">
      <div class="options">
        <ul>
          <li>İstanbul</li>
          <li>Ankara</li>
          <li>İzmir</li>
          <li>Bursa</li>
          <li>Diyarbakır</li>
        </ul>
      </div>
    </div>

  </section>
</template>

<script>
export default {};
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
  }
</style>
