<template>
  <div class="app">
    <header>
      <h1>Translate what you want</h1>
    </header>
    <main>
      <form @submit.prevent="requestTranslate">
        <div class="row">
          <div class="col-6">
            <select name="" id="" v-model="sceltaUtenteIN">
              <option value="bg">Bulgaro</option>
              <option value="cs">Ceco</option>
              <option value="zh">Cinese</option>
              <option value="da">Danese</option>
              <option value="et">Estone</option>
              <option value="fi">Finlandese</option>
              <option value="fr">Francese</option>
              <option value="ja">Giapponese</option>
              <option value="el">Greco</option>
              <option value="en">Inglese</option>
              <option value="it">Italiano</option>
              <option value="lv">Lettone</option>
              <option value="lt">Lituano</option>
              <option value="nl">Olandese</option>
              <option value="pl">Polacco</option>
              <option value="pt">Portoghese</option>
              <option value="ro">Rumeno</option>
              <option value="ru">Russo</option>
              <option value="sk">Slovacco</option>
              <option value="sl">Sloveno</option>
              <option value="es">Spagnolo</option>
              <option value="sv">Svedese</option>
              <option value="de">Tedesco</option>
              <option value="hu">Ungherese</option>
            </select>
            <textarea name="testoUtente" id="testoUtente" v-model="testoUtente">
            </textarea>
          </div>
          <div class="col-6">
            <select name="" id="" v-model="sceltaUtenteOUT">
              <option value="bg">Bulgaro</option>
              <option value="cs">Ceco</option>
              <option value="zh">Cinese</option>
              <option value="da">Danese</option>
              <option value="et">Estone</option>
              <option value="fi">Finlandese</option>
              <option value="fr">Francese</option>
              <option value="ja">Giapponese</option>
              <option value="el">Greco</option>
              <option value="en">Inglese</option>
              <option value="it">Italiano</option>
              <option value="lv">Lettone</option>
              <option value="lt">Lituano</option>
              <option value="nl">Olandese</option>
              <option value="pl">Polacco</option>
              <option value="pt">Portoghese</option>
              <option value="ro">Rumeno</option>
              <option value="ru">Russo</option>
              <option value="sk">Slovacco</option>
              <option value="sl">Sloveno</option>
              <option value="es">Spagnolo</option>
              <option value="sv">Svedese</option>
              <option value="de">Tedesco</option>
              <option value="hu">Ungherese</option>
            </select>
            <textarea name="testoUtente" id="testoUtente" v-model="traduzione">
            </textarea>
          </div>
        </div>
        <input type="submit" value="Translate!" />
      </form>
    </main>
  </div>
</template>

<script>
import { ref } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
import "jquery/src/jquery.js";
import "bootstrap/dist/js/bootstrap.min.js";

export default {
  name: "App",
  setup() {
    const testoUtente = ref("");
    const sceltaUtenteIN = ref("");
    const sceltaUtenteOUT = ref("");
    const traduzione = ref("");

    const requestTranslate = async () => {
      const res = await fetch("http://localhost:4000/screenshot", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          testoUtente: testoUtente.value,
          sceltaUtenteIN: sceltaUtenteIN.value,
          sceltaUtenteOUT: sceltaUtenteOUT.value,
        }),
      }).then((data) => data.json());
      traduzione.value = res.grabTraduzinoe;
    };

    return {
      testoUtente,
      sceltaUtenteIN,
      sceltaUtenteOUT,
      traduzione,
      requestTranslate,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
