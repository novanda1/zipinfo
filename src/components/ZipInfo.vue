<template>
  <ion-grid v-if="info">
    <ion-row>
      <ion-col size="12">
        <ion-card>
          <ion-card-header>
            <ion-card-subtitle>{{ info["post code"] }}</ion-card-subtitle>
            <ion-card-title>{{
              info["places"][0]["place name"]
            }}</ion-card-title>
          </ion-card-header>

          <ion-card-content>
            <ion-list>
              <ion-item>
                <ion-label>
                  <strong>State:</strong>
                  {{ info["places"][0]["state"] }} ({{
                    info["places"][0]["state abbreviation"]
                  }})
                </ion-label>
              </ion-item>
              <ion-item>
                <ion-label>
                  <strong>Latitude:</strong>
                  {{ info["places"][0]["latitude"] }}
                </ion-label>
              </ion-item>
              <ion-item>
                <ion-label>
                  <strong>Longitude:</strong>
                  {{ info["places"][0]["longitude"] }}
                </ion-label>
              </ion-item>
            </ion-list>
          </ion-card-content>
        </ion-card>
      </ion-col>
      <ion-col size="12">
        <ion-button v-on:click="$emit('clearInfo')" expand="block" color="light">
          Clear
        </ion-button>
      </ion-col>
    </ion-row>
  </ion-grid>
</template>

<script>
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonList,
  IonItem,
  IonLabel,
  IonButton,
} from "@ionic/vue";

export default {
  name: "ZipInfo",
  props: {
    info: Object,
  },
  components: {
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonCardSubtitle,
    IonCardContent,
    IonList,
    IonItem,
    IonLabel,
    IonButton,
  },
};
</script>