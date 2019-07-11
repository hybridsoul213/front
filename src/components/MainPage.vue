<template>
  <div class="jumbotron jumbotron-fluid">
    <div class="container">
      <h1 class="display-4">Summer Practice</h1>
      <div class="btn-group btn-group-toggle d-flex flex-column flex-md-row" data-toggle="buttons">
        <label class="btn btn-secondary">
          <input type="radio" name="options" id="client" autocomplete="off" checked @click="clientTab">
          Client
        </label>
        <label class="btn btn-secondary">
          <input type="radio" name="options" id="task" autocomplete="off" checked @click="taskTab"> Task
        </label>
        <label class="btn btn-secondary  mr-3">
          <input type="radio" name="options" id="worker" autocomplete="off" checked @click="workerTab">
          Worker
        </label>
      </div>
      <div class="col-md-4">
        <div class="form-group pt-4">
          <label for="search">Search by Id</label>
          <input
                  type="text"
                  class="form-control"
                  id="search"
                  placeholder="Enter Id"
                  v-model="id"
          >

        </div>
      </div>
      <div class="col-md-8">
        <b-button v-if="tableId === 0" key="addCL" class="btn" v-b-modal.addCL @click="reset">Add new record
          <b-modal
                  id="addCL"
                  ref="modal"
                  title="Enter New Client"
                  @ok="handlePost"
          >
            <form ref="form" @submit.stop.prevent="handlePost">
              <b-form-group
                      label="Enter Id"
              >
                <b-form-input
                        v-model="client.Id"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Client Name"
              >
                <b-form-input
                        v-model="client.ClientName"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter registration number"
              >
                <b-form-input
                        v-model="client.RegistrationNumber"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter FML Manager"
              >
                <b-form-input
                        v-model="client.FML_Manager"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Adress"
              >
                <b-form-input
                        v-model="client.Adress"
                ></b-form-input>
              </b-form-group>
            </form>
          </b-modal>
        </b-button>
        <b-button v-else-if="tableId === 1" key="addTS" class="btn" v-b-modal.addTS @click="reset">Add new record
          <b-modal
                  id="addTS"
                  ref="modal"
                  title="Enter New Task"
                  @show="resetModal(clientNameState)"
                  @hidden="resetModal(clientNameState)"
                  @ok="handlePost"
          >
            <form ref="form" @submit.stop.prevent="handlePost">
              <b-form-group
                      label="Enter Id"
              >
                <b-form-input
                        v-model="client.Id"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Client Name"
              >
                <b-form-input
                        v-model="client.ClientName"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter registration number"
              >
                <b-form-input
                        v-model="client.RegistrationNumber"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter FML Manager"
              >
                <b-form-input
                        v-model="client.FML_Manager"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Adress"
              >
                <b-form-input
                        v-model="client.Adress"
                ></b-form-input>
              </b-form-group>
            </form>
          </b-modal>
        </b-button>
        <b-button v-else="tableId === 2" key="addWK" class="btn" v-b-modal.addWK @click="reset">Add new record
          <b-modal
                  id="addWK"
                  ref="modal"
                  title="Enter New Worker"
                  @show="resetModal(clientNameState)"
                  @hidden="resetModal(clientNameState)"
                  @ok="handlePost"
          >
            <form ref="form" @submit.stop.prevent="handlePost">
              <b-form-group
                      label="Enter Id"
              >
                <b-form-input
                        v-model="client.Id"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Client Name"
              >
                <b-form-input
                        v-model="client.ClientName"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter registration number"
              >
                <b-form-input
                        v-model="client.RegistrationNumber"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter FML Manager"
              >
                <b-form-input
                        v-model="client.FML_Manager"
                ></b-form-input>
              </b-form-group>
              <b-form-group
                      label="Enter Adress"
              >
                <b-form-input
                        v-model="client.Adress"
                ></b-form-input>
              </b-form-group>
            </form>
          </b-modal>
        </b-button>

      </div>
    </div>
    <div class="col pt-4" align="center">
      <template v-if="tableId === 0">
        <table class="table table-striped table-bordered">
          <thead class="thead-dark">
          <th scope="col">#</th>
          <th scope="col">Client Name</th>
          <th scope="col">Registration Number</th>
          <th scope="col">FML Manager</th>
          <th scope="col">Adress</th>
          <th scope="col"></th>
          </thead>
          <tbody>
          <tr scope="row" v-for="item in filtredEntity">
            <td>{{item.Id}}</td>
            <td>{{item.ClientName}}</td>
            <td>{{item.RegistrationNumber}}</td>
            <td>{{item.FML_Manager}}</td>
            <td>{{item.Adress}}</td>
            <td>
              <b-button class="btn-sm mr-4" @click="edit(item)" v-b-modal.editCL>Edit</b-button>
              <button type="button" class="btn btn-secondary btn-sm"
                      @click="deleteEntity(url.clients,item.Id)">Delete
              </button>

            </td>
          </tr>
          </tbody>
        </table>
        <b-modal
                id="editCL"
                ref="modal"
                title="Enter New Data"
                @show="resetModal(clientNameState)"
                @hidden="resetModal(clientNameState)"
                @ok="handleEdit"
        >
          <form ref="form" @submit.stop.prevent="handleEdit">
            <b-form-group
                    label="Enter Client Name"
            >
              <b-form-input
                      v-model="client.ClientName"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                    label="Enter registration number"
            >
              <b-form-input
                      v-model="client.RegistrationNumber"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                    label="Enter FML Manager"
            >
              <b-form-input
                      v-model="client.FML_Manager"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                    label="Enter Adress"
            >
              <b-form-input
                      v-model="client.Adress"
              ></b-form-input>
            </b-form-group>
          </form>
        </b-modal>
      </template>
      <template v-else-if="tableId === 1">
        <table class="table table-striped table-bordered">
          <thead class="thead-dark">
          <th scope="col">#</th>
          <th scope="col">Project Name</th>
          <th scope="col">Client Id</th>
          <th scope="col">Priority</th>
          <th scope="col">Start Date</th>
          <th scope="col">End Date</th>
          <th scope="col">Done</th>
          </thead>
          <tbody>
          <tr scope="row" v-for="item in filtredEntity">
            <td>
              {{item.Id}}
            </td>
            <td>{{item.ProjectName}}</td>
            <td>{{item.ClientRefId}}</td>
            <td>
              {{item.Priority}}
            </td>
            <td>{{item.StartDate}}</td>
            <td>{{item.EndDate}}</td>
            <td>{{item.Done}}</td>
          </tr>
          </tbody>
        </table>
      </template>
      <template v-else-if="tableId === 2">
        <table class="table table-striped table-bordered">
          <thead class="thead-dark">
          <th scope="col">#</th>
          <th scope="col">Passport</th>
          <th scope="col">Project Id</th>
          <th scope="col">FML Name</th>
          <th scope="col">Function</th>
          <th scope="col">Company</th>
          </thead>
          <tbody>
          <tr scope="row" v-for="item in filtredEntity">
            <td>
              {{item.Id}}
            </td>
            <td>{{item.Passport}}</td>
            <td>{{item.ProjectRefId}}</td>
            <td>
              {{item.FML_Name}}
            </td>
            <td>{{item.Function}}</td>
            <td>{{item.Company}}</td>
          </tr>
          </tbody>
        </table>
      </template>
    </div>
  </div>
