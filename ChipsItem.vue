<script setup>
import Icon from '@/ui-library-b2b/icons/B2BBaseIcon.vue'

const props = defineProps({
  item: {
    type: Object,
  },
  bindName: {
    type: String,
    default: 'name',
  },
})

const emit = defineEmits(['delete'])

function deleteItem() {
  emit('delete', props.item)
}
</script>

<template>
  <div class="selected-item">
    {{ item[bindName] }}
    <div class="selected-item__close" @click.stop="deleteItem()">
      <Icon icon="Close" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.selected-item {
  display: flex;
  gap: 4px;
  align-items: center;
  color: var(--text-colors);
  font-weight: 300;
  font-style: normal;
  line-height: 20px;
  white-space: nowrap;
  font-size: 14px;
  letter-spacing: 0.005em;
  text-align: left;
  flex-direction: row;
  padding: 4px 6px 4px 8px;
  background: rgba(16, 24, 40, 0.1);
  border-radius: 2px;

  &__close {
    color: black;
    cursor: pointer;
  }
}
</style>
