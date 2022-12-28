<template>
  <p>导航栏</p>
  <router-link to='/'>Frank</router-link> &nbsp;
  <router-link to='/xxx'>Frank2</router-link>
  <hr />
  <router-view />
</template>

<script>

export default {
  name: 'App',
}
</script>
