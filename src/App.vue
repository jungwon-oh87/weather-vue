<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-input" placeholder="Enter a city..." />
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "3427d2595b7499ffd1720796ac1b567f",
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "montserrat", sans-serif;
}
main {
  min-height: 100vh;
  /* border: 1px solid red; */
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0),
    rgba(0, 0, 0, 0.75)
  );
}
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
  /* border: 1px solid red; */
}

.search-box .search-input {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 16px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  border-radius: 0 16px 0 16px;
  background-color: rgba(255, 255, 255, 0.5);
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  transition: 0.4s;
}

.search-box .search-input:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.75);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0 16px 0;
}
</style>
