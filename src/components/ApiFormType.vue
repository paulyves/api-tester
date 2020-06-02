<template>
	<div class="api-form-type">
		<div class="container">
			<div class="row">
				<div class="col-12">
					<div class="form-group">
			            <label for="url">URL</label>
		    			<textarea class="form-control" style="min-height:150px" id="url" readonly="true" v-model="url"></textarea>
	                 </div>
				</div>
			</div>
		</div>
		<div class="form-block type acc-status container" v-if="apiType == 'acc-status-get' || apiType == 'acc-status-set'">
			<h6 v-if="showParameters">Parameters</h6>
			<div class="row" v-if="showParameters">
				<div class="col-3">
					<div class="form-group">
		                <label for="url">Country Code</label>
	    				<input type="text" class="form-control" v-model="statParams.country_code">
                  	</div>
                </div>
                <div class="col-3">
					<div class="form-group">
		                <label for="url">Area Code</label>
	    				<input type="text" class="form-control" v-model="statParams.area_code">
                  	</div>
                </div>
                <div class="col-3">
					<div class="form-group">
		                <label for="api-type">Include Group</label>
                        <select class="form-control" id="api-type" v-model="statParams.include_group">
                          <option value="true">True</option>
                          <option value="false">False</option>
                        </select>
                  	</div>
				</div>
				<div class="col-3">
					<div class="form-group">
		                <label for="api-type">Source</label>
                        <select class="form-control" id="api-type" v-model="statParams.source">
                          <option value="sip">SIP</option>
                          <option value="prov">Prov</option>
                          <option value="both">Both</option>
                        </select>
                  	</div>
				</div>
				<div class="col-6">
					<div class="form-group">
		                <label for="url">Username</label>
	    				<input type="text" class="form-control" v-model="statParams.username">
                  	</div>
				</div>
				<div class="col-6" v-if="apiType == 'acc-status-set'">
					<div class="form-group">
		                <label for="ext-status">Status</label>
                        <select class="form-control" id="ext-status" v-model="statParams.status">
                          <option value="active">Active</option>
                          <option value="deactivated">Deactivated</option>
                          <option value="suspended">Suspended</option>
                          <option value="pending">Pending</option>
                        </select>
                  	</div>
				</div>
			</div>
			<div class="row">
				<div class="col"><button type="button" class="btn btn-primary mb-2 float-right" @click="submit">Submit</button></div>
			</div>
		</div>
		<div class="form-block type acc-lock container" v-if="apiType == 'acc-lock-get' || apiType == 'acc-lock-set'">
			<h6 v-if="showParameters">Parameters</h6>
			<div class="row" v-if="showParameters">
				<div class="col-3">
					<div class="form-group">
		                <label for="url">Country Code</label>
	    				<input type="text" class="form-control" v-model="lockParams.country_code">
                  	</div>
                </div>
                <div class="col-3">
					<div class="form-group">
		                <label for="url">Area Code</label>
	    				<input type="text" class="form-control" v-model="lockParams.area_code">
                  	</div>
                </div>
                <div class="col-3">
					<div class="form-group">
		                <label for="api-type">Include Group</label>
                        <select class="form-control" id="api-type" v-model="lockParams.include_group">
                          <option value="true">True</option>
                          <option value="false">False</option>
                        </select>
                  	</div>
				</div>
				<div class="col-3" v-if="apiType == 'acc-lock-set'">
					<div class="form-group">
		                <label for="ext-status">Clear Device Info</label>
                        <select class="form-control" id="ext-status" v-model="lockParams.clear_device_info">
                          <option value="true">True</option>
                          <option value="false">False</option>
                        </select>
                  	</div>
				</div>
				<div class="col-3" v-else>
					<div class="form-group">
		                <label for="url">Username</label>
	    				<input type="text" class="form-control" v-model="lockParams.username">
                  	</div>
				</div>
				<div class="col-6" v-if="apiType == 'acc-lock-set'">
					<div class="form-group">
		                <label for="url">Username</label>
	    				<input type="text" class="form-control" v-model="lockParams.username">
                  	</div>
				</div>
				<div class="col-6" v-if="apiType == 'acc-lock-set'">
					<div class="form-group">
		                <label for="ext-status">Status</label>
                        <select class="form-control" id="ext-status" v-model="lockParams.status">
                          <option value="locked">Locked</option>
                          <option value="unlocked">Unlocked</option>
                        </select>
                  	</div>
				</div>
				
			</div>
			<div class="row">
				<div class="col"><button type="button" class="btn btn-primary mb-2 float-right" @click="submit">Submit</button></div>
			</div>
		</div>
		<div class="form-block type acc-status container" v-if="apiType == 'replace-wh1'">
			<h6 v-if="showParameters">Parameters</h6>
			<div class="row" v-if="showParameters">
				<div class="col-3">
					<div class="form-group">
		                <label for="url">Username</label>
	    				<input type="text" class="form-control" v-model="repWh1Params.username">
                  	</div>
                </div>
                <div class="col-3">
					<div class="form-group">
		                <label for="ext-status">Force</label>
                        <select class="form-control" id="ext-status" v-model="repWh1Params.force">
                          <option value="true">True</option>
                          <option value="false">False</option>
                        </select>
                  	</div>
                </div>
                
				<div class="col-6">
					<div class="form-group">
		                <label for="url">Install ID</label>
	    				<input type="text" class="form-control" v-model="repWh1Params.install_id">
                  	</div>
				</div>
			</div>
			<div class="row">
				<div class="col"><button type="button" class="btn btn-primary mb-2 float-right" @click="submit">Submit</button></div>
			</div>
		</div>
	</div>
