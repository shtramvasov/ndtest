<template>
  <section class="courses-page app-wrapper flex cols gap-30">
    <img src="@/assets/img/logo.svg" alt="Новый Диск" height="36" width="98">
    <h1 class="mobile-size dark--text">Каталог курсов</h1>
    <vSearch v-model="searchQuery" />
    <div class="flex cols gap-15">
      <div class="flex jcsb">
        <p class="caption dark--text">{{ searchedItems.length }} результатов</p>
        <VSelect 
          :sortByPrice="this.sortByPrice"
          :sortByTitle="this.sortByTitle"
          :priceSorted="this.priceSorted"
          :titleSorted="this.titleSorted"
          :windowWidth="this.windowWidth"
          @sortPrice="(desc) => {this.sortByPrice.desc = desc; this.priceSorted = true}"
          @sortTitle="(desc) => {this.sortByTitle.desc = desc; this.titleSorted = true}"
        />
      </div>
      <div class="cards-container flex-wrap">
        <Card v-for="item in itemsPerPage" 
          :key=item.id 
          :title="item.title"
          :preview_img_path="item.preview_img_path"
          :cost="item.cost"
          :cost_currency="item.cost_currency"
          :series="item.series"
          :img="item.preview_img_path"
        />
      </div>
      <PaginationBlock 
        :items="searchedItems.length"
        :limit="this.limit"
        :currentPage="this.currentPage"
        @pageClick="(page) => this.currentPage = page"       
      />
    </div>
  </section>
</template>

<script>
import Card from '@/components/Card.vue';
import axios from 'axios';
import PaginationBlock from '@/components/PaginationBlock.vue';
import VSelect from '@/components/ui/vSelect.vue';
import VSearch from '@/components/ui/vSearch.vue';

export default {
  name: 'CoursesView',
  components: {
    Card,
    PaginationBlock,
    VSelect,
    VSearch
},
  mounted() {
    this.fetchData();
    window.addEventListener('resize', this.onResize);
    localStorage.searchQuery ? this.searchQuery = localStorage.searchQuery : '';
    localStorage.priceSorted ? this.priceSorted  = localStorage.priceSorted : false;
  },
  data() {
    return { 
      items: [],
      currentPage: 1,
      limit: Number | 9,
      windowWidth: window.innerWidth,
      priceSorted: localStorage.priceSorted,
      titleSorted: false,
      searchQuery: localStorage.searchQuery || '',
      sortByPrice: { desc: false },
      sortByTitle: { desc: false },
    }
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('/API.json');
        this.items = response.data;
      } catch (error) {
        console.error(error.message)
      }
    },
    onResize() {
      this.windowWidth = window.innerWidth;
      if (this.windowWidth <= 1366 && this.windowWidth > 768) 
        return this.limit = 9
      if (this.windowWidth <= 768 && this.windowWidth > 360) 
        return this.limit = 6
      if (this.windowWidth <= 360) 
        return this.limit = 3
    },
  },
  computed: {
    itemsHandler() {
      return [...this.items];
    },
    itemsPerPage() {
      let from = (this.currentPage - 1) * this.limit;
      let to = from + this.limit;
      return this.searchedItems.slice(from, to);
    },
    searchedItems() {
      localStorage.searchQuery = this.searchQuery;
      return this.itemsHandler.filter(item => item.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
    },
  },
  watch: {
    'sortByPrice.desc': function() { 
      if(this.sortByPrice.desc) {
        localStorage.priceSorted = true;
        this.items.sort((a, b) => a.cost > b.cost ? 1: -1);
      } else {
        this.items.sort((a, b) => a.cost > b.cost ? -1 : 1);
      }
    },
    'sortByTitle.desc': function() { 
      if(this.sortByTitle.desc) {
        this.items.sort((a, b) => a.title > b.title ? 1: -1);
      } else {
        this.items.sort((a, b) => a.title > b.title ? -1 : 1);
      }
    },
  }
}
</script>
<style lang="scss">
@import '../assets/styles/breakpoints';

.cards-container {
    display: grid;
    gap: 1.875rem;
    grid-template-columns: repeat(3, 1fr);
}

@media (max-width: $screen-medium) {
  .cards-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: $screen-small) {
  .cards-container {
    gap: 0.9375rem;
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>