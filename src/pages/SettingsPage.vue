<template>
  <q-page class="flex justify-start column">
    <q-tabs
      v-model="tab"
      inline-label
      outside-arrows
      mobile-arrows
      class="bg-blue-grey-10 text-white shadow-2"
    >
      <q-tab name="general" icon="display_settings" label="General" />
      <q-tab name="damage_meter" icon="speed" label="Damage Meter" />
      <!-- <q-tab name="upload_logs" icon="cloud_upload" label="Log Uploading" /> -->
      <q-tab name="log" icon="article" label="Log " />
    </q-tabs>
    <q-scroll-area style="height: calc(100vh - 124px); padding: 8px 16px">
      <GeneralPage v-if="tab === 'general'" />
      <DamageMeterPage v-if="tab === 'damage_meter'" />
      <UploadPage v-if="tab === 'upload_logs'" />
      <LogPage v-if="tab === 'log'" />
    </q-scroll-area>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import GeneralPage from "src/components/SettingsPage/GeneralPage.vue";
import DamageMeterPage from "src/components/SettingsPage/DamageMeterPage.vue";
import UploadPage from "src/components/SettingsPage/UploadPage.vue";
import LogPage from "src/components/SettingsPage/LogPage.vue";

import { useSettingsStore } from "src/stores/settings";
const settingsStore = useSettingsStore();

let tab = ref("general");

settingsStore.$subscribe(() => {
  window.messageApi.send("window-to-main", {
    message: "save-settings",
    value: JSON.stringify(settingsStore.settings),
  });
});
</script>
