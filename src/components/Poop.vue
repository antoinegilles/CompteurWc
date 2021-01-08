<template>
  <div class="hello">
    <h1>Combien de temps as tu passés aux toilettes dans ta vie ?</h1>

    <v-form class="formulaire" ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="tmpsPipi"
        label="Temps passé pour les PETITS besoins (mn) ?"
        required
        filled
        dense
        rounded
        type="number"
        @change="reset = false"
      ></v-text-field>
      <v-text-field
        v-model="jrsPipi"
        label="Nombres de fois par jour pour les petits besoins ?"
        required
        filled
        dense
        rounded
        type="number"
        @change="reset = false"
      ></v-text-field>
      <v-text-field
        v-model="tmpsCaca"
        label="Temps passé pour les GROS besoins (mn) ?"
        required
        filled
        dense
        rounded
        type="number"
        @change="reset = false"
      ></v-text-field>
      <v-text-field
        v-model="jrsCaca"
        label="Nombres de fois par jour pour les gros besoins ?"
        required
        filled
        dense
        rounded
        type="number"
        @change="reset = false"
      ></v-text-field>
      <v-text-field
        v-model="age"
        label="Quel âge as-tu"
        required
        filled
        dense
        rounded
        type="number"
        @change="reset = false"
      ></v-text-field>
    </v-form>

    <div @click="calcul" class="circle">
      <div class="roll">
        <div class="sheetHolder">
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
        </div>
        <div class="paper">
          <div class="tube"></div>
        </div>
        <div class="paperHang">
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
          <div class="sheet"></div>
        </div>
      </div>
    </div>
    <p>Clique pour afficher les résultats</p>

    <br />

    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="headline grey lighten-2">
          Résultats
        </v-card-title>

        <v-card-text>
          <div v-if="reset">
            <h4>
              Tu as passés <b class="result">{{ result }}</b> minutes ,
              <b class="result">{{ resultHeure }}</b> heures et
              <b class="result">{{ resultJours.toFixed(1) }}</b> jours aux
              toilettes dans ta vie !
            </h4>
            <h4>
              Soit <b class="result">{{ resultSemaine.toFixed(1) }}</b> semaines
              ou <b class="result">{{ resultMois.toFixed(1) }}</b> mois !
            </h4>
          </div>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="dialog = false"> Fermer </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      tmpsPipi: "",
      jrsPipi: "",
      tmpsCaca: "",
      jrsCaca: "",
      age: "",
      result: "",
      resultHeure: "",
      resultJours: "",
      resultSemaine: "",
      resultMois: "",
      reset: false,
      dialog: false,
    };
  },
  methods: {
    calcul() {
      if (
        this.tmpsPipi < 0 ||
        this.jrsPipi < 0 ||
        this.tmpsCaca < 0 ||
        this.jrsCaca < 0 ||
        this.age < 0
      ) {
        alert("Les données ne peuvent être négative !");
      } else if (
        this.tmpsPipi == "" ||
        this.jrsPipi == "" ||
        this.tmpsCaca == "" ||
        this.jrsCaca == "" ||
        this.age == ""
      ) {
        alert("les données ne peuvent être vide !");
      } else if (
        this.tmpsPipi == null ||
        this.jrsPipi == null ||
        this.tmpsCaca == null ||
        this.jrsCaca == null ||
        this.age == null
      ) {
        alert("les données ne peuvent être nulle !");
      } else {
        const audio = new Audio(require('../assets/chassedo.mp3'))
        audio.play()
        this.dialog = true
        let calcul =
          (this.jrsPipi * this.tmpsPipi + this.jrsCaca * this.tmpsCaca) *
          (this.age * 365);

        this.result = calcul;
        this.resultHeure = calcul / 60;
        this.resultJours = calcul / 1440;
        this.resultSemaine = calcul / 10080;
        this.resultMois = calcul / 40320;
        this.reset = true;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.result {
  color: rgb(139, 37, 37);
}
.formulaire {
  padding-left: 10%;
  padding-right: 10%;
  padding-top: 4em;
}
.hello {
  text-align: center;
}
</style>
<style lang="scss" scoped>
body {
  padding: 0px;
  margin: 0px;
  background-color: #7dd;
}

$speed: 1s;

.circle {
  position: relative;
  top: 20px;
  width: 300px;
  height: 300px;
  border: solid;
  border-radius: 200px;
  background-color: #444;
  border-color: #444;
  margin: 0 auto;
  box-shadow: 0 0px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
}

.roll {
  position: relative;
  top: 80px;
  left: 30px;
  width: 250px;
  height: 150px;
  background-color: #eee;
  border-radius: 200px;
  -webkit-transition: all $speed ease;
  transition: all $speed ease;
  transform: scale(0.8, 1);
  cursor: pointer;
}

.roll:hover .paperHang {
  height: 200px;
}
.roll:active .paperHang {
  height: 220px;
}
.roll:hover .paperHang .sheet {
  top: -20px;
}

.roll:active .paperHang .sheet:nth-child(3) {
  margin-top: 20px;
}

.roll:hover .sheetHolder .sheet {
  top: -20px;
}

.paper {
  position: absolute;
  width: 150px;
  height: 150px;
  background-color: #ddd;
  border-radius: 200px;
  overflow: hidden;
  z-index: 20;
}
.tube {
  width: 55px;
  height: 55px;
  background-color: #aa9b83;
  border-radius: 200px;
  top: 47.5px;
  left: 47.5px;
  position: absolute;
  border: solid;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-color: #686154;
  border-width: thin;
  background: -webkit-linear-gradient(#614c2a, #a79a82);
  background: -o-linear-gradient(#614c2a, #a79a82);
  background: -moz-linear-gradient(#614c2a, #a79a82);
  background: linear-gradient(#614c2a, #a79a82);
}
.paperHang {
  width: 100px;
  height: 50px;
  top: 75px;
  left: 150px;
  position: absolute;
  overflow: hidden;
  -webkit-transition: all $speed ease;
  transition: all $speed ease;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19);
}
p {
  width: 100%;
  color: #555;
  font-size: 1.5em;
  font-family: "lato", sans-serif;
  font-style: normal;
  font-weight: 700;
  text-align: center;
  line-height: 5em;
}
.sheet {
  margin-top: 0px;
  top: -175px;
  width: 600px;
  height: 75px;
  background-color: #eee;
  position: relative;
  -webkit-transition: all $speed ease;
  transition: all $speed ease;
  border: dashed;
  border-color: #999;
  border-width: thin;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-left: 0;
  border-right: 0;
  border-bottom: 0;
}
.sheetHolder {
  position: absolute;
  top: 0px;
  left: 20px;
  width: 255px;
  height: 150px;
  border-radius: 200px;
  overflow: hidden;
  -webkit-transition: all $speed ease;
  transition: all $speed ease;
  transform: scale(0.8, 1);
  cursor: pointer;
}
.sheetHolder .sheet {
  top: -175px;
}
</style>


