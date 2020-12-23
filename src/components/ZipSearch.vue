<template>
  <ion-grid fixed>
    <form @submit.prevent="onSubmit">
      <ion-row>
        <ion-col>
          <ion-item>
            <ion-label>Zipcode:</ion-label>
            <ion-input
              type="text"
              :value="zip"
              @input="zip = $event.target.value"
              placeholder="Enter US Zipcode"
              name="zip"
            ></ion-input>
          </ion-item>
        </ion-col>
        <ion-col size="12">
          <ion-button expand="block" type="submit" color="primary">
            Find
          </ion-button>
        </ion-col>
      </ion-row>
    </form>
  </ion-grid>
</template>

<script>
import {
  IonGrid,
  IonRow,
  IonCol,
  IonButton,
  IonInput,
  IonItem,
  IonLabel,
} from "@ionic/vue";

export default {
  components: {
    IonGrid,
    IonRow,
    IonCol,
    IonButton,
    IonInput,
    IonItem,
    IonLabel,
  },
  data: () => ({
    zip: "",
  }),
  methods: {
    onSubmit: function () {
      const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
      if (!isValidZip) this.showAlert();
      else this.$emit("get-zip", this.zip);
      this.zip = "";
    },
    showAlert: function () {
      const alert = document.createElement("ion-alert");
      alert.header = "Enter zipcode";
      alert.message = "Please enter valid US zipcod";
      alert.buttons = ["ok"];

      document.body.appendChild(alert);
      return alert.present();
    },
  },
};
</script>