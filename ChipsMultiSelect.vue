<script setup lang="ts">
// import
import { ref } from 'vue'
import Chips from '@/ui-library-b2b/search/ChipsList.vue'
import Icon from '@/ui-library-b2b/icons/B2BBaseIcon.vue'

// props
const props = defineProps({
  caption: {
    type: String,
    default: 'Список холдингов',
  },
  placeholder: {
    type: String,
    default: '',
  },
})

// const
const searchText = defineModel()
const chips = ref([])
const title = ref('My title')
const titleElement = ref(null)

// methods
function validate(event: Event) {
  event.preventDefault()
  // (event.target as HTMLInputElement).blur()
  chips.value.push(titleElement.value.innerText.trim())
  titleElement.value.innerText = ''
}

function keyUp() {
  searchText.value = titleElement.value.innerText
  console.log(titleElement.value.innerText)
}

defineExpose({ titleElement })
</script>

<template>
  <div class="multi-search">
    <div class="multi-search__input">
      <Icon class="multi-search__icon-search" icon="Search" />
      <Chips v-model="chips" style="padding-left: 40px;" />
      <div
        ref="titleElement" contenteditable="true" spellcheck="false" :placeholder="chips.length > 0 ? '' : placeholder" @keyup="keyUp"
        @keydown.enter="validate"
      />
    </div>
  </div>
</template>

<style scoped lang="scss">
.multi-search{
  [contenteditable=true]:empty:before{
    content: attr(placeholder);
    padding-top: 3px;
    pointer-events: none;
    display: block;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.005em;
    color: rgba(16, 24, 40, 0.5);
  }

  div[contenteditable=true] {
    padding: 5px;
    width: 100%;
    outline:none;
  }

  position: relative;

  &__icon-search{
    position: fixed;
    margin: 5px 10px;
    width: 24px;
    height: 24px;
  }

  &__input{
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    width: 800px;
    height: 36px;
    box-sizing: border-box;
    border: 1px solid rgba(16, 24, 40, 0.1);
    box-shadow: inset 0px 1px 0px rgba(16, 24, 40, 0.05), inset 0px 2px 0px rgba(16, 24, 40, 0.05);
    border-radius: 4px;

  }

  .btn {
    width: 16px;
    height: 16px;

    position: absolute;
    top: 8px;
    bottom: 10px;
    right: 10px;
    display: none;
    border: 0;
    padding-top: 0 -5px;
    border-radius: 50%;
    background-color: #fff;
    transition: background 200ms;
    outline: none;

    &:hover {
      width: 16px;
      height: 16px;
      display: block;
      background: url("../../assets/img/navigation/close.svg") no-repeat;
    }

  }

  input:valid ~ div {
    display: block;
  }

  .ok {
    background: url("../../assets/img/navigation/ok.svg") no-repeat;
  }

  .err {
    background: url("../../assets/img/navigation/close_gray.svg") no-repeat;
  }
}
</style>
