<template>
  <q-drawer side="left" bordered :width="250" :breakpoint="500">
    <q-scroll-area class="fit">
      <q-list padding class="menu-list">
        <q-item to="/" clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="r_inbox" />
          </q-item-section>

          <q-item-section> Home </q-item-section>
        </q-item>

        <q-item to="/About" clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="r_star" />
          </q-item-section>

          <q-item-section> Impressum </q-item-section>
        </q-item>
      </q-list>
    </q-scroll-area>
  </q-drawer>
</template>
<script setup></script>
