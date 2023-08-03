<script setup lang="ts">

</script>

<template>
  <main>
    <div class="search-box">
      <input type="text" name="" id="" class="search-bar" placeholder="Search">
    </div>
    <div class="weather-wrap">
      <div class="location-box">
        <div class="location">London</div>
        <div class="date">Monday 20</div>
        <div class="weather-box">
          <div class="temp">9 C</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  color: #313131;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus{
  background-color: rgba(255,255,255,0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius:  16px 0px 16px 0px;


}
</style>
