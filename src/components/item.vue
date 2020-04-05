<template>
  <q-item
    clickable
    v-bind:class="{ 'bg-green-4' : isSelected }"
  >
    <q-item-section @click="$emit('SelectQuestion', question)">
      <q-item-label> {{ title }} - {{ question.videoBlob }} </q-item-label>
      <div class="row">
        <q-btn
          class="all-pointer-events"
          dense
          icon="play_arrow"
        />
        <q-btn
          dense
          icon="delete"
          @click="$emit('DeleteBlob', question)"
        />
      </div>
    </q-item-section>
  </q-item>
</template>

<script>

export default {
  props: ['title', 'question', 'isSelected'],

};
</script>

<style>
</style>
