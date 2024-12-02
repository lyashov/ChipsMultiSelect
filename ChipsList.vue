<script setup>
import { ref } from 'vue'
import SelectedItem from '@/ui-library-b2b/search/ChipsItem.vue'

const props = defineProps({
  bindName: {
    type: String,
    default: 'name',
  },
  inn: {
    type: Boolean,
    default: false,
  },
})
const emit = defineEmits(['on-keyup', 'blur'])
const chips = defineModel()
const multiselectRef = ref(null)

function deleteItem(item) {
  chips.value = chips.value.filter((el) => el !== item)
}

function onKeyUp(e) {
  emit('on-keyup', multiselectRef.value.textContent)
  if (e.key === 'Enter') {
    multiselectRef.value.textContent = ''
  }
}

function onBlur() {
  emit('blur', multiselectRef.value.textContent)
  multiselectRef.value.textContent = ''
}

function handleInput() {
  const maxLength = 12

  if (props.inn) {
    if (multiselectRef.value.textContent.length > maxLength) {
      multiselectRef.value.textContent = multiselectRef.value.textContent.slice(0, maxLength)
    }
    multiselectRef.value.textContent = multiselectRef.value.textContent.replace(/\D/g, '')
  }
}
</script>

<template>
  <div class="chips">
    <div v-for="(item, index) in chips" :key="index">
      <SelectedItem :item="item" :bind-name @delete="deleteItem" />
    </div>
    <div
      ref="multiselectRef"
      contenteditable="true"
      spellcheck="false"
      class="custom-div"
      @keydown.enter.prevent=""
      @keyup="onKeyUp"
      @blur="onBlur"
      @input="handleInput"
    />
  </div>
</template>

<style lang='scss' scoped>
.chips {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 3px;
  margin-top: 4px;
  width: 100%;
}

.custom-div {
  flex-grow: 1;
  white-space: nowrap;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.custom-div:focus {
  outline: none;
}
</style>
