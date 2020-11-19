<template>
  <ion-page>
    <ion-header :translucent="true" color="secondary">
      <ion-toolbar color="secondary">
        <ion-title>প্রণোদনা ক্যালকুলেটর</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">প্রণোদনা1</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="container">
        <ion-list lines="full" class="ion-no-margin">
          <ion-item>
            <ion-label position="floating"
              >যত পাঠাবেন(ডলার, রিঙ্গিত ইত্যাদি)
            </ion-label>
            <ion-input
              type="number"
              required="true"
              v-model="exchangeAmount"
            ></ion-input>
          </ion-item>
          <ion-item>
            <ion-label position="floating"
              >এক্সচেঞ্জ রেট(যেমন ডলার টু টাকা)</ion-label
            >
            <ion-input
              type="number"
              required="true"
              v-model="exchangeRate"
            ></ion-input>
          </ion-item>
          <ion-item>
            <ion-label position="floating">প্রণোদনার হার</ion-label>
            <ion-input type="number" required="true" v-model="incentiveRate">
            </ion-input>
          </ion-item>
        </ion-list>
        <ion-button color="secondary" @click="calculate()"
          >হিসেব করুন</ion-button
        >

      <ion-row v-if="calculationComplete">
        <ion-col size="6">
          <ion-card>
            <ion-card-content>
              <ion-text color="success" class="ion-text-center">
                <p>{{ Math.round(incentiveAmount * 100) / 100 }}&nbsp;টাকা</p>
              </ion-text>
              <ion-text class="ion-text-center">
                <p>প্রণোদনা পাবেন</p>
              </ion-text>
            </ion-card-content>
          </ion-card>
        </ion-col>

        <ion-col size="6">
          <ion-card>
            <ion-card-content>
              <ion-text color="success" class="ion-text-center">
                <p>{{ Math.round(convertedAmountWithIncentive * 100) / 100 }}&nbsp;টাকা</p>
              </ion-text>
              <ion-text class="ion-text-center">
                <p>প্রণোদনা সহ মোট</p>
              </ion-text>
            </ion-card-content>
          </ion-card>
        </ion-col>
      </ion-row>
      </div>
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
  IonInput,
  IonLabel,
  IonCardContent,
  IonButton,
  IonItem,
  IonList,
  IonCard,
  IonRow,
  IonCol,
  IonText,
} from '@ionic/vue'

export default {
  name: 'Home',
  data: () => ({
    exchangeAmount: null,
    exchangeRate: null,
    incentiveRate: 2,
    incentiveAmount: null,
    convertedAmountWithoutIncentive: null,
    convertedAmountWithIncentive: null,
    calculationComplete: false,
  }),
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonInput,
    IonLabel,
    IonCardContent,
    IonCard,
    IonList,
    IonItem,
    IonButton,
    IonRow,
    IonCol,
    IonText,
  },
  methods: {
    calculate() {
      this.convertedAmountWithoutIncentive =
        this.exchangeAmount * this.exchangeRate
      this.incentiveAmount =
        this.convertedAmountWithoutIncentive * (this.incentiveRate / 100.0)
      this.convertedAmountWithIncentive =
        this.convertedAmountWithoutIncentive + this.incentiveAmount
      this.calculationComplete = true
    },
  },
}
</script>
