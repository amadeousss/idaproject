<template>
  <div class="flex">
    <h1>Добавление товара</h1>
    <dropdown-menu />
  </div>
</template>

<style lang="scss" scoped>
  .flex{
    display: flex;
    align-items: center;
    justify-content: space-between;
    @media (max-width: 430px){
      flex-direction: column;
      row-gap: 1rem;
    }
    h1{
      color: rgb(63, 63, 63);
      font-size: 1.75rem;
      @media (max-width: 650px){
        font-size: 1.25rem;
      }
    }
  }
</style>
