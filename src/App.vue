<template>
  <div class="wrapper">
    <div class="container">
      <div class="inner">
        <ul class="timer-list">
          <component
            v-for="(component, index) in components"
            :key="index"
            :is="component"
          />
          <NewTimer @addComponentTimer="addTimer()"/>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import TimerItemT from '@/components/TimerItemT.vue';
import TimerItemR from '@/components/TimerItemT.vue';
import TimerItemS from '@/components/TimerItemT.vue';
import NewTimer from '@/components/NewTimer.vue';

export default {
  name: 'App',
  components: {TimerItemT, NewTimer},
  data: () => ({
    components: [TimerItemT]
  }),
  methods: {
    addTimer() {
      this.components.push(TimerItemT);
    }
  }
}
</script>

<style lang="scss" scoped>
.timer-list {
  --grid-template-columns: 4;
  display: grid;
  grid-template-columns: repeat(var(--grid-template-columns), 1fr);
  gap: 25px 30px;
  @media (max-width: 1024px) {
    --grid-template-columns: 3;
  }
  @media (max-width: 768px) {
    --grid-template-columns: 2;
  }
  @media (max-width: 540px) {
    --grid-template-columns: 1;
  }
}
</style>