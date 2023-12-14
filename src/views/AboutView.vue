<template>
  <div class="q-pa-md row items-start q-gutter-md">
    <q-card class="my-card">
      <q-card-section>
        <h5>Impressum</h5>
        Implementiert von Talha Canli  
        © HTL WIEN WEST 2023
      </q-card-section>
    </q-card>
  </div>
</template>
<script setup>
import useDefaultStore from '@/stores/defaultStore.js';

const store = useDefaultStore();

console.log('Talha Canli  :)')
</script>
