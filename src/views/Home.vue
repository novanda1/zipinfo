<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Zip Info Git </ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <zip-search @get-zip="getZipInfo" />
      <zip-info :info="info" @clearInfo="clearZipInfo" />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import ZipSearch from "../components/ZipSearch.vue";
import ZipInfo from "../components/ZipInfo.vue";

export default {
  name: "Home",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    ZipSearch,
    ZipInfo,
  },
  data: () => ({
    info: null,
  }),
  methods: {
    getZipInfo: async function (zip) {
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);
      const info = await res.json();
      if (res.status == 404) this.showAlert();
      this.info = info;
    },
    clearZipInfo: function () {
      this.info = null;
    },
    showAlert: function () {
      const alert = document.createElement("ion-alert");
      alert.header = "Not Valid";
      alert.message = "Please enter valid US zipcod";
      alert.buttons = ["ok"];
      document.body.appendChild(alert);
      return alert.present();
    },
  },
};
</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>