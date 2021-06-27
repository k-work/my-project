<template>
  <div id="app">
    <NavBar avatar="AYUDA" login="SIGN IN" text="ES" />
    <div>
      <div class="stepStyle">
        <el-steps :active="active" :align-center="true" finish-status="success">
          <el-step title="MIS DATOS"></el-step>
          <el-step title="PAGO"></el-step>
        </el-steps>
      </div>
      <div class="formStyle">
        <div class="formSection" v-if="active === 0">
          <h1 class="title">Mis Datos</h1>
          <p class="description">Revisa las datos y completa oquellas pendientes antes de continuar con el proceso.</p>
          <div style="text-align: left;height: 330px;">
            <el-form label-position="top" label-width="80px" :model="formLabel">
              <el-form-item label="Nombre">
                <el-input v-model="formLabel.nombre"></el-input>
              </el-form-item>
              <el-form-item label="Apellidos">
                <el-input v-model="formLabel.apellidos"></el-input>
              </el-form-item>
            </el-form>
          </div>
          <div style="margin-top: 20px;display: flex;justify-content: flex-end;">
            <el-button type="primary" round @click="next(1)">Continuar <i class="el-icon-right"></i></el-button>
          </div>
        </div>
        <div class="formSection" v-if="active === 1">
          <h1 class="title">Pago del producto</h1>
          <p class="description">Una vez efectuado el pago del producto, recibios un email con los detalles de la compro.</p>
          <div class="rect">
            <i class="el-icon-bank-card" style="margin-top: 20px;font-size: 80px; color:#F56C6C;"></i>
            <h2>Tarjeta de crédito</h2>
            <p>Se redirigira a uno plaraforma de pago. Se trata de un proceso seguro. Puede que la validacion del pago tarde 24 horas en completarse.</p>
            <img src="@/assets/visa-master-icon-19.png" style="width: 100px;padding-bottom: 30px;">
          </div>
          <div style="margin-top: 20px;display: flex;justify-content: space-between;">
            <el-button round @click="next(0)"><i class="el-icon-back"></i> Anterior</el-button>
            <el-button type="primary" round @click="next(3)">Pagar&emsp;&emsp;<i class="el-icon-right"></i></el-button>
          </div>
        </div>
        <div class="formSection" v-if="active === 3">
            <img src="@/assets/diploma.svg" style="margin-top: 200px;width: 100px;" />
            <h2>{{ resTitle }}</h2>
            <p>{{ resDescription }}</p>
        </div>
      </div>
    </div>
    <div style="height: 50px;"></div>
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #F5F5F5;
}
.stepStyle {
  margin: 50px 0px;
  width: 50%;
  display: inline-block;
  justify-content: center;
}
.formStyle {
  background:#fff;
  width: 80%;
  height: 680px;
  margin: 0 auto;
  box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.08);
  .formSection {
    width: 50%;
    height: 400px;
    display: inline-block;
    text-align: center;
    margin-bottom: 10px;
  }
  .title {
    padding-top: 30px;
  }
  .description {
    margin-bottom: 60px;
  }
}
.rect {
  border: 1px solid #F5F5F5;
  // height: 280px;
  padding: 0 50px;
}
</style>

<script>
import axios from 'axios';
import NavBar from './components/NavBar.vue'

export default {
  name: 'app',
  components: {
    NavBar,
  },
  data() {
      return {
        active: 0,
        formLabel: {
          nombre: '',
          apellidos: ''
        },
        resTitle: '',
        resDescription: '',
      };
    },
  methods: {
    next(val) {
      if (val === 0) {
        this.active = 0;
      }
      if (val === 1) {
        this.active = 1;
      }
      if (val === 2) {
        this.active = 2;
      }
      if (val === 3) {
        this.active = 3;
        const apiUrl = 'http://www.mocky.io/v2/5e3d41272d00003f7ed95c09';
        axios
          .get(apiUrl)
          .then(response => {
            this.resTitle = response.data.title;
            this.resDescription = response.data.text;
          })
      }
    }
  }
}
</script>
