<template>
    <div>
        <CRow>
            <CCol lg="6" class="offset-3">
                <transition name="fade">
                    <CCard v-if="show">
                        <CCardHeader>
                            <span class="font-weight-bold"> Weather APP </span>
                            <div class="card-header-actions"></div>
                        </CCardHeader>
                        <CCollapse :show="formCollapsed" class="p-0 m-0">
                            <CCardBody id="card-body" class="p-0 m-0">
                                <img id="img" :src="img"  width="100%" height="100%" alt="">

                                <div id="country-id">
                                <CInput
                                        type="text"
                                        autocomplete="text"
                                        Placeholder = "Please type Country Name Here, eg. Afghanistan.."
                                        id="country"
                                        v-model="query"
                                        @keypress.enter="fetchWeather"
                                />
                                </div>
                                <div id="info" v-if="dataAccess">
                                    <div id="info-country">
                                    <h3 class="font-weight-bold">{{weather.name}}, {{weather.sys.country}}</h3>
                                        <span class="font-weight-bold font-sm">{{todayDate()}}</span>
                                    </div>
                                    <div id="degree-box">
                                        <h1 class="font-weight-bolder">{{Math.round(weather.main.temp)}} <sup>0</sup> C</h1>
                                    </div>

                                    <div id="weather-status">
                                        <h1>{{ weather.weather[0].main }}</h1>
                                    </div>
                                </div>
                            </CCardBody>
                        </CCollapse>
                    </CCard>
                </transition>
            </CCol>
        </CRow>
    </div>
</template>

<script>
    export default {
        name: "weather",
        data(){
            return {
                show:true,
                formCollapsed: true,
                api_key: '592095b81b9e01e6f69144446c1db6ab',
                url_base: 'https://api.openweathermap.org/data/2.5/',
                query: '',
                dataAccess: false,
                weather: {},
                img: '../../../public/weather/cold.jpg'
            }
        },
        methods: {
            fetchWeather(){
                fetch(`${this.url_base}weather?q=${this.query}&units=metric&&APPID=${this.api_key}`)
                    .then(res => {
                        return res.json();
                    }).then( results => {
                        this.dataAccess = true;
                    this.weather = results;
                });
            },

            todayDate(){
                var d = new Date();
                var day = d.getDate();
                var month = d.getMonth()+1;
                var year = d.getFullYear();
                if (day < 10) {
                    day = "0" + day;
                }
                if (month < 10) {
                    month = "0" + month;
                }
                console.log(d)
                return  `${day}, ${month}, ${year}`;
            }
        }
    }
</script>

<style scoped>
    .card-body {
        height: 500px;
        /*background-image: url("../../../public/weather/cold.jpg");*/
        /* Center and scale the image nicely */
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        position: relative;
        /*background-blend-mode: screen;*/
        /*filter: brightness(0.7);*/
    }
    #img {
        position: relative;
        filter: brightness(0.5);
    }
    #country-id {
        position: absolute;
        top: 25px;
        width: 90%;
        left: 5%;
    }
    #info-country{
        position: absolute;
        top: 80px;
        width: 80%;
        left: 5%;
        text-align: center;
        color: #f7f7f7;
    }
    #degree-box{
        position: absolute;
        top: 170px;
        width: 30%;
        left: 30%;
        text-align: center;
        color: #f7f7f7;
        background-color: rgba(191, 107 , 107, 0.9);
    }
    #weather-status{
        position: absolute;
        top: 230px;
        width: 30%;
        left: 30%;
        text-align: center;
        color: white;
        font-weight: 500;
        font-style: italic;
    }
    #weather-status h1 {
        font-size: 2.60rem;
    }



</style>
