<template>



  <section class="h-custom h-100">

    <div class="container py-5">

      <div class="col-5 m-auto"><img
          src="https://i5.walmartimages.com/dfw/63fd9f59-b3e1/7a569e53-f29a-4c3d-bfaf-6f7a158bfadd/v1/walmartLogo.svg"
          height="120px" /></div>

      <div class="row mt-4 d-flex justify-content-center align-items-center h-100">
        <div class="col-12">
          <div class="card card-registration card-registration-2" style="border-radius: 15px;">
            <div class="card-body p-0">
              <div class="row g-0">
                <div class="col-lg-7">
                  <div class="p-5">
                    <div class="d-flex justify-content-between align-items-center mb-5">
                      <h1 class="fw-bold mb-0 text-black">Shopping Cart</h1>
                      <h6 class="mb-0 text-muted">{{ basketData.length }} items</h6>
                    </div>
                    <hr class="my-4">


                    <BasketItem v-for="item in basketData" :key="item.id" :item="item" />


                    <div class="pt-5">
                      <h6 class="mb-0"><button @click="$router.go(-1)" class="text-body"><i
                            class="fas fa-long-arrow-alt-left me-2"></i> Back to shop</button>
                      </h6>
                    </div>
                  </div>
                </div>
                <div class="col-lg-5 bg-grey">
                  <div class="p-5">
                    <h3 class="fw-bold mb-5 mt-2 pt-1">Summary</h3>
                    <hr class="my-4">

                    <div class="d-flex justify-content-between mb-4">
                      <h5 class="text-uppercase">items {{ basketData.length }}</h5>
                      <h5>$ {{ this.getTotalPrice.toFixed(2)}}</h5>
                    </div>

                    <h5 class="text-uppercase mb-3">Shipping</h5>

                    <div class="mb-4 pb-2">
                      <select class="select">
                        <option value="1">Standard-Delivery- $5.00</option>
                        <option value="2">Two</option>
                        <option value="3">Three</option>
                        <option value="4">Four</option>
                      </select>
                    </div>

                    <hr class="my-4">

                    <CreditCard />

                    <hr class="my-4" />
                    <div class="d-flex justify-content-between mb-5">
                      <h5 class="text-uppercase">Total price</h5>
                      <h5>$ {{ this.getTotalPrice.toFixed(2) }}</h5>
                    </div>


                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>


</template>



<script>
import { collection, query, where, getDocs } from "firebase/firestore";
import { mapGetters } from "vuex";
import { db } from "~/firebase";
export default {

  data() {
    return {
      dbBasketData: [],
      basketData: [],
      totalPrice:0
    }
  },

  async mounted() {
    const q = query(collection(db, "users"), where("email", "==", this.getUser.email));
    const basket = await getDocs(q);
    basket?.forEach((doc) => {

      this.dbBasketData?.push(doc.data().basket)

      this.dbBasketData?.forEach((item) => {
        item?.forEach((item) => {
          this.basketData.push(item)
        })
      })
    });

    this.basketData.forEach((item) => {


      this.totalPrice = this.totalPrice + item.unitPrice

    })

    this.$store.commit('setTotalPrice', this.totalPrice)

    console.log(this.getTotalPrice);
  },


  computed: {

    ...mapGetters(['getUser', 'getTotalPrice'])

  }



}
</script>


<style>
body,
html {
  padding: 0;
  margin: 0;
  width: 100%;
  min-height: 100%;
  background-color: #0071DC
}
</style>
