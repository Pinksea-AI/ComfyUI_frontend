<template>
  <Button
    v-show="isSingleImageNode"
    v-tooltip.top="{
      value: t('commands.Comfy_MaskEditor_OpenMaskEditor.label'),
      showDelay: 1000
    }"
    severity="secondary"
    text
    icon="pi pi-pencil"
    @click="openMaskEditor"
  />
</template>

<script setup lang="ts">
import Button from 'primevue/button'
import { computed } from 'vue'

import { t } from '@/i18n'
import { useCommandStore } from '@/stores/commandStore'
import { useCanvasStore } from '@/stores/graphStore'
import { isImageNode, isLGraphNode } from '@/utils/litegraphUtil'

const commandStore = useCommandStore()
const canvasStore = useCanvasStore()

const isSingleImageNode = computed(() => {
  const { selectedItems } = canvasStore
  const item = selectedItems[0]
  return selectedItems.length === 1 && isLGraphNode(item) && isImageNode(item)
})

const openMaskEditor = () => {
  void commandStore.execute('Comfy.MaskEditor.OpenMaskEditor')
}
</script>
