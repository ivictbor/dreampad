<template>
  <div class="holder">
    <div>
      
      <b-alert variant="success" :key='key' v-for="(dream, key) in dreams" show>
        <svgicon v-if="dream.share == 'yes'"  icon="share" width="24" height="24"></svgicon>    
        {{ dream.description }}
      </b-alert>

      <b-button @click="$router.push({name:'create'})" >
            <font-awesome-icon icon="plus" />
            Add dream
      </b-button>
    </div>
  </div>
</template>

<script>
  
  import { mapState } from 'vuex';

  export default {
    computed: {
      ...mapState(['dreams']),
    }
  }
</script>

<style lang="scss" scoped>
.holder {
  position: absolute;
  top:0;
  bottom: 0;
  right: 0;
  left: 0;
  background-color: rgba(white, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;

  .svg-icon {
    fill:#aaa;
  }
}

</style>
