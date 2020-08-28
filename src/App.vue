<template>
  <div>
    <div
      id="app"
      :class="typeof weather.main != 'undefined' && weather.main.temp > 85 ? 'warm' : ''"
    >
      <main>
        <div class="search-container">
          <input
            type="text"
            class="search-input"
            placeholder="Enter a city..."
            v-model="query"
            @keypress="fetchWeather"
          />
        </div>
        <div class="content-container" v-if="typeof weather.main != 'undefined'">
          <div class="location-container">
            <div class="location">{{weather.name}}, {{weather.sys.country}}</div>

            <!-- <div class="location">{{weather.sys.country}}</div> -->
            <div class="date">{{getDate()}}</div>
          </div>
          <div class="weather-container">
            <div class="temp">{{Math.round(weather.main.temp)}}°f</div>
            <div class="weather">{{weather.weather[0].main}}</div>
          </div>
        </div>
        <div
          class="content-container error"
          v-else-if="typeof weather.main === 'undefined' && this.weather.cod === '404'"
        >{{this.weather.message}}</div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "3427d2595b7499ffd1720796ac1b567f",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResult);
        this.query = "";
        console.log("weather main: ", this.weather.main);
      }
    },
    setResult(result) {
      console.log("result: ", result);
      this.weather = result;
      // let d = new Date();
      // console.log(d.getDay());
    },
    getDate() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let month = months[d.getMonth()];
      let date = d.getDate();
      let day = days[d.getDay()];
      let year = d.getFullYear();
      // console.log("day: ", day);
      // console.log("month: ", month);
      // console.log("date: ", d.getDate());
      return `${day} ${month} ${date}, ${year}`;
    },
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
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  background-image: url("./assets/warm-bg.jpg");
}

.search-container {
  width: 100%;
  margin-bottom: 30px;
  /* border: 1px solid red; */
}

.search-container .search-input {
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

.location-container .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.error {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-container .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-container {
  text-align: center;
}

.weather-container .temp {
  display: inline-block;
  background-color: rgba(225, 225, 225, 0.25);
  padding: 10px 25px;
  font-size: 100px;
  font-weight: 900;
  border-radius: 16px;
  color: #fff;
  margin: 30px 0;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  box-shadow: 3px 6px rgba(66, 64, 226, 0.25);
}

.weather-container .weather {
  color: #fff;
  font-size: 48px;
  font-style: italic;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
