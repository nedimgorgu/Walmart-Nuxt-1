<template>
  <div>

    <header>
      <v-toolbar style="height: 120px;" class="pt-4 fixed-top" color="bg-primary" dark  fixed>
        <v-toolbar-title>


          <img
            src="https://i5.walmartimages.com/dfw/63fd9f59-b3e1/7a569e53-f29a-4c3d-bfaf-6f7a158bfadd/v1/walmartLogo.svg">

        </v-toolbar-title>

        <v-divider class="mx-4" vertical></v-divider>

        <span class="subheading me-4 ">





          <div class="btn-group" role="group">
            <button id="btnGroupDrop1" type="button" class="btn btn-primary dropdown-toggle" data-bs-toggle="dropdown"
              aria-expanded="false">
              <img width="20" src="@/static/photos/department1.png">

              Department
            </button>
            <ul class="dropdown-menu" aria-labelledby="btnGroupDrop1">
              <li><a class="dropdown-item" href="#">Dropdown link</a></li>
              <li><a class="dropdown-item" href="#">Dropdown link</a></li>
            </ul>
          </div>


        </span>
        <span class="subheading fw-bold">

          <button class="btn btn-sm btn-primary fw-bold">

            <img width="20" src="@/static/photos/services1.png">

            Services
          </button>



        </span>



        <div class="input-group w-50 ms-5">
          <input id="searchInput" type="search" class="form-control rounded-pill"
            placeholder="Search everything at Walmart online and in store" aria-label="Recipient's username"
            aria-describedby="basic-addon2">

        </div>

        <v-spacer></v-spacer>

        <v-toolbar-items class="hidden-sm-and-down">


          <router-link :to="{ path: '/favorite' }">
            <button v-if="checkLoginSituation" class="btn btn-sm btn-primary">

              <div class="row">

                <div class="col-2 mt-2">
                  <v-icon class="text-light">mdi-heart</v-icon>
                </div>



                <div class="col-9 text-start ms-2"> <small>Reorder <br /><span class="fw-bold fs-6">My
                      items</span></small></div>

              </div>

            </button>
          </router-link>

          <v-divider vertical></v-divider>

          <button v-if="!checkLoginSituation" class="btn btn-sm btn-primary">
            <router-link class="text-light text-decoration-none" :to="{ path: '/login' }">

              <div class="row">

                <div class="col-2 mt-2">
                  <img width="20" src="@/static/photos/account.png">
                </div>



                <div class="col-9 text-start ms-2"> <small>Sign In <br />
                    <span class="fw-bold fs-6">Account</span></small></div>

              </div>
            </router-link>

          </button>

          <v-divider vertical></v-divider>
          <routerLink :to="{ path: '/basket' }">
            <button v-if="checkLoginSituation" class="btn btn-sm btn-primary">

              <div class="row">

                <div class="col mt-2">
                  <img width="20" src="@/static/photos/basket.png">
                  <p>$ {{this.getTotalPrice.toFixed(2)}} </p>
                </div>





              </div>

            </button>

          </routerLink>
          <button v-if="checkLoginSituation == true" class="btn btn-sm btn-primary " @click="logout">

            <div class=" my-auto">

              <button type="button" class="btn btn-danger">Logout</button>





            </div>

          </button>


        </v-toolbar-items>








      </v-toolbar>

    </header>


  </div>
</template>

<script>

import { mapGetters } from "vuex"

export default {



  computed: {

    ...mapGetters(['checkLoginSituation','getTotalPrice'])

  },
  methods: {
    logout() {
      this.$store.commit('setUser', null)
      this.$store.commit('setLogin', false)
    }
  },






}
</script>
