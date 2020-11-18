<template>
  <ion-page>
    <ion-header :translucent="true" color="secondary">
      <ion-toolbar color="secondary">
        <ion-title>প্রণোদনা হিসেব করুন</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">প্রণোদনা হিসেব করুন</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="container">
        <ion-list lines="full" class="ion-no-margin">
          <ion-item>
            <ion-label position="floating"
              >ডলার/রিয়ালের পরিমাণ
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

        <ion-card v-if="calculationComplete">
          <ion-card-header>
            <ion-card-title>ফলাফল</ion-card-title>
          </ion-card-header>

          <ion-card-content>
            <ion-item-divider>
              প্রণোদনার পরিমাণ &nbsp;<ion-text color="primary">
                {{ incentiveAmount }}
              </ion-text>
              &nbsp;টাকা
            </ion-item-divider>
            <ion-item-divider>
              প্রণোদনা বাদে&nbsp;<ion-text color="primary">
                {{ convertedAmountWithoutIncentive }}
              </ion-text>
              &nbsp;টাকা
            </ion-item-divider>
            <ion-item-divider>
              প্রণোদনা সহ &nbsp;<ion-text color="primary">
                {{ convertedAmountWithIncentive }}
              </ion-text>
              &nbsp;টাকা
            </ion-item-divider>
          </ion-card-content>
        </ion-card>
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
  IonItemDivider,
  IonButton,
  IonItem,
  IonList,
  IonCard,
  IonCardHeader,
  IonCardTitle,
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
    IonItemDivider,
    IonCardContent,
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonList,
    IonItem,
    IonButton,
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

<style scoped></style>
