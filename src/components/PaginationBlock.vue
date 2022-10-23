<template>
  <div class="flex gap-10 jcc" v-if="items > limit">
    <VButtonPrevious 
      v-show="this.limit > 3"
      @click.native="pageClick(currentPage - 1)" 
      :disabled="this.currentPage == 1" 
    />
    <button 
      v-for="page in pages" 
      :key="page" 
      :class="{'active' : page === currentPage}" 
      @click="pageClick(page)">
      {{ page }}
    </button>
    <VButtonNext 
      v-show="this.limit > 3" 
      @click.native="pageClick(currentPage + 1)" 
      :disabled="this.currentPage == this.maxPages" 
    />
  </div>
</template>
<script>
import VButtonPrevious from '@/components/ui/vButtonPrevious.vue';
import VButtonNext from '../components/ui/vButtonNext.vue';

export default {
  components: {
    VButtonPrevious,
    VButtonNext
  },
  props: ['items', 'limit', 'currentPage'],
  data() {
    return {
      maxPages: Number,
    }
  },
  methods: {
    pageClick(page) {
      this.$emit('pageClick', page);
    }
  },
  computed: {
    pages() {
      return this.maxPages = Math.ceil(this.items / this.limit);
    }
  }
}
</script>