<template>
  <form>
    <label for="new-todo">What needs to be done?</label>
    <input
      type="text"
      name="new-todo"
      id="new-todo"
      v-model.lazy.trim="inputVal"
      autocomplete="off"
    />
    <button @click.prevent="OnSubmit">Add</button>
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
      // this.$emit('event-name');
      this.$emit('todo-added', this.inputVal);
    },
  },
};
</script>