</template>

<script>


export default {
  name: 'ApiFormType',
  props: ['apiType'],
  data(){
  	return{
  		url : process.env.VUE_APP_API_URL,
  		showParameters : true,
  		statParams : {
  			source : "both",
  			username : "",
  			area_code : "2",
  			country_code : "63",
  			include_group : true,
  			status : ""
  		},
  		lockParams : {
  			clear_device_info : false,
  			username : "",
  			area_code : "2",
  			country_code : "63",
  			include_group : true,
  			status : ""
  		},
  		repWh1Params : {
  			username : "",
  			install_id : "",
  			force : false
  		}
  	}
  },
  watch: {
  	apiType: {
  		handler: 'updateUrlParam',
  		immediate: true
  	},
  	statParams: {
  		handler: "updateUrlParam",
  		immediate: true,
  		deep: true
  	},
  	lockParams: {
  		handler: "updateUrlParam",
  		immediate: true,
  		deep: true
  	},
  	repWh1Params: {
  		handler: "updateUrlParam",
  		immediate: true,
  		deep: true
  	},

  },
  methods : {
  	submit(){
  		this.$emit("submit",{url:this.url});
  	},
  	updateUrlParam(){
  		let arrayParams = [];
  		let params = {};
  		if(this.apiType == 'acc-status-get' || this.apiType == 'acc-status-set'){
  			params = this.statParams;
  		}else if(this.apiType == 'acc-lock-get' || this.apiType == 'acc-lock-set'){
  			params = this.lockParams;
  		}else if(this.apiType == 'replace-wh1'){
  			params = this.repWh1Params;
  		}
  		for(let i in params){
  			if(params[i].length != 0)
  				arrayParams.push(`${i}=${encodeURIComponent(params[i])}`);
  		}
  		this.url = this.getUrlByType(this.apiType) +  '?' + arrayParams.join("&");
  	},
  	getUrlByType(data){
  		let url = "";
  		switch(data){
  			case "acc-status-get" :
  				url = process.env.VUE_APP_API_URL + "get_extension_status";
  				this.statParams.status = "";
  				break;
  			case "acc-status-set" :
  				url = process.env.VUE_APP_API_URL + "set_extension_status";
  				this.statParams.status = this.statParams.status || "active";
  				break;
  			case "acc-lock-set" :
  				url = process.env.VUE_APP_API_URL + "set_extension_lock_status";
  				this.lockParams.status = this.lockParams.status || "locked";
  				this.lockParams.clear_device_info = this.lockParams.clear_device_info || false;
  				break;
  			case "acc-lock-get" :
  				url = process.env.VUE_APP_API_URL + "get_extension_lock_status";
  				this.lockParams.status = "";
  				this.lockParams.clear_device_info = "";
  				break;
  			case "replace-wh1" :
  				url = process.env.VUE_APP_API_URL + "set_install_id";
  				break;
  			default: 
  				url = process.env.VUE_APP_API_URL;
  		}
  		this.url = url;
  		return url;
  	}
  }
}
</script>

<style>

</style>