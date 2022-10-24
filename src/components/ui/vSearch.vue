<template >
    <label for="search">
      <span>Поиск</span>
      <input 
        :value="value" 
        type="text" 
        placeholder="Поиск по каталогу" 
        @input="$emit('input', $event.target.value)"
      />
    </label>
</template>
<script>
export default {
  name: 'vSearch',
  props: ['value']
}
</script>
