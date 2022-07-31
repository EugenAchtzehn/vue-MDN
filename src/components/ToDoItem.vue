<template>
  <!-- 非編輯狀態時才會顯示 -->
  <div class="stack-small" v-if="!isEditing">
    <div class="custom-checkbox">
      <input
        type="checkbox"
        :id="id"
        :checked="isDone"
        class="checkbox"
        @change="$emit('checkbox-changed')"
      />
      <label :for="id" class="checkbox-label">{{ label }}</label>
    </div>

    <div class="btn-group">
      <button type="button" class="btn" @click="toggleToItemEditForm">
        編輯 <span class="visually-hidden">{{ label }}</span>
      </button>
      <button type="button" class="btn btn__danger" @click="deleteTodo">
        刪除 <span class="visually-hidden">{{ label }}</span>
      </button>
    </div>
  </div>
  <to-do-item-edit-form
    v-else
    :id="id"
    :label="label"
    @item-edited="itemEdited"
    @edit-cancelled="editCancelled"
  ></to-do-item-edit-form>
</template>

<script>
import ToDoItemEditForm from '@/components/ToDoItemEditForm';
export default {
  components: {
    ToDoItemEditForm,
  },
  // 子元件接收傳入：陣列方式
  // props: ['title', 'img']

  // 子元件接收傳入：物件方式
  // 可自訂預設值，外層如果沒傳入，會帶入預設值
  // 另外可加入驗證，判斷外層傳入是否符合規則
  props: {
    label: {
      // 指定為必要屬性，型別為字串
      required: true,
      type: String,
      // [String, Number] => 允許多種型別
    },
    done: {
      // 預設為false，輸入為布林值
      default: false,
      type: Boolean,
    },
    id: {
      required: true,
      type: String,
    },
  },
  data() {
    return {
      // 取出 props 的 done 內容，改由 isDone 進行操作
      // isDone: this.done,

      // 記錄是否編輯的狀態
      isEditing: false,
    };
  },
  methods: {
    toggleToItemEditForm() {
      this.isEditing = true;
    },
    deleteTodo() {
      this.$emit('item-deleted');
    },
    // Pass the edited result to parent
    itemEdited(newLabel) {
      this.$emit('item-edited', newLabel);
      // 結束編輯狀態，返回一般待辦
      this.isEditing = false;
    },
    // 終結編輯程序
    editCancelled() {
      this.isEditing = false;
    },
  },
  computed: {
    isDone() {
      return this.done;
    },
  },
  mounted() {
    // console.log(this.label, this.required);
  },
  // setup() {},
};
</script>

<style scoped>
.custom-checkbox > .checkbox-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 400;
  font-size: 16px;
  font-size: 1rem;
  line-height: 1.25;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}
.custom-checkbox > .checkbox {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 400;
  font-size: 16px;
  font-size: 1rem;
  line-height: 1.25;
  box-sizing: border-box;
  width: 100%;
  height: 40px;
  height: 2.5rem;
  margin-top: 0;
  padding: 5px;
  border: 2px solid #0b0c0c;
  border-radius: 0;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}
.custom-checkbox > input:focus {
  outline: 3px dashed #fd0;
  outline-offset: 0;
  box-shadow: inset 0 0 0 2px;
}
.custom-checkbox {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  font-weight: 400;
  font-size: 1.6rem;
  line-height: 1.25;
  display: block;
  position: relative;
  min-height: 40px;
  margin-bottom: 10px;
  padding-left: 40px;
  clear: left;
}
.custom-checkbox > input[type='checkbox'] {
  -webkit-font-smoothing: antialiased;
  cursor: pointer;
  position: absolute;
  z-index: 1;
  top: -2px;
  left: -2px;
  width: 44px;
  height: 44px;
  margin: 0;
  opacity: 0;
}
.custom-checkbox > .checkbox-label {
  font-size: inherit;
  font-family: inherit;
  line-height: inherit;
  display: inline-block;
  margin-bottom: 0;
  padding: 8px 15px 5px;
  cursor: pointer;
  touch-action: manipulation;
}
.custom-checkbox > label::before {
  content: '';
  box-sizing: border-box;
  position: absolute;
  top: 0;
  left: 0;
  width: 40px;
  height: 40px;
  border: 2px solid currentColor;
  background: transparent;
}
.custom-checkbox > input[type='checkbox']:focus + label::before {
  border-width: 4px;
  outline: 3px dashed #228bec;
}
.custom-checkbox > label::after {
  box-sizing: content-box;
  content: '';
  position: absolute;
  top: 11px;
  left: 9px;
  width: 18px;
  height: 7px;
  transform: rotate(-45deg);
  border: solid;
  border-width: 0 0 5px 5px;
  border-top-color: transparent;
  opacity: 0;
  background: transparent;
}
.custom-checkbox > input[type='checkbox']:checked + label::after {
  opacity: 1;
}
@media only screen and (min-width: 40rem) {
  label,
  input,
  .custom-checkbox {
    font-size: 19px;
    font-size: 1.9rem;
    line-height: 1.31579;
  }
}
</style>
