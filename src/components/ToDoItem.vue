<template>
  <div>
    <input type="checkbox" name="checkbox" :id="id" :checked="isDone" />
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script>
export default {
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
      isDone: this.done,
    };
  },
  mounted() {
    console.log(this.label, this.required);
  },
  // setup() {},
};
</script>