</template>

<script>
  const cl = (Id, ClientName, RegistrationNumber, FML_Manager, Adress) => ({
    Id,
    ClientName,
    RegistrationNumber,
    FML_Manager,
    Adress
  });
  const ts = (Id, ProjectName, ClientRefId, Priority, StartDate, EndDate, Done) => ({
    Id,
    ProjectName,
    ClientRefId,
    Priority,
    StartDate,
    EndDate,
    Done
  });
  const wk = (Id, Passport, ProjectRefId, FML_name, Function, Company) => ({
    Id,
    Passport,
    ProjectRefId,
    FML_name,
    Function,
    Company
  });
  export default {
    name: 'TaskTracking',
    props: {
      msg: String
    },
    data: () => {
      return {
        id: '',
        clientNameState: null,
        client: cl(),
        task: ts(),
        worker: wk(),
        tableId: Number,
        entity: [],
        url: {
          clients: 'https://localhost:44353/api/client',
          tasks: 'https://localhost:44353/api/task',
          workers: 'https://localhost:44353/api/worker'
        }
      }
    },
    created: function () {
      this.clientTab();
    },
    computed: {
      filtredEntity() {
        if (this.id) {
          const self = this;
          const filter = this.entity.filter(function (entity) {
            return entity.Id.toString().indexOf(self.id) > -1
          });
          return filter;
        } else return this.entity;
      }
    },
    methods: {
      reset() {
        switch (this.tableId) {
          case 0 : {
            this.client = cl;
            break;
          }
          case 1 : {
            this.task = ts;
            break;
          }
          case 2: {
            this.worker = wk;
            break;
          }
        }
        if (this.tableId === 1)
          this.task = ts;
        else
          this.worker = cl;
      },
      edit(entity) {
        switch (this.tableId) {
          case 0: {
            this.client = entity;
            break;
          }
          case 1: {
            this.task = entity;
            break;
          }
          case 2: {
            this.worker = entity;
            break;
          }
        }
      },
      handleEdit(bvModalEvt) {
        bvModalEvt.preventDefault();
        switch (this.tableId) {
          case 0: {
            this.put(this.url.clients + '/' + this.client.Id, this.client);
            break;
          }
          case 1: {
            this.put(this.url.tasks + '/' + this.task.Id, this.task);
            break;
          }
          case 2: {
            this.put(this.url.workers + '/' + this.worker.Id, this.worker);
            break;
          }
        }
      }
      ,
      handlePost(bvModalEvt) {
        bvModalEvt.preventDefault();
        switch (this.tableId) {
          case 0: {
            this.post(this.url.clients, this.client);
            break;
          }
          case 1: {
            this.post(this.url.clients, this.client);
            break;
          }
          case 2: {
            this.post(this.url.clients, this.client);
            break;
          }
        }
      }
      ,
      resetModal(state) {
        state = null;
      }
      ,
      clientTab() {
        if (this.tableId !== 0) {
          this.tableId = 0;
          this.getEntities(this.url.clients);
        }
      }
      ,
      taskTab() {
        if (this.tableId !== 1) {
          this.tableId = 1;
          this.getEntities(this.url.tasks);
        }
      }
      ,
      workerTab() {
        if (this.tableId !== 2) {
          this.tableId = 2;
          this.getEntities(this.url.workers);
        }
      }
      ,
      getEntities(url) {
        axios.get(url).then((response) => {
          console.log(response.data);
          this.entity = response.data;
        })
      }
      ,
      deleteEntity(url, id) {
        axios.delete(url + '/' + id).then((response) => {
          this.entity = response.data;
        })
      }
      ,
      getEntity(url, id) {
        axios.get(url + '/' + id).then((response) => {
          this.entity = response.data;
        })
      }
      ,
      put(url, obj) {
        axios.put(url, obj)
                .then(function (response) {
                  console.log(response);
                }).catch(function (error) {
          console.log(error);
        });
      },
      post(url, obj) {
        axios.post(url, obj)
                .then(function (response) {
                  console.log(response);
                }).catch(function (error) {
          console.log(error);
        });
      }
    }
  }
</script>
