<template>
  <custom-input v-model="filter"
                :label="props.label || t('defaults.filter.label')"
                :title="columns"
                dense outlined name="filter"
                @keydown.esc="filter = ''">
    <template #append>
      <q-icon name="search" />
    </template>
  </custom-input>
</template>

<script setup lang="ts">
  import { ref, watch } from 'vue'
  import { useTranslation } from '../../composables/i18n'
  import CustomInput from './CustomInput.vue'

  const t = useTranslation()

  const props = defineProps<{ modelValue: string, label?: string, columns?: string[] }>()

  const emit = defineEmits(['update:modelValue'])
  const filter = ref(props.modelValue)
  watch(filter, newValue => (emit('update:modelValue', newValue)))
  watch(() => props.modelValue, newValue => (filter.value = newValue))
</script>
