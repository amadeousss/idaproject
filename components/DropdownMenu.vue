<template>
  <div>
    <select @change="$parent.$parent.sortProducts(selected)" v-model="selected">
      <option>По умолчанию</option>
      <option>По цене min</option>
      <option>По цене max</option>
      <option>По наименованию</option>
    </select>
  </div>
</template>

<script>
export default {
  data () {
    return {
      selected: 'По умолчанию'
    }
  }
}
</script>

<style lang="scss" scoped>
  select{
    padding: 0.625rem 1rem;
    font-family: 'Source Sans Pro';
    font-size: 0.75rem;
    border: none;
    outline: none;
    background-color: rgb(255, 254, 251);
    box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    color: rgb(180, 180, 180);
    max-width: 155px;
    option{
      color: black;
    }
  }
</style>
