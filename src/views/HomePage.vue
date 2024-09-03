<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div class="readerQR">
        <StreamBarcodeReader
          v-if="scanReader == true"
          @decode="onDecode"
          @loaded="onLoaded"
        ></StreamBarcodeReader>
        <div>
          <ion-button @click="isOpen()">{{ textBtn }} Scanner</ion-button>
        </div>
      </div>

      <p>{{ outputReader }}</p>

      <div id="container">
        <div class="showQR" v-if="showQR == true">
          <qrcode-vue :value="value" :size="size" level="H" />
        </div>
        <div>
          <ion-button @click="isShowQR()">{{ textBtnQR }} QR</ion-button>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
// scanner barcode
import QrcodeVue from "qrcode.vue";
import { StreamBarcodeReader } from "vue-barcode-reader";
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButton,
} from "@ionic/vue";

export default {
  components: {
    IonContent,
    IonHeader,
    IonTitle,
    IonPage,
    IonToolbar,
    IonButton,
    StreamBarcodeReader,
    QrcodeVue,
  },

  data() {
    return {
      scanReader: false,
      textBtn: "Open",
      showQR: false,
      textBtnQR: "Open",
      value: "MD001/MC001/1",
      size: 300,
      outputReader: "",
    };
  },

  methods: {
    isShowQR() {
      if (this.showQR == false) {
        this.showQR = true;
        this.textBtnQR = "Close";
      } else {
        this.showQR = false;
        this.textBtnQR = "Open";
      }
    },
    isOpen() {
      if (this.scanReader == false) {
        this.scanReader = true;
        this.textBtn = "Close";
      } else {
        this.scanReader = false;
        this.textBtn = "Open";
      }
    },

    onDecode(result) {
      this.outputReader = result;
    },
  },
};
</script>

<style scoped>
.readerQR {
  margin-top: 20px;
  text-align: center;
}

#container {
  margin-top: 30px;
  text-align: center;
}

.showQR {
  padding: 20px 0;
  background-color: white;
}
</style>
