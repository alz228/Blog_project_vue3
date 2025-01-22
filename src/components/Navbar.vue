<template>
  <div class="navbar">
    <div class="main-page--textbox" @click="$router.push('/')">Main page</div>
    <div class="navbar__btns">
      <!-- <my-button @click="$router.push('./posts')">blog</my-button> -->
      <my-button @click="$router.push('/blog')" style="margin-left: 15px"
        >Blog</my-button
      >
      <my-button @click="$router.push('/about')" style="margin-left: 15px"
        >about</my-button
      >
      
    </div>
  </div>
</template>

<script></script>

<style scoped>
.navbar {
  height: 60px;
  background-color: #1a1a1a;
  box-shadow: 2px 2px 4px gray;
  display: flex;
  align-items: center;
  padding: 0 15px;
  border-bottom: 1px solid #f0f0f0;
  color: #e3e3e3;
  font-family: 'Roboto', sans-serif;
}

.navbar__btns {
  margin-left: auto;
}

.main-page--textbox{
  cursor: pointer;
  font-size: 20px;
  font-weight: bold;
  color: teal;

}
</style>
