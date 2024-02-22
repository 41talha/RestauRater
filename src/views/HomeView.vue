<template>
  <div class="q-pa-md row justify-center">
    <q-table
      style="width: 100vw"
      flat
      bordered
      card-container-class="justify-center"
      grid
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

      <!-- Grid Card Mobile Version -->
      <template v-slot:item="props">
        <div class="q-pa-lg row q-gutter-lg">
          <q-card class="">
            <q-img
              style="width: 294px; height: 250px; object-fit: cover"
              :src="`/images/${props.row.img}`"
            />
            <q-card-section>
              <div class="text-h6">{{ props.row.name }}</div>
              <div class="text-h9">{{ props.row.type }}</div>
              <div class="row q-gutter-md q-my-xs">
                <q-btn @click="dialog(props.row)" color="primary" class="col">Rate</q-btn>
                <q-btn color="accent" class="col">Details</q-btn>
              </div>
            </q-card-section>

            <q-card-section class="q-pt-none"> </q-card-section>
          </q-card>
        </div>
      </template>
      <!-- Buttons -->
      <template v-slot:body-cell-actions="props">
        <q-td class="q-gutter-md">
          <q-btn @click="dialog(props.row)" label="Rate" color="primary" icon="ios_share"></q-btn>
          <q-btn @click="dialog(props.row)" label="Details" color="accent" icon="info"></q-btn>
        </q-td>
      </template>
    </q-table>
    <!--  -->
    <q-dialog v-model="show">
      <q-card class="my-card">
        <q-img
              style="width: 330px; height: 250px;"
              :src="`/images/${restaurantD.img}`"
            />
        <q-card-section>
          <q-btn
            fab
            color="primary"
            icon="place"
            class="absolute"
            style="top: 0; right: 12px; transform: translateY(-50%)"
          />

          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">{{ restaurantD.name }}</div>
          </div>

          <q-rating v-model="stars" :max="5" size="32px" />
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-subtitle1">{{ restaurantD.category}}, {{ restaurantD.type}}</div>
          <div class="text-caption text-grey">
            Small plates,  & sandwiches in an intimate setting.
          </div>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right">
          <q-btn v-close-popup flat color="primary" label="Reserve" />
          <q-btn v-close-popup flat color="primary" round icon="event" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script setup>
import useDefaultStore from '@/stores/defaultStore.js';
import { ref } from 'vue';
import { Screen } from 'quasar';
const store = useDefaultStore();

const show = ref(false);

const restaurantD = ref();

const dialog = (restaurant) => {
  show.value = true;
  restaurantD.value = restaurant;
  console.log('funktioniert');
};

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
    category: 'Arabic',
    type: 'Restaurant'
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
    category: 'Kurdish',
    type: 'Restaurant'

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
    category: 'American',
    type: 'Restaurant'

  },
  {
    img: 'restaurant4.jpg',
    name: 'Nesil',
    adresse: 'Thaliastrasse 125',
    category: 'Turkish',
    type: 'Restaurant'

  },
  {
    img: 'restaurant5.jpg',
    name: 'Hossains Pizza',
    adresse: 'Thaliastrasse 125',
    category: 'Pakistani',
    type: 'Restaurant'

  },
  {
    img: 'restaurant6.jpg',
    name: 'Gültekins Döner',
    adresse: 'Thaliastrasse 125',
    category: 'Turkish',
    type: 'Imbiss'

  },
  {
    img: 'restaurant7.jpg',
    name: 'Maisams Börek',
    adresse: 'Thaliastrasse 125',
    category: 'Afghan',
    type: 'Bakery'

  },
];


self.addEventListener('install', event => {
  console.log('Service Worker installiert');
});

self.addEventListener('activate', event => {
  console.log('Service Worker aktiviert');
});

self.addEventListener('fetch', event => {
  console.log('Service Worker holt Ressource: ', event.request.url);
  event.respondWith(
    caches.match(event.request).then(response => {
      return response || fetch(event.request);
    })
  );
});

self.addEventListener('push', event => {
  console.log('Push-Benachrichtigung empfangen');
});

if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(registration => {
        console.log('Service Worker registriert: ', registration);
      })
      .catch(error => {
        console.log('Service Worker Registrierung fehlgeschlagen: ', error);
      });
  });
}

</script>
