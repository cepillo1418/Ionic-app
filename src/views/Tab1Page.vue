<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Register</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Register</ion-title>
        </ion-toolbar>
      </ion-header>

    
     <div>
     <ion-item>
      <ion-label>Name:</ion-label>
      <ion-input type="text" v-model="name"></ion-input>
     </ion-item>

     <ion-item>
        <ion-label>Mail:</ion-label>
        <ion-input type="mail" v-model="mail"></ion-input>
      </ion-item>

   <ion-item>
        <ion-label>Password:</ion-label>
        <ion-input type="password" v-model="password"></ion-input>
      </ion-item>

     <ion-item>
        <ion-label>Confirm password:</ion-label>
        <ion-input type="password" v-model="password_confirmation"></ion-input>
     </ion-item>
      
        <ion-button color="secondary" @click="addRegister">register</ion-button>
      
    </div>

    </ion-content>
  </ion-page>
</template>

<script>
import {defineComponent, ref} from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonInput, IonButton, IonItem, IonLabel } from '@ionic/vue';
import {HTTP} from '@awesome-cordova-plugins/http'

export default defineComponent({
  name: 'TabPage',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonInput, IonButton, IonItem, IonLabel },
  setup() {
    let name = ref()
    let mail = ref()
    let password = ref()
    let password_confirmation = ref()

    const addRegister = () => {
      HTTP.post(`http://localhost:8000/api/inscription`, {name}, {mail}, {password}, {password_confirmation})
          .then(response => {
            
            console.log(response.status)
            console.log(JSON.parse(response.data)[0].name) // data received by server
            console.log(response.headers)
          })
          .catch(error => {
            console.log(error.status)
            console.log(error.error) // error message as string
            console.log(error.headers)
          })
    }
        
   return {addRegister} 
  }
});
</script>
