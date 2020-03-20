<template>
  <v-timeline-item fill-dot small color="rgb(63,182,220)">
    <v-card>
      <v-card-text>
        <span >{{item.location}}</span>
        <span >
            {{ item.time }}
        </span>
      </v-card-text>
    </v-card>
  </v-timeline-item>
</template>

<script>
export default {
  props: [
      'item'
  ],
  created(){
      console.log(this.item)
  }
};
</script>

<style></style>
