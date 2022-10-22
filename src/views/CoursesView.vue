<template>
  <section class="courses-page app-wrapper flex cols gap-30">
    <img src="@/assets/img/logo.svg" alt="Новый Диск" height="36" width="98">
    <h1 class="mobile-size dark--text">Каталог курсов</h1>
    <label for="search">
      <span>Поиск</span>
      <input 
        id="search" 
        type="text" 
        placeholder="Поиск по каталогу" 
      />
    </label>
    <div class="courses-content flex cols gap-15">
      <div class="flex jcsb">
        <p class="caption dark--text">458 результатов</p>
        <div class="courses-content__sorting">
          <p class="caption dark__middle--text">Сортировать по:</p>
        </div>
      </div>

      <div class="cards-container flex-wrap">
        <Card :img="'cover/pic1.jpg'"/>
        <Card :img="'cover/pic1.jpg'"/>
        <Card :img="'cover/pic1.jpg'"/>
        <Card :img="'cover/pic1.jpg'"/>
      </div>
    </div>
  </section>
</template>

<script>
import Card from '@/components/Card.vue';

export default {
  name: 'HomeView',
  components: {
    Card
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