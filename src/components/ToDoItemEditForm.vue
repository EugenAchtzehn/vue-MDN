<template>
  <form class="stack-small" @submit.prevent="onSubmit">
    <div>
      <label class="edit-label">編輯： "{{ label }}" 任務</label>
      <input :id="id" type="text" autocomplete="off" v-model.lazy.trim="newLabel" />
    </div>
    <div class="btn-group">
      <button type="button" class="btn" @click="onCancel">
        取消
        <span class="visually-hidden">editing {{ label }}</span>
      </button>
      <!-- submit 事件觸發元素 -->
      <button type="submit" class="btn btn__primary">
        儲存
        <span class="visually-hidden">edit for {{ label }}</span>
      </button>
    </div>
  </form>
</template>
<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      newLabel: this.label,
    };
  },
  methods: {
    onSubmit() {
      // 當 newLabel (input 輸入) 有值，且有被更動 (不等同於傳入值) 時
      // 將 newLabel 數值往上層丟
      if (this.newLabel && this.newLabel !== this.label) {
        this.$emit('item-edited', this.newLabel);
      }
    },
    onCancel() {
      this.$emit('edit-cancelled');
    },
  },
};
</script>
<style scoped>
.edit-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}
input {
  display: inline-block;
  margin-top: 0.4rem;
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}
form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
form > * {
  flex: 0 0 100%;
}
</style>
