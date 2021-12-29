<template>
  <button @click="processSendForm" class="btn">Зарегистрироваться</button>
</template>

<script>
  export default {
    /*data() {
      /*return {
        isFormSent: false,
      };
    },*/
    methods: {
      processSendForm() {
        this.$emit("handleForm", true);
      },
    },
  };
</script>

<style lang="scss">
  .btn {
    background-color: rgb(19, 95, 210);
    font-size: 1rem;
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 0.9em 2.1875em;
    cursor: pointer;
    &:hover {
      background-color: #176ef3;
    }
  }
</style>
