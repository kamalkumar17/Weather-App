In this article, we developed an Interactive Weather Application using ReactJS Framework. The developed application will provide real-time weather information to the user for the city they have searched. If the user searches, for the wrong city, an Error message is also displayed to the user. We have used OpenWeatherMap API which provides us with access to weather data from around the world. We have fetched the weather information for various locations, including wind speed and more.

![Screenshot 2024-04-25 191500](https://github.com/kamalkumar17/Weather-App/assets/160104271/c1a46ab1-116d-44b7-8bf8-5109a06eab23)


.CSS
.JSX
.ReactJS
.Function Components in React

.JSX File
import React from 'react';
import { useState } from "react";
import "./WeatherApp.css";
import search_icon from "../Assets/search.png";
import clear_icon from "../Assets/clear.png";
import cloud_icon from "../Assets/cloud.png";
import drizzle_icon from "../Assets/drizzle.png";
import rain_icon from "../Assets/rain.png";
import snow_icon from "../Assets/snow.png";
import wind_icon from "../Assets/wind.png";
import humidity_icon from "../Assets/humidity.png";
export const WeatherApp = () => {
  let api_key="9e89af3257435c0d6dc99656d490fd9f";
  const [wicon,setWicon]=useState(cloud_icon);

  const search=async()=>{
    let element=document.getElementsByClassName("cityinput");
    if(element[0].value===""){
      return 0;
    }
    let url=`https://api.openweathermap.org/data/2.5/weather?q=${element[0].value}&units=Metric&appid=${api_key}`;
    let response=await fetch(url);
    let data=await response.json();
    const humidity=document.getElementsByClassName("humidity-percent");
    const wind=document.getElementsByClassName("wind-rate");
    const temp=document.getElementsByClassName("weather-temp");
    const location=document.getElementsByClassName("weather-location");
    humidity[0].innerHTML=data.main.humidity+"%";
    wind[0].innerHTML=data.wind.speed+" km/h";
    temp[0].innerHTML=data.main.temp+"°C";
    location[0].innerHTML=data.name;


    if(data.weather[0].icon==="01d" || data.weather[0].icon==="01n" )
    {
      setWicon(clear_icon);
    }
    else if(data.weather[0].icon==="02d" || data.weather[0].icon==="02n" )
    {
      setWicon(cloud_icon);
    }

    else if(data.weather[0].icon==="03n" || data.weather[0].icon==="03n" )
    {
      setWicon(drizzle_icon);
    }

    else if(data.weather[0].icon==="04d" || data.weather[0].icon==="04n" )
    {
      setWicon(drizzle_icon);
    }

    else if(data.weather[0].icon==="09d" || data.weather[0].icon==="09n" )
    {
      setWicon(rain_icon);
    }

    else if(data.weather[0].icon==="10d" || data.weather[0].icon==="10n" )
    {
      setWicon(rain_icon);
    }

    else if(data.weather[0].icon==="13d" || data.weather[0].icon==="13n" )
    {
      setWicon(snow_icon);
    }
    else{
      setWicon(clear_icon);
    }
  }
  return (
    <div className='container'>
      <div className="top-bar">
        <input type="text" className="cityinput" placeholder="Search"/>
        <div className="search_icon" onClick={()=>{search()}}>
          <img src={search_icon}  alt="search_icon" />
        </div>
      </div>

      <div className="weather-image">
        <img src={wicon} alt="" />
      </div>
      <div className="weather-temp"> 24°C</div>
      <div className="weather-location">London</div>
      <div className="data-container">
        <div className="element">
          <img src={humidity_icon} alt=""  className="icon" />
          <div className="data">
            <div className="humidity-percent">64%</div>
            <div className="text">Humidity</div>
          </div>
        </div>

        <div className="element">
          <img src={wind_icon} alt="" className="icon"/>
          <div className="data" >
            <div className="wind-rate">18km/h</div>
            <div className="text">Wind Speed</div>
          </div>
        </div>

      </div>
    </div>
  )
}

.CSS File

.container{
    width: 607px;
    height: 829px;
    margin: auto;
    margin-top: 75px;
    border-radius: 12px;
    background-image: linear-gradient(180deg,#130754 0%,#3b2f80 100%);
}

.top-bar{
    display:flex;
    justify-content: center;
    gap: 14px;
    padding-top: 60px;
}

.top-bar input{
    display: flex;
    width: 362px;
    height: 78px;
    border-radius:50px;
    background: #ebfffc;
    color: #626262;
    border: none;
    outline: none;
    padding-left: 40px;
    font-size: 20px;
    font-weight: 400;
}

.search_icon{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 78px;
    width: 78px;
    border-radius: 50px;
    background: #ebfffc;
    cursor: pointer;
}

.weather-image{
    margin-top: 39px;
    display: flex;
    justify-content: center;
}

.weather-temp{
    display: flex;
    justify-content: center;
    font-size: 100px;
    color: white;
    font-weight: 400;
}

.weather-location{
    display: flex;
    justify-content: center;
    font-size: 60px;
    color: white;
    font-weight: 400;
}

.data-container{
    margin-top: 50px;
    display: flex;
    justify-content:center;
    color: white;
}

.element{
    display: flex;
    margin: auto;
    align-items: flex-start;
    gap: 12px;

}

.data{
    font-size: 34px;
    font-weight: 400;
}

.text{
    font-size: 20px;
    font-weight: 400;
}

.icon{
    margin-top: 10px;
}
