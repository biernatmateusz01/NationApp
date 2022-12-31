<template>
  <div class="container">
    <!-- <div class="name-element">
      <span>Items:</span>
      <span>{{ allCites }}</span>
    </div> -->
    <div
      v-for="item in listCountry"
      :key="item"
      class="element"
      style="display: flex; gap: 8px"
    >
      <div>
        <div class="name-element">
          <span>Name:</span>
          <span>{{ item.name.common }}</span>
        </div>
        <div v-if="item.name.common != item.name.official" class="name-element">
          <span>Full name:</span>
          <span>{{ item.name.official }}</span>
        </div>

        <div class="name-element">
          <span>Flag:</span>
          <span>{{ item.flag }}</span>
        </div>

        <div v-if="item.capital" class="name-element">
          <span>Capital city:</span>
          <span>{{ [item.capital].toString() }}</span>
        </div>

        <div class="name-element">
          <span>Region:</span>
          <span>{{ item.region }}</span>
        </div>
        <div class="name-element">
          <span>Subregion:</span>
          <span>{{ item.subregion }}</span>
        </div>
        <div class="name-element">
          <span>Start of week:</span>
          <span>{{ item.startOfWeek }}</span>
        </div>

        <div class="name-element">
          <span>Timezones:</span>
          <span>{{ [item.timezones].toString() }}</span>
        </div>

        <div class="name-element">
          <span>Population:</span>
          <span>{{ item.population }}</span>
        </div>
      </div>

      <span
        @click="deleteElement(item)"
        class="material-symbols-outlined delete"
      >
        delete
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const listCountry = ref([]);
const allCites = ref(0);
const filteredElements = ref([]);

const getData = () => {
  fetch("https://restcountries.com/v3.1/all")
    .then((res) => res.json())
    .then((res) => {
      listCountry.value = res;
      allCites.value = res.length;
      filteredElements.value = res.filter((el) => el.subregion === "Caribbean");
      console.log(filteredElements, "filtrowane");
    });
};
getData();

// const sortElement = () => {
//   filteredElements.value = listCountry.value;
//   console.log(filteredElements.value)
// }

// sortElement()

const deleteElement = (item) => {
  console.log("usuń element", item);
  alert("usuń element", item);
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 14px;
  max-width: 1600px;
  padding: 24px;
}
.element {
  position: relative;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  gap: 8px;
  min-height: 250px;
  width: 270px;
  background-color: rgb(36, 33, 228);
  color: rgb(255, 251, 0);
  /* border-radius: 5px; */
  padding: 16px;
  transition: all 1s;
  overflow: hidden;
}
.element:hover {
  width: 300px;
  padding: 12px;
  border-radius: 5px;
}
.name-element {
  display: flex;
  justify-content: space-between;
  font-size: 14px;
}
.delete {
  position: absolute;
  cursor: pointer;
  font-size: 24px;
  background-color: white;
  left: -10px;
  bottom: -8px;
  padding: 12px;
  border-radius: 50%;
  z-index: 50;
  color: black;
}

</style>
