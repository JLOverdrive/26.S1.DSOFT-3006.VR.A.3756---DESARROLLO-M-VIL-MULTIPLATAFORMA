<template>
  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>Login</ion-title>
        <ion-buttons slot="end">
          <ion-button fill="solid" @click="router.push({ name: 'Registro' })">
            Registro
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding login-background">

      <div class="login-container">

        <ion-card class="login-card animate__animated animate__fadeInUp">

          <ion-card-header>
            <ion-card-title class="card-title">
              Riksiri
            </ion-card-title>
            <ion-card-subtitle class="card-subtitle">
              Inicia sesión para continuar
            </ion-card-subtitle>
          </ion-card-header>

          <ion-card-content>

            <!-- Input Usuario -->
            <ion-item class="ion-margin-top input-item" lines="none">
              <ion-icon :icon="personOutline" slot="start"></ion-icon>
              <ion-input
                label="Usuario"
                label-placement="floating"
                fill="outline"
                v-model="userStore.login.username"
                placeholder="Escribe tu usuario">
              </ion-input>
            </ion-item>

            <!-- Input Contraseña -->
            <ion-item class="ion-margin-top input-item" lines="none">
              <ion-icon :icon="lockClosedOutline" slot="start"></ion-icon>
              <ion-input
                label="Contraseña"
                label-placement="floating"
                fill="outline"
                type="password"
                v-model="userStore.login.password"
                placeholder="Escribe tu contraseña"
                @keyup.enter="login">
              </ion-input>
            </ion-item>

            <!-- Botón Ingresar -->
            <ion-button expand="block" class="ion-margin-top login-button" @click="login">
              Ingresar
            </ion-button>

          </ion-card-content>

        </ion-card>

      </div>

    </ion-content>

  </ion-page>
</template>

<script setup lang="ts">
import { 
  IonContent, 
  IonHeader, 
  IonTitle, 
  IonToolbar, 
  IonPage, 
  IonInput, 
  IonButtons, 
  IonButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonItem,
  IonIcon,
  alertController 
} from '@ionic/vue';

import { useRouter } from 'vue-router';
import { useUserStore } from '@/stores/user';

// IMPORTAR LOS ICONOS CORRECTAMENTE
import { personOutline, lockClosedOutline } from 'ionicons/icons';

const userStore = useUserStore();
const router = useRouter();

function login() {
    userStore.$login().then(() => {
        router.push({ name: 'Seccion' });
    }).catch(error => {
        alertController.create({
            header: 'Error',
            message: error.response?.data?.message || 'Hubo un error',
            buttons: ['Continuar']
        }).then(alert => alert.present());
    });
}
</script>

<style scoped>
/* Contenedor centralizado */
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

/* Tarjeta moderna */
.login-card {
  width: 100%;
  max-width: 400px;
  border-radius: 20px;
  box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  background-color: rgba(255,255,255,0.95);
  padding: 20px;
}

/* Títulos centrados */
.card-title, .card-subtitle {
  text-align: center;
}

/* Inputs con estilo uniforme */
.input-item {
  --border-radius: 12px;
  --padding-start: 10px;
  --padding-end: 10px;
}

/* Iconos a la izquierda */
ion-item ion-icon {
  color: #4f46e5;
  font-size: 24px;
  min-width: 32px;
  margin-right: 12px;
}

/* Efecto al enfocar input */
ion-item:focus-within ion-icon {
  color: #06b6d4;
  transform: scale(1.2);
  transition: 0.3s;
}

/* Botón profesional */
.login-button {
  --border-radius: 12px;
  --box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  --background: #4f46e5;
  --color: #ffffff;
  --padding-start: 20px;
  --padding-end: 20px;
}

.login-button:hover {
  --background: #3730a3;
}
</style>