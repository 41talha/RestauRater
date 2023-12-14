<template>
  <div class="q-pa-md row justify-center">
    <q-table
      style="width:100vw"
      flat
      bordered
      card-container-class="justify-center"
      :grid="Screen.lt.lg"
      title="Todays Restaurants"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :filter="filter"
    >
      <!-- Table Image -->
      <template v-slot:body-cell-image="props">
        <td><q-img style="width: 150px" :src="`/images/${props.row.img}`" /></td>
      </template>

      <!-- Grid Card Mobiel Version -->
      <template v-slot:item="props">
        <div class="q-pa-md row q-gutter-md">
          <q-card class="">
            <q-img
              style="width: 294px; height: 250px; object-fit: cover"
              :src="`/images/${props.row.img}`"
            />
            <q-card-section>
              <div class="text-h6">{{ props.row.name }}</div>
              <div class="text-h9">{{ props.row.name }}</div>
              <div class="row q-gutter-md q-my-xs">
                <q-btn class="col">Share</q-btn>
                <q-btn class="col">Details</q-btn>
              </div>
            </q-card-section>

            <q-card-section class="q-pt-none">
            </q-card-section>
          </q-card>
        </div>
      </template>
      <!-- Buttons -->
      <template v-slot:body-cell-actions="props">
        <q-td class="q-gutter-md">
          <q-btn label="Share" color="primary" icon="ios_share"></q-btn>
          <q-btn label="Details" color="accent" icon="info"></q-btn>
        </q-td>
      </template>
    </q-table>
  </div>
</template>

<script setup>
import useDefaultStore from '@/stores/defaultStore.js';
import { Screen } from 'quasar';
const store = useDefaultStore();

const columns = [
  {
    name: 'image',
    required: true,
    label: 'Bild',
    align: 'left',
    field: 'img',
    format: (val) => `${val}`,
    sortable: false,
  },
  { name: 'adress', label: 'Adresse', field: 'adresse', sortable: false, align: 'left' },
  { name: 'actions', label: 'Aktionen', sortable: false, align: 'center' },
];

const rows = [
  {
    img: 'restaurant1.jpg',
    name: "Mo's Kitchen",
    fat: 6.0,
    carbs: 24,
    protein: 4.0,
    sodium: 87,
    calcium: '14%',
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant2.jpg',
    name: 'Nasip',
    fat: 9.0,
    carbs: 37,
    protein: 4.3,
    sodium: 129,
    calcium: '8%',
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant3.jpg',
    name: 'Burger Factory',
    fat: 16.0,
    carbs: 23,
    protein: 6.0,
    sodium: 337,
    calcium: '6%',
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant4.jpg',
    name: 'Nesil',
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant5.jpg',
    name: "Hossains Pizza",
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant6.jpg',
    name: "Gültekins Döner",
    adresse: 'Thaliastrasse 125',
  },
  {
    img: 'restaurant7.jpg',
    name: "Maisams Börek",
    adresse: 'Thaliastrasse 125',
  },
];
</script>
