<template>
  <div class="sidebar">
    <Card class="sidebar-card">
      <template #title>Navigation</template>
      <template #content>
        <ul class="menu">
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/about">About</router-link></li>
          <li><router-link to="/contact">Contact</router-link></li>
        </ul>
      </template>
    </Card>
  </div>
</template>

<style scoped>
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 250px;
  height: 100vh;
  background-color: #f8f9fa;
  padding: 1rem;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.sidebar-card {
  width: 100%;
}

.menu {
  list-style: none;
  padding: 0;
}

.menu li {
  margin-bottom: 10px;
}

.menu a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
  transition: 0.3s;
}

.menu a:hover {
  color: #007bff;
}
</style>
