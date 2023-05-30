<template>
  <ion-page>
    <ion-content :fullscreen="true" v-if="start === true">
      <ion-grid>
        <ion-row style="min-height: calc(100vh - 70px)">
          <ion-col size="12">
            <h2 style="font-weight: bolder">WALKOMETER</h2>
          </ion-col>
          <ion-col size="12" class="ion-text-center">
            <ion-card color="light" style="border: 2px solid white">


              <ion-card-content>



                <h6 style="
                color: grey;
                font-weight: bold;
                padding-bottom: 0px;
                margin-bottom: 0px;
              ">
                  CURRENT SPEED:
                </h6>
                <h1 style="
                font-weight: bolder;
                color: green;
                font-size: 5rem;
                margin-top: 0%;
              ">
                  {{ Math.round(current_speed) }} km/h
                </h1>


                <hr />
                <hr />
                <div class="ion-text-left">
                  <p style="
                  color: grey;
                  font-weight: bold;
                  padding-bottom: 0px;
                  margin-bottom: 0px;
                ">
                    AVERAGE SPEED:
                    <span style="color: green">{{ Math.round(average_speed) }} m/h</span>
                  </p>
                  <p style="
                  color: grey;
                  font-weight: bold;
                  padding: 0px;
                  margin: 0px;
                ">
                    GPS Data:
                    <span style="color: green">{{ current_lat }} - {{ current_long }}</span>
                  </p>
                </div>
              </ion-card-content>
            </ion-card>
          </ion-col>

          <ion-col size="4" class="ion-flex ion-align-self-end">
            <ion-button color="danger" expand="block" fill="outline" @click="stop()">Stop</ion-button>
          </ion-col>
          <ion-col size="8" class="ion-align-self-end">
            <ion-button color="dark" expand="block" fill="outline" @click="pause_toggle()">
              {{ pause ? 'Pause' : 'Contine' }}


            </ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>

    <ion-content :fullscreen="true" v-if="start === false">
      <ion-grid>
        <ion-row class="ion-justify-content-center ion-align-items-center" style="height: 90vh">
          <ion-col size="10">
            <p class="ion-text-center">
              <ion-icon :icon="footstepsSharp" style="font-size: 130px"></ion-icon>
            </p>
            <p class="ion-text-center">Press START to continue!</p>
            <hr />
            <hr />
            <ion-button expand="block" color="primary" @click="start = true">
              Start</ion-button>
          </ion-col>
        </ion-row>

        <!-- <ion-row>
          <ion-col>
            <ion-button
              style="margin-top: 65vh"
              expand="block"
              @click="start = true"
              >Start</ion-button
            >
          </ion-col>
        </ion-row> -->
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script >
import { defineComponent } from "vue";
import {
  IonPage,
  IonContent,
  IonButton,
  IonGrid,
  IonRow,
  IonCol,
  IonIcon,
  // IonText,
  IonCard,
  IonCardContent,
} from "@ionic/vue";

// import {
// footstepsSharp
// } from 'ionicons/icons';

import { Geolocation } from "@awesome-cordova-plugins/geolocation";

import { footstepsSharp } from "ionicons/icons";

import { LocalNotifications } from "@awesome-cordova-plugins/local-notifications";

import { Vibration } from '@awesome-cordova-plugins/vibration';

// const { Gelocation } = Plugins;

export default defineComponent({
  name: "Tab1Page",
  components: {
    IonContent,
    IonPage,
    IonButton,
    IonGrid,
    IonRow,
    IonCol,
    IonIcon,
    IonCard,
    IonCardContent,


    // IonText,
  },
  data() {
    return {
      pause: false,
      start: false,
      active: false,
      current_speed: 0,
      average_speed: 0,
      current_lat: "",
      current_long: "",
      geolocation_instance: null,
      footstepsSharp,
    };
  },
  methods: {

    pause_toggle() {
      this.pause = !this.pause;

    },

    stop() {
      this.active = !this.active;
      this.start = false;
      alert("Stoped");

    },



    async show_notification() {
      Vibration.vibrate(100);


      await LocalNotifications.schedule({
        title: "My first notification",
        text: "Thats pretty easy...",
        foreground: true,
      });


    },
    get_location_data() {
      if (this.start === false || this.pause == true) {
        console.log("Press Start to continue!");
        return;
      }
      // maximumAge: Accept a cached position whose age is no greater than the specified time in milliseconds. (Number)
      var options = {
        maximumAge: 1000,
        timeout: 800,
        enableHighAccuracy: true,
      };

      Geolocation.watchPosition(options).subscribe((resp) => {
        if (resp.coords === undefined) {
          console.log(resp.message);
          return;
        }
        // console.log(resp.coords.latitude);
        // console.log(resp.coords.longitude);
        // console.log(resp.coords);
        if (resp.coords.speed) {
          this.current_speed = resp.coords.speed * 3.6;

          this.average_speed = (this.average_speed+this.current_speed/2);
        }

        this.current_lat = resp.coords.latitude;
        this.current_long = resp.coords.longitude;
      });


    },
  },

  mounted() {
    // console.log(`The initial count is ${this.count}.`)

    this.get_location_data();
    // console.log(`Current speed ${this.current_speed}.`);
    // console.log(`GPS Cordinates ${this.current_lat} - ${this.current_long}.`);
  },

  watch: {
    active() { },
  },
});
</script>
