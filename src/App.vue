<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <a class="navbar-brand" href="#">
        Account REST API Tester
      </a>
    </nav>
    <div class="container">
      <div class="row mt-5">
        <div class="col-2"></div>
        <div class="col">
          <div class="row">
            <div class="col">
              <div class="card">
                <div class="card-body">
                  <!-- FORM Ruquest-->
                  <div class="row">
                    <div class="col-6">
                      <div class="form-group">
                        <label for="api-type">API</label>
                        <select class="form-control" id="api-type" v-model="apiType">
                          <option value="acc-status-get">Get Extension Status</option>
                          <option value="acc-status-set">Set Extension Status</option>
                          <option value="acc-lock-get">Get Lock Status</option>
                          <option value="acc-lock-set">Set Lock Status</option>
                          <option value="replace-wh1">Replace WH1 Unit</option>
                          <option value="trnsf-wavenum">Transfer Wave Number</option>
                          <option value="set-dev-wavenum">Set Device Wave Number</option>
                        </select>
                      </div>
                    </div>
                    <div class="col-6">
                      <div class="form-group">
                        <label for="token">Token</label>
                        <input type="text" class="form-control" id="token" v-model="token">
                      </div>
                    </div>
                  </div>
                </div>
               <div class="row">
                    <div class="col">
                      <ApiFormType :apiType="apiType" @submit="submit" :isLoading="isLoading" @clearResponse="clearResponse" />
                    </div>
                  </div>
              </div>
            </div>
          </div>
          <div class="row mt-2">
            <div class="col">
              <div class="card">
                <div class="card-body">
                  <h4>Response</h4>
                  <div>Status Code {{statusCode}}</div>
                  <div class="pre-container">
                    <pre>{{jsonResponse}}</pre>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-2"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ApiFormType from "@/components/ApiFormType";
export default {
  name: 'App',
  components: {
    // HelloWorld
    ApiFormType
  },
  data(){
    return {
      apiType : "acc-status-get",
      jsonResponse: "",
      statusCode : "",
      isLoading : false,
      token : ""
    }
  },
  methods: {
    submit(data){
      this.isLoading = true;
      this.clearResponse();
      axios.defaults.headers.common["Authorization"] = this.token;
      axios.get(data.url)
      .then(response=>{
        console.log(response);
        this.statusCode = response.status;
        this.jsonResponse = JSON.stringify(response.data, null , 2);
      })
      .catch(err =>{
        this.statusCode = err.response.status;
        this.jsonResponse = JSON.stringify(err.response.data, null , 2);
      }).finally(()=>this.isLoading = false)
    },
    clearResponse(){
      this.jsonResponse = "";
      this.statusCode = "";
    }
  }
}
</script>

<style>

</style>
