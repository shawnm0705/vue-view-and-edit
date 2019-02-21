<template>
  <a v-if="!isEditing" href="javascript:void(0)" @click="edit">{{ (value) ? value : defaultValue }}</a>
  <div v-else>
    <select v-if="type == 'select'" v-model="innerValue" @blur="save">
      <option v-for="option in options" v-bind:key="option.value" :value="option.value">{{ option.text }}</option>
    </select>
    <textarea v-else-if="type == 'textarea'"
      v-model="innerValue"
      :style="{'min-width': minWidth, 'min-height': minHeight}"
      @blur="save" />
    <input v-else
      type="text"
      v-model="innerValue"
      :style="{width: width}"
      @keyup.enter="save"
      @blur="save"
      >
    <button @click="save"><font-awesome-icon icon="check-circle" class="green"/></button>
    <button @click="cancel"><font-awesome-icon icon="times-circle" class="red"/></button>
  </div>
</template>

<script>
export default {
  name: 'view-and-edit',
  props: {
    type: {
      type: String,
      default: 'text-field'
    },
    value: {
      type: String,
      default: ''
    },
    defaultValue: {
      type: String,
      default: 'no value'
    },
    options: {
      type: Array,
      default: () => {
        return [];
      }
    },
    width: {
      type: String,
      default: "150px"
    },
    minWidth: {
      type: String,
      default: "500px"
    },
    minHeight: {
      type: String,
      default: "200px"
    }
  },
  data() {
    return {
      isEditing: false,
      innerValue: ''
    };
  },
  methods: {
    // when user click the link to edit
    edit() {
      this.innerValue = this.value;
      if (this.value === this.defaultValue) {
        this.innerValue = '';
      }
      this.isEditing = true;
    },
    // when user click "times" to cancel the edition
    cancel() {
      this.isEditing = false;
    },
    // when user click "check" to save the edition
    save() {
      // send "save" event back to parent component with the edited value
      this.$emit('save', this.innerValue);
      this.isEditing = false;
    }
  }
}
</script>

<style scoped>
a {
  border-bottom: 1px dashed;
  text-decoration: none;
  white-space: pre;
}
button {
  border: none;
  padding: 0 3px;
}
button:hover {
  transform: scale(1.2);
}
.green {
  color: green;
}
.red {
  color: red;
}
</style>
