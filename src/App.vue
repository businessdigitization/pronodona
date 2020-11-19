<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script>
import { IonApp, IonRouterOutlet } from '@ionic/vue'
import { useBackButton, useIonRouter } from '@ionic/vue'
import { Plugins } from '@capacitor/core'
const { App } = Plugins

export default {
  setup() {
    const ionRouter = useIonRouter()
    useBackButton(-1, () => {
      if (!ionRouter.canGoBack()) {
        App.exitApp()
      }
    })
  },
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet,
  },
}
</script>
