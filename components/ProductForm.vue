<template>
  <div id="root">
    <form @submit.prevent="submitForm()">
      <div class="form-group">
        <label class="productName">Наименование товара<div class="required-dot"></div></label>
        <input type="text" :class="{ 'invalid-field': $v.name.$invalid && $v.name.$dirty }" v-model.trim="$v.name.$model" placeholder="Введите наименование товара">
        <div class="error name-error" v-if="!$v.name.required && $v.name.$dirty">Поле является обязательным</div>
      </div>
      <div class="form-group">
        <label>Описание товара</label>
        <textarea style="resize: none;" v-model.trim="description" class="form__input description" placeholder="Введите описание товара"></textarea>
      </div>
      <div class="form-group">
        <label>Ссылка на изображение товара<div class="required-dot"></div></label>
        <input type="text" :class="{ 'invalid-field': $v.link.$invalid && $v.link.$dirty }" v-model.trim="$v.link.$model" placeholder="Введите ссылку">
        <div class="error link-error" v-if="!$v.link.required && $v.link.$dirty">Поле является обязательным</div>
        <div class="error link-error" v-if="$v.link.required && !$v.link.url && $v.link.$dirty ">Введена некорректная ссылка</div>
      </div>
      <div class="form-group">
        <label>Цена товара<div class="required-dot"></div></label>
        <input type="text" :class="{ 'invalid-field': $v.price.$invalid && $v.price.$dirty }" v-model.trim="$v.price.$model" placeholder="Введите цену">
        <div class="error price-error" v-if="!$v.price.required && $v.price.$dirty">Поле является обязательным</div>
        <div class="error price-error" v-if="!$v.price.decimal && $v.price.required && $v.price.$dirty">Введите число</div>
      </div>
      <input type="submit" class="button" :class="{ 'button-valid': !$v.$invalid }" value="Добавить товар">
    </form>
  </div>
</template>

<script>
import { required, url, decimal } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      name: '',
      description: '',
      link: '',
      price: ''
    }
  },
  validations: {
    name: { required },
    link: { required, url },
    price: { required, decimal }
  },
  methods: {
    submitForm () {
      this.$v.$touch()
      if (!this.$v.$invalid) {
        this.$parent.addProduct(this.name, this.description, this.link, this.price)
        this.name = ''
        this.description = ''
        this.link = ''
        this.price = ''
        this.$v.$reset()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  #root{
    background-color: rgb(255, 254, 251);
    box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.02), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
    max-width: 332px;
    border-radius: 0.25rem;
    padding: 1.5rem;
    height: 440px;
    @media (max-width: 743px){
      max-width: 100%;
    }
    label{
      display: block;
      font-size: 0.625rem;
      margin-top: 1rem;
      margin-bottom: 0.25rem;
      &.productName{
        margin-top: 0;
      }
    }
    input[type=text], textarea{
      width: 100%;
      padding: 0.625rem 1rem;
      font-size: 0.75rem;
      border: none;
      box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.1);
      border-radius: 0.25rem;
      transition: 0.2s ease-in-out;
      &.description{
        height: 108px;
        font-family: inherit;
      }
      &:focus{
        outline: 1px solid gray;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 2px 10px;
      }
    }
    .button{
      width: 100%;
      text-align: center;
      border: none;
      border-radius: 0.625rem;
      background-color: rgb(238, 238, 238);
      font-size: 0.75rem;
      font-weight: 600;
      padding-block: 0.625rem;
      color: rgb(180, 180, 180);
      margin-top: 1.5rem;
      transition: 0.1s ease-in-out;
    }
    .error{
      color: rgb(255, 132, 132);
      font-size: 0.5rem;
      padding: 0;
      margin: 0;
    }
    .form-group{
      position: relative;
    }
    .error{
      position: absolute;
      bottom: -14px;
    }
    .required-dot{
      width: 4px;
      height: 4px;
      background-color: rgb(255, 132, 132);
      border-radius: 4px;
      display: inline-block;
      vertical-align: top;
    }
    .button-valid{
      background-color: rgb(123, 174, 115);
      color: white;
      cursor: pointer;
      &:hover{
        background-color: rgb(113, 160, 107);
      }
    }
    .invalid-field{
      outline: 1px solid #FF8484;
    }
  }
</style>
