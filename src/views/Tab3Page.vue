<template>
  <ion-page>

    <ion-content :fullscreen="true">
      <ion-grid>
        <ion-row style="min-height: calc(100vh - 70px)">
          <ion-col size="12">
            <h2 style="font-weight: bolder">ABOUT</h2>
          </ion-col>
          <ion-col size="12" class="ion-text-center ion-aling-slef-center">
            <p>Developed by: Klevis Sahitaj 05-2022</p>

          </ion-col>

        </ion-row>
      </ion-grid>


    </ion-content>
  </ion-page>
</template>

<script >
import { defineComponent } from 'vue';
import {
  IonPage,
  IonContent,
  IonGrid,
  IonRow,
  IonCol,
  // IonButton,
  // IonIcon,
} from "@ionic/vue";



export default defineComponent({
  name: "Tab3Page",
  components: {
    IonContent,
    IonPage,
    IonGrid,
    IonRow,
    IonCol,
    // IonButton,
    // IonIcon,

  },
});
</script>
