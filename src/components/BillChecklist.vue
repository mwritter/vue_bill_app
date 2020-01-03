<template>
  <main>
      <div class="container">
          <div id="heading">
            <h1 class="text">Bill Checklist</h1>
          </div>
          <ul id="bill-list">
              <li class="bill-list-item" v-for="(bill) in bills" :key="bill.name">
                    <div>
                        <input type="checkbox" />
                        <label class="text" for="price">{{bill.name}}</label>
                    </div>
                    <span id="price" class="text" name="price">${{bill.value}}</span>
              </li>
          </ul>
      </div>
  </main>
</template>

<script>
export default {
    name: 'BillChecklist',
    props:{
        bills: {
            type: Array
        }
    }
}
</script>

<style>
main{
    display: flex;
    justify-content: center;
}
.container{
    display: grid;
}
#heading{
    transform: rotate(-6deg);
    background-color: #E7DAB6;
    width: 30%;
    justify-self: center;
    /* background-image: url('../assets/logo.png') no-repeat; */
    /* background-size: 100%; */
    /* clip-path: polygon(100% 23%, 91% 31%, 100% 38%, 89% 59%, 100% 73%, 92% 86%, 100% 100%, 0 100%, 0 0, 100% 0); */
}
#heading h1 {
    margin: 0px;
}
#bill-list{
    width: 500px;
}
.bill-list-item{
    display: flex;
    justify-content: space-between;
}

</style>