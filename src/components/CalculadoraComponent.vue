<template>
  <div class="box">
  <div class="calculadora">
    <div class="display">{{valorCorrente || '0'}}</div>
    <div v-on:click="juntarNumeros('1')" class="botao">1</div>
    <div v-on:click="juntarNumeros('2')" class="botao">2</div>
    <div v-on:click="juntarNumeros('3')" class="botao">3</div>
    <div v-on:click="somar" class="botao operadores">+</div>
    <div v-on:click="juntarNumeros('4')" class="botao">4</div>
    <div v-on:click="juntarNumeros('5')" class="botao">5</div>
    <div v-on:click="juntarNumeros('6')" class="botao">6</div>
    <div v-on:click="diminuir" class="botao operadores">-</div>
    <div v-on:click="juntarNumeros('7')" class="botao">7</div>
    <div v-on:click="juntarNumeros('8')" class="botao">8</div>
    <div v-on:click="juntarNumeros('9')" class="botao">9</div>
    <div v-on:click="multiplicar" class="botao operadores">x</div>
    <div v-on:click="juntarNumeros('0')" class="botao zero">0</div>
    <div v-on:click="juntarNumeros('00')" class="botao zero">00</div>
    <div v-on:click="ponto" class="botao">.</div>
    <div v-on:click="dividir" class="botao operadores">/</div>
    <div v-on:click="limpar" class="botao limpar">C</div>
    <div v-on:click="porcentagem" class="botao porcentagem">%</div>
    <div v-on:click="resultado" class="botao operadores igual"> = </div>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valorCorrente: '',
      numeroAnterior: null,
      operador: null,
      operadorClicado: false,
    };
  },
  methods: {
    limpar() {
      this.valorCorrente = '';
    }, sinal() {
      this.valorCorrente = this.valorCorrente.charAt(0) === '-'
          ? this.valorCorrente.slice(1)
          : `-${this.valorCorrente}`;
    }, porcentagem() {
      this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
    }, juntarNumeros(numero) {
      if (this.operadorClicado) {
        this.valorCorrente = '';
        this.operadorClicado = false;
      }

      this.valorCorrente = `${this.valorCorrente}${numero}`;
    }, ponto() {
      if (this.valorCorrente.indexOf('.') === -1) {
        this.juntarNumeros('.');
      }
    }, setarValor() {
      this.numeroAnterior = this.valorCorrente;
      this.operadorClicado = true;
    }, resultado() {
      this.valorCorrente = `${this.operador(
          parseFloat(this.numeroAnterior),
          parseFloat(this.valorCorrente),
      )}`;
      this.numeroAnterior = null;
    }, dividir() {
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    }, multiplicar() {
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    }, diminuir() {
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    }, somar() {
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    }
  }
}
</script>
<style scoped>
.box {
  display: flex;
  background-color: black;
  margin: 0 auto;
  max-width: 400px;
 height: 500px;
  align-content: center;
 padding: 50px 0px 20px 0px;
}
.calculadora {
  margin: 0 auto;
  width: 350px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  grid-gap: 5px;
}
.display {
  grid-column: 1 / 5;
  background-color: #000000;
  color: white;
  border-top: solid 3px white;
  padding-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.zero {
  grid-column: 0/ 4;
  display: flex;
  justify-content: center;
  align-items: center;
}
.botao {
  background-color: #171717;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.botao:active {
  background-color: #0d0d0d;
}
.operadores:active {
  background-color: #cc0000;
}
.operadores {
  background-color: #ff1313;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.igual {
  grid-column: 3/5;
}
.limpar {
  color: white;
  background-color: #ff1313;
 }
.porcentagem {
  color: white;
  background-color: #ff1313;
}
</style>