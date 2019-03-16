<template>
  <mdb-container>
    <nav class="navbar navbar-dark primary-color justify-content-between">
      <a class="navbar-brand" href="#">BankApp</a>
      <form class="form-inline my-1">
        <div class="md-form form-sm my-0"></div>
        <button class="btn btn-outline-white btn-sm my-0" type="submit">Wyloguj</button>
      </form>
    </nav>

    <div class="chart-wrapper">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">Wydatki</h5>
          <mdb-pie-chart :data="pieChartData" :options="pieChartOptions" :width="600" :height="300"></mdb-pie-chart>
        </div>
      </div>
    </div>

    <div class="account-wrapper">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">Dostępne środki</h5>
          <p id="currency" class="text-right">PLN</p>
          <div class="value-wrapper">
            <p class="text-right">{{ money }}</p>
          </div>
          <mdb-btn
            color="cyan lighten-1"
            size="md"
            @click="register = true"
            class="waves-light"
          >Nowy przelew</mdb-btn>
        </div>
      </div>
    </div>

    <mdb-modal v-if="register" @close="register = false">
      <form class="needs-validation" novalidate @submit="checkForm">

      <mdb-modal-header class="text-center">
        <mdb-modal-title tag="h4" bold class="w-100">Nowy przelew</mdb-modal-title>
      </mdb-modal-header>

      <mdb-modal-body class="mx-3 grey-text">
        <mdb-input required label="Numer konta" v-model="to" icon="money-check-alt" class="mb-5"/>
        <mdb-input required label="Kwota" v-model="amount" icon="hand-holding-usd" class="mb-5"/>
      </mdb-modal-body>


      <mdb-modal-footer center>
        <mdb-btn type="submit"  v-on:click="transfer" color="default">Wyślij</mdb-btn>
      </mdb-modal-footer>
      </form>
    </mdb-modal>

    <!-- <div class="table-wrapper">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">Historia</h5>
          <mdb-datatable
            :data="data"
            striped
            bordered
            :pagination="false"
            :sorting="false"
            :searching="false"
          />
        </div>
      </div>
    </div>-->
    <div class="table-wrapper">
        <h5 class="card-title">Historia</h5>
      <mdb-tbl>
        <mdb-tbl-head>
          <tr>
            <th><b>Data</b></th>
            <th><b>Nadawca</b></th>
            <th><b>Odbiorca</b></th>
            <th><b>Kwota</b></th>
          </tr>
        </mdb-tbl-head>
        <mdb-tbl-body>
          <tr v-for="item in data.rows">
            <td v-bind:style= "[item.type == 'ADDITION' ? {'color': '#00C851'} : {'color': '#ff4444'}]">{{ item.date }}</td>
            <td v-bind:style= "[item.type == 'ADDITION' ? {'color': '#00C851'} : {'color': '#ff4444'}]">{{ item.from }}</td>
            <td v-bind:style= "[item.type == 'ADDITION' ? {'color': '#00C851'} : {'color': '#ff4444'}]">{{ item.to }}</td>
            <td v-bind:style= "[item.type == 'ADDITION' ? {'color': '#00C851'} : {'color': '#ff4444'}]"> {{ item.amount }}</td>
          </tr>
        </mdb-tbl-body>
      </mdb-tbl>
    </div>

    <!-- <div class="table-wrapper">
      <mdb-datatable :data="data" striped bordered  :pagination="false" :sorting="false"  :searching="false"/>
    </div>-->
  </mdb-container>
</template>

<script>
import {
  mdbContainer,
  mdbPieChart,
  mdbDatatable,
  mdbBtn,
  mdbModal,
  mdbModalHeader,
  mdbModalBody,
  mdbModalFooter,
  mdbInput,
  mdbTbl,
  mdbTblHead,
  mdbTblBody
} from "mdbvue";

import axios from "axios";

export const HTTPP = axios.create({
  baseURL: `http://localhost:8090/user/dashboard`,
  headers: {
    "Access-Control-Allow-Origin": "*",
    testyd: "ddd",
    Authorization: localStorage.Authorization
  }
});

export const tr = axios.create({
  baseURL: `http://localhost:8090/user/dashboard`,
  headers: {
    "Access-Control-Allow-Origin": "*",
    Authorization: localStorage.Authorization
  }
});

export default {
  name: "Dashboard",
  components: {
    mdbContainer,
    mdbPieChart,
    mdbDatatable,
    mdbBtn,
    mdbModal,
    mdbModalHeader,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbTbl,
    mdbTblHead,
    mdbTblBody
  },
  data() {
    return {
      register: false,
      money: null,
      amount: null,
      to: null,
      pieChartData: {
        labels: ["Żywność", "Gry i zabawy", "Inne"],
        datasets: [
          {
            data: [300, 50, 100],
            backgroundColor: ["#F7464A", "#46BFBD", "#FDB45C"],
            hoverBackgroundColor: ["#FF5A5E", "#5AD3D1", "#FFC870"]
          }
        ]
      },
      pieChartOptions: {
        responsive: true,
        maintainAspectRatio: false
      },
      data: {
        columns: [
          {
            label: "Data",
            field: "date",
            sort: "asc"
          },
          {
            label: "Nadawca",
            field: "from",
            sort: "asc"
          },
          {
            label: "Odbiorca",
            field: "to",
            sort: "asc"
          },
          {
            label: "Kwota",
            field: "amount",
            sort: "asc"
          }
        ],
        rows: [
          {
            nadawca: "3524",
            data: "16-01-2019",
            odbiorca: "1234",
            kwota: 1
          }
        ]
      }
    };
  },
  methods: {
    transfer: function() {
      tr.post("http://localhost:8090/user/transfer", {
        amount: this.amount,
        to: this.to
      }).then(
        response => {
          HTTPP.get("http://localhost:8090/user/dashboard").then(response => {
            this.money = response.data.account.balance;
            this.data.rows = response.data.account.history.transfers;
          });
        },
        error => {
          this.error = true;
        }
      );
    },
      checkForm(event) {
      event.preventDefault();
      event.target.classList.add('was-validated');
    }
  },
  mounted() {
    HTTPP.get("http://localhost:8090/user/dashboard").then(response => {
      this.money = response.data.account.balance;
       this.data.rows = response.data.account.history.transfers;
    });
  }
};
</script>

<style scoped>
#currency {
  font-size: 24px;
  position: relative;
  top: 10%;
  margin-left: 10px;
  float: right;
}

.value-wrapper p {
  font-size: 34px;
  float: right;
}

.container {
  width: 60%;
  background-color: white;
  height: 100vh;
}

.chart-wrapper {
  position: relative;
  top: 5%;
  width: 30%;
  float: left;
}

.account-wrapper {
  position: relative;
  top: 5%;
  width: 55%;
  left: 15%;
  float: left;
}

/* .table-wrapper {
  position: absolute;
  top: 65%;
  left: 21%;
  width: 58%;
} */

.table-wrapper {
  position: absolute;
  top: 40%;
  left: 47%;
  width: 32%;
  -webkit-box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12);
  padding: 1.25rem;
}

mdb-input:invalid {
  border-bottom: 1px solid green;
}
</style>



