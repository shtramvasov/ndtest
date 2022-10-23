<template>
  <div class="card flex rounded-4" :style="{'background-image': 'url(' + require(`@/assets/img/${preview_img_path}`)}">
    <div class="wrapper rounded-4">
      <div class="content flex cols jcsb">
        <div class="flex cols gap-12">
          <p class="caption white--text"><span class="badge blue rounded-2">{{ series }}</span></p>
          <h5 class="mobile-size white--text">{{ title }}</h5>
        </div>
        <h5 class="mobile-size white--text">{{ cost }} {{ cost_currency }}</h5>
        <p class="arrow bold white--text">
          Подробнее
          <svg width="20" height="10" viewBox="0 0 20 10">
            <path d="M1 5H19M19 5L15.1 9M19 5L15.1 1" stroke="white" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </p>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  props: {
    preview_img_path: String,
    title: String,
    cost: Number,
    cost_currency: String,
    series: String,
  },
  }
</script>
<style lang="scss">
@import '../assets/styles/breakpoints';
@import '../assets/styles/variables';

.card {
  background-repeat: no-repeat;
  background-size: cover;
  cursor: pointer;
  padding: 9rem 0 0; 
  height: 400px;
  transition: $transition;
  overflow: hidden;

  &:hover 
    .wrapper {
      background: linear-gradient(hsl(221 23 39 / 0.5),hsl(221 23 39 / 0.9));
      transform: translateY(-9rem);
    .content {
      transform: translateY(5.5rem);
      .arrow {
        opacity: 1;
        transform: translateY(1rem);
      }
    }
  }     
}

.wrapper {
  width: 100%;
  height: 400px;
  padding: 3.5rem 1.875rem 1.25rem;
  transition: $transition;
  transform: translateY(3rem);

  .content {
    position: relative;
    transition: $transition;
    height: 50%;
    transform: translateY(-4rem);

    h5 {
      text-transform: uppercase;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
    }
  
    .badge {
      display: inline-flex;
      padding: 2px 0.625rem;
    }
  
    .arrow {
      position: absolute;
      bottom: -2rem;
      transition: $transition;
      opacity: 0;
    }
  }
}

@media (max-width: $screen-small) {
  .card {
    height: 300px;
    padding: 9rem 0 0;

    &:hover 
      .wrapper {
        .content {
          transform: translateY(6rem);
          .arrow {
            opacity: 1;
            transform: translateY(0.5rem);
          }
        }
      }
  }

  .wrapper {
    height: 300px;
    padding: 0.9375rem 0.9375rem;
    transform: translateY(2rem);

    h5 {
      font-size: 0.875rem; // 14px
      line-height: 1.375rem; // 22px
    }
  }
}
</style>