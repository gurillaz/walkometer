<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-grid>
        <ion-row>
          <ion-col size="12">
            <h2 style="font-weight: bolder">SETTINGS</h2>
          </ion-col>
          <ion-col size="12" class="ion-aling-slef-center">
            <ion-card color="light" style="border: 2px solid white">
              <ion-card-content>
                <ion-row>
                  <ion-col size="4">
                    <h1
                      style="
                        font-weight: bolder;
                        color: white;
                        font-size: 2rem;
                        margin-top: 0%;
                      "
                    >
                      01-12
                      <!-- <span style="font-size:1rem;">2022</span> -->
                    </h1>
                  </ion-col>
                  <ion-col size="4" class="ion-text-center">
                    <h6
                      style="
                        color: grey;
                        font-weight: bold;
                        padding-bottom: 0px;
                        margin-bottom: 0px;
                      "
                    >
                      Max speed:
                    </h6>
                    <h1
                      style="
                        font-weight: bolder;
                        color: yellow;
                        font-size: 1rem;
                        margin-top: 0%;
                      "
                    >
                      23 km/h
                    </h1>
                  </ion-col>

                  <ion-col size="4" class="ion-text-center">
                    <h6
                      style="
                        color: grey;
                        font-weight: bold;
                        padding-bottom: 0px;
                        margin-bottom: 0px;
                      "
                    >
                      Avg speed:
                    </h6>
                    <h1
                      style="
																								font-weight: bolder;
																								color: green;s
																								font-size: 1rem;
																								margin-top: 0%;
																																													"
                    >
                      23 km/h
                    </h1>
                  </ion-col>
                </ion-row>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from "vue";
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
  name: "Tab2Page",
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
