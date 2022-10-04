<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 2</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>

      <div>
        <ion-item>
          <ion-label>Mail:</ion-label>
          <ion-input type="mail" v-model="mail"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label>Password:</ion-label>
          <ion-input type="password" v-model="password"></ion-input>
        </ion-item>

        <ion-button color="secondary" @click="Connexion">Connexion</ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import {defineComponent, ref} from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonInput, IonButton, IonItem, IonLabel } from '@ionic/vue';
import {HTTP} from '@awesome-cordova-plugins/http'

export default defineComponent({
  name: 'Tab1Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonInput, IonButton, IonItem, IonLabel },
  setup() {
 
    let mail = ref()
    let password = ref()
   

    const Connexion = () => {
      HTTP.get(`http://localhost:8000/api/connexion`,  {mail}, {password})
      .then(data => {

console.log(data.status);
console.log(data.data); // data received by server
console.log(data.headers);

})
          .catch(error => {
            console.log(error.status)
            console.log(error.error) // error message as string
            console.log(error.headers)
          })
    }
        
    return {Connexion}
  }
});
</script>
