<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Monitoreo de Usuarios</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-grid>
          <ion-row>
            <ion-col>
              <div>Clave</div>
            </ion-col>
            <ion-col>
              <div>Nombre</div>
            </ion-col>
            <ion-col>
              <div>Apellido</div>
            </ion-col>
            <ion-col>
              <div>Carrera</div>
            </ion-col>
            <ion-col>
              <div>Semestre</div>
            </ion-col>
          </ion-row>
          <ion-row v-for="(item, index) in listaUsuarios" :key="index">
            <ion-col>
              <div>{{listaKeys[index]}}</div>
            </ion-col>
            <ion-col>
              <div>{{item.nombre}}</div>
            </ion-col>
            <ion-col>
              <div>{{item.apellido}}</div>
            </ion-col>
            <ion-col>
              <div>{{item.carrera}}</div>
            </ion-col>
            <ion-col>
              <div>{{item.semestre}}</div>
            </ion-col>
          </ion-row>
        </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol } from '@ionic/vue';
import { getDatabase, ref, onValue } from "firebase/database"

export default defineComponent({
  name: 'Tab2Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonGrid, IonRow, IonCol },
  mounted() {
    const db = getDatabase();
    const starCountRef = ref(db, "usuario/");
    onValue(starCountRef, (snapshot) => {
      const data = snapshot.val();
      console.log(data);
    var cont = 0
      snapshot.forEach(element => {
        this.listaKeys[cont]=element.key
        this.listaUsuarios[cont] = element.toJSON()
        cont++
      });
    });
    console.log("lista de usuarios", this.listaUsuarios)
  },

  data(){ return{
  listaUsuarios: [{status:"", usuario:""}],
  listaKeys:[]
  }}

});
</script>
