<template>
  <section class="dropdown-wrapper">
    <div class="selected-item">
      <span>Select One</span>
    </div>
    <div class="dropdown-popover">
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

</script>

<style>

</style>
