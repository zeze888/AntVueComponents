<template>
  <div class="editable-cell">
    <div v-if="editable" class="editable-cell-input-wrapper">
      <a-input
        class="edit-input"
        :value="value"
        @change="handleChange"
        @pressEnter="check"
      />
      <span class="editable-cell-icon-check">
        <a-icon type="check" @click="check" />
      </span>
    </div>
    <div v-else class="editable-cell-text-wrapper">
      {{ value }}
      <span class="editable-cell-icon">
        <a-icon type="edit" @click="edit" />
      </span>
    </div>
  </div>
</template>
<script>
import { Icon, Input } from "ant-design-vue";

const components = {};
components[Icon.name] = Icon;
components[Input.name] = Input;
export default {
  name: "EditableCell",
  props: {
    text: Number
  },
  data() {
    return {
      editable: false,
      value: this.text
    };
  },
  components,
  watch: {
    text: function(n, o) {
      this.value = n;
    }
  },
  methods: {
    handleChange(e) {
      const value = e.target.value;
      this.value = value ? parseInt(value, 10) : 0;
    },
    check(e) {
      e.preventDefault();
      this.editable = false;
      this.$emit("change", this.value);
    },
    edit(e) {
      e.preventDefault();
      this.editable = true;
    }
  }
};
</script>
<style lang="less" scoped>
.editable-cell {
  position: relative;
}

.editable-cell-input-wrapper,
.editable-cell-text-wrapper {
  padding-right: 24px;
}

.editable-cell-text-wrapper {
  padding: 5px 24px 5px 5px;
}

.editable-cell-icon,
.editable-cell-icon-check {
  position: absolute;
  right: 0;
  width: 20px;
  cursor: pointer;
}

.editable-cell-icon {
  line-height: 18px;
  display: none;
}

.editable-cell-icon-check {
  line-height: 28px;
}

.editable-cell:hover .editable-cell-icon {
  display: inline-block;
}

.editable-cell-icon:hover,
.editable-cell-icon-check:hover {
  color: #108ee9;
}

.editable-add-btn {
  margin-bottom: 8px;
}

.edit-input {
  width: 100%;
  border: 0px;
  height: 30.8px;
  border-bottom: 1px dashed;
  box-sizing: border-box;
  background-color: #eeea;
}
</style>
