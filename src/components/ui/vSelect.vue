<template >
  <div class="sorting-container">
    <p class="caption dark__middle--text flex gap-15">
      Сортировать по:
      <span class="sorting" :class="{'sorting__active' : priceSorted}" @click="sortPrice(!sortByPrice.desc)">
        Цене
        <i v-show="priceSorted">
          <VIconDown v-if="!sortByPrice.desc" />
          <VIconUp v-if="sortByPrice.desc" />
        </i>
      </span>
      <span class="sorting" :class="{'sorting__active' : titleSorted}" @click="sortTitle(!sortByTitle.desc)">
        Алфавиту
        <i v-show="titleSorted">
          <VIconDown v-if="!sortByTitle.desc" />
          <VIconUp v-if="sortByTitle.desc" />
        </i>
      </span>
    </p>
  </div>
</template>
<script>
import VIconDown from './vIconDown.vue';
import VIconUp from './vIconUp.vue';

export default {
  name: "vSelect",
  components: { VIconDown, VIconUp },
  props: ['sortByPrice', 'sortByTitle', 'priceSorted', 'titleSorted'],
  methods: {
    sortPrice(desc) {
      this.$emit('sortPrice', desc);
      this.$emit('priceSorted', true)
    },
    sortTitle(desc) {
      this.$emit('sortTitle', desc);
      this.$emit('titleSorted', true)
    },
  }
}
</script>