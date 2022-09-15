<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wether Application</title>
    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }

        .container {
            width: 100%;
            height: 100vh;
            background-color: steelblue;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .row {
            display: flex;
            align-items: center;
            /* vertically align*/
            justify-content: space-evenly;
            /* horizontally align*/
            width: 1000px;
            margin: 10px;
            font-size: 32px;
            color: white;
            padding-right: 20px;

        }

        #search {
            font-size: 25px;
            padding: 10px;
            border-radius: 25px;
            border: none;
            outline: none;
            box-shadow: 0px 0px 5px gray;
        }
        h1{
            color: white;
            padding-bottom: 20px;
            font-family: Verdana, Geneva, Tahoma, sans-serif;
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>WEATHER REPORT APPLICATION</h1>

        <div class="row" style="text-align:center;">
            <form action="">
                <input type="search" id="search" placeholder="Search by City Name...">
            </form>
        </div>
        <div class="row" id="weather">
            <!-- <div>
                <img src="https://openweathermap.org/img/wn/04n@2x.png" alt="">
            </div>
            <div>
                <h2>32 ℃</h2>
                <h4> Clear </h4>
            </div> -->
        </div>
    </div>
    <script>

        // const API_KEY = `3265874a2c77ae4a04bb96236a642d2f`
        const API_KEY = `d21e97bd76ad07c2a49d1fc965c80534`

        const form = document.querySelector("form")
        const search = document.querySelector("#search")
        const weather = document.querySelector("#weather")
        // const API = `https://api.openweathermap.org/data/2.5/weather?
        // q=${city}&appid=${API_KEY}&units=metric`
        // const IMG_URL = `https: //openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`
        const getWeather = async (city) => {
            weather.innerHTML = `<h2> Loading... <h2>`
            // const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric`
            
            // const url = `http://api.openweathermap.org/data/2.5/weather?q=London,uk&APPID=d21e97bd76ad07c2a49d1fc965c80534`
            const url = `http://api.openweathermap.org/data/2.5/weather?q=${city}&APPID=${API_KEY}&units=metric`


            const response = await fetch(url);
            const data = await response.json();
            console.log(data);
            return showWeather(data)
        }

        const showWeather = (data) => {
            if (data.cod == "404") {
                weather.innerHTML = `<h2> City Not Found <h2>`
                return;
            }
            weather.innerHTML = `
        <div>
            <img src="https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png" alt="">
            <h4> ${data.weather[0].main} </h4>

        </div>
        <div>
            <h2>${data.main.temp} ℃</h2>
        </div>
        <div>
            <h2>${data.main.humidity} RH</h2>
        </div>
        <div>
            <h2>${data.main.pressure} Pa</h2>
        </div>
    `
        }

        form.addEventListener(
            "submit",
            function (event) {
                getWeather(search.value)
                event.preventDefault();
            }
        )

    </script>
</body>

</html>
