<template>
  <div>
    <CRow>
      <CCard>
        <CCardBody>
          <CRow class="card-option-table">
            <CCol md="6" style="display: -webkit-inline-box">
              <CFormInput
                placeholder="Insira o CEP"
                autocomplete="cep"
                v-model="cep"
                class="input-cep"
              />
              <CButton
                size=""
                class="button-add btn-primary"
                @click="adicionarCEP"
              >
                <CIcon icon="cil-plus" class="me-2" />
                Adicionar endereço
              </CButton>
            </CCol>
          </CRow>
          <div v-for="(item, index) in items" :key="index" class="list-cep">
            <p><strong>CEP</strong> {{ item }}</p>
          </div>
          <div class="col-3 offset-6" style="margin-top: 20px">
            <CButton size="" class="button-gerar btn-primary" @click="gerarCEP">
              Gerar endereços
            </CButton>
          </div>
          <CCard
            v-for="(item, index) in itemsCompletos"
            :key="index"
            style="margin-top: 10px; border-radius: 20px"
          >
            <CCardBody>
              <CRow class="card-option-table">
                <CCol md="6">
                  <p>
                    <strong>{{ item.logradouro }}, {{ item.bairro }}</strong>
                  </p>
                  <p style="margin-top: -10px">
                    {{ item.localidade }} - {{ item.uf }}
                  </p>
                </CCol>
                <CCol md="2 offset-4">
                  <p style="margin-top: 10px; color: #d570f5">
                    <strong>{{ item.cep }}</strong>
                  </p>
                  <CButton
                    size="sm"
                    class="btn-danger"
                    @click="removerCEP(item, index)"
                  >
                    Remover
                  </CButton>
                </CCol>
              </CRow>
            </CCardBody>
          </CCard>
        </CCardBody>
      </CCard>
    </CRow>
  </div>
</template>

<script>
import avatar1 from '@/assets/images/avatars/1.jpg'
import avatar2 from '@/assets/images/avatars/2.jpg'
import avatar3 from '@/assets/images/avatars/3.jpg'
import avatar4 from '@/assets/images/avatars/4.jpg'
import avatar5 from '@/assets/images/avatars/5.jpg'
import avatar6 from '@/assets/images/avatars/6.jpg'
import axios from 'axios'

export default {
  data() {
    return {
      cep: null,
      items: [],
      itemsCompletos: [],
      fields: [{ key: 'cep', label: 'CEP' }],
    }
  },
  name: 'Dashboard',
  components: {},
  methods: {
    async adicionarCEP() {
      if (this.cep == null) alert('CEP vazio')
      else {
        this.cep.replace('-', '')
        this.items.push(this.cep)
      }
      this.cep = null
    },
    async removerCEP(item) {
      if (this.itemsCompletos.length == 1) this.itemsCompletos = []
      else {
        this.itemCompletos.splice(item)
      }
    },
    async gerarCEP() {
      this.itemsCompletos = []
      for (let i = 0; i < this.items.length; i++) {
        axios
          .get(`https://viacep.com.br/ws/${this.items[i]}/json/`)
          .then((res) => {
            this.itemsCompletos.push(res.data)
          })
          .catch((error) => {
            if (error) alert(`CEP ${this.items[i]} inválido`)
          })
      }
      this.items = []
    },
  },
  setup() {
    const progressGroupExample1 = [
      { title: 'Monday', value1: 34, value2: 78 },
      { title: 'Tuesday', value1: 56, value2: 94 },
      { title: 'Wednesday', value1: 12, value2: 67 },
      { title: 'Thursday', value1: 43, value2: 91 },
      { title: 'Friday', value1: 22, value2: 73 },
      { title: 'Saturday', value1: 53, value2: 82 },
      { title: 'Sunday', value1: 9, value2: 69 },
    ]
    const progressGroupExample2 = [
      { title: 'Male', icon: 'cil-user', value: 53 },
      { title: 'Female', icon: 'cil-user-female', value: 43 },
    ]
    const progressGroupExample3 = [
      {
        title: 'Organic Search',
        icon: 'cib-google',
        percent: 56,
        value: '191,235',
      },
      { title: 'Facebook', icon: 'cib-facebook', percent: 15, value: '51,223' },
      { title: 'Twitter', icon: 'cib-twitter', percent: 11, value: '37,564' },
      { title: 'LinkedIn', icon: 'cib-linkedin', percent: 8, value: '27,319' },
    ]
    const tableExample = [
      {
        avatar: { src: avatar1, status: 'success' },
        user: {
          name: 'Yiorgos Avraamu',
          new: true,
          registered: 'Jan 1, 2021',
        },
        country: { name: 'USA', flag: 'cif-us' },
        usage: {
          value: 50,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'success',
        },
        payment: { name: 'Mastercard', icon: 'cib-cc-mastercard' },
        activity: '10 sec ago',
      },
      {
        avatar: { src: avatar2, status: 'danger' },
        user: {
          name: 'Avram Tarasios',
          new: false,
          registered: 'Jan 1, 2021',
        },
        country: { name: 'Brazil', flag: 'cif-br' },
        usage: {
          value: 22,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'info',
        },
        payment: { name: 'Visa', icon: 'cib-cc-visa' },
        activity: '5 minutes ago',
      },
      {
        avatar: { src: avatar3, status: 'warning' },
        user: { name: 'Quintin Ed', new: true, registered: 'Jan 1, 2021' },
        country: { name: 'India', flag: 'cif-in' },
        usage: {
          value: 74,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'warning',
        },
        payment: { name: 'Stripe', icon: 'cib-cc-stripe' },
        activity: '1 hour ago',
      },
      {
        avatar: { src: avatar4, status: 'secondary' },
        user: { name: 'Enéas Kwadwo', new: true, registered: 'Jan 1, 2021' },
        country: { name: 'France', flag: 'cif-fr' },
        usage: {
          value: 98,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'danger',
        },
        payment: { name: 'PayPal', icon: 'cib-cc-paypal' },
        activity: 'Last month',
      },
      {
        avatar: { src: avatar5, status: 'success' },
        user: {
          name: 'Agapetus Tadeáš',
          new: true,
          registered: 'Jan 1, 2021',
        },
        country: { name: 'Spain', flag: 'cif-es' },
        usage: {
          value: 22,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'primary',
        },
        payment: { name: 'Google Wallet', icon: 'cib-cc-apple-pay' },
        activity: 'Last week',
      },
      {
        avatar: { src: avatar6, status: 'danger' },
        user: {
          name: 'Friderik Dávid',
          new: true,
          registered: 'Jan 1, 2021',
        },
        country: { name: 'Poland', flag: 'cif-pl' },
        usage: {
          value: 43,
          period: 'Jun 11, 2021 - Jul 10, 2021',
          color: 'success',
        },
        payment: { name: 'Amex', icon: 'cib-cc-amex' },
        activity: 'Last week',
      },
    ]

    return {
      tableExample,
      progressGroupExample1,
      progressGroupExample2,
      progressGroupExample3,
    }
  },
}
</script>

<style scoped>
.button-add {
  background-color: #b600ee;
  border-radius: 10px;
  width: 50%;
}
.input-cep {
  margin-left: 20px;
  margin-right: 20px;
  border-radius: 10px;
}
.list-cep {
  margin-top: 20px;
}
.button-gerar {
  background-color: #b600ee;
  border-radius: 10px;
  margin-left: 25px;
  margin-bottom: 25px;
  width: 100%;
}
</style>
