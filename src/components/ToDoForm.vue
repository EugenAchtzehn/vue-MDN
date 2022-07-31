<template>
  <form @submit.prevent="OnSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo" class="label__lg">What needs to be done?</label>
    </h2>
    <input
      type="text"
      id="new-todo"
      name="new-todo"
      v-model.lazy.trim="inputVal"
      autocomplete="off"
      class="input__lg"
    />
    <button type="sumbit" class="btn btn__primary btn__lg">Add</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      inputVal: '',
    };
  },
  methods: {
    OnSubmit() {
      // Cannot use capital case as event name.
      // Ensure no empty value will be passed.
      if (this.inputVal === '') {
        return;
      }

      // this.$emit('event-name');
      this.$emit('todo-added', this.inputVal);

      // Clean the input section.
      this.inputVal = '';
    },
  },
};
</script>
