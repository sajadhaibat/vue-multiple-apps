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
                                <img id="img" src="../../../public/weather/cold.jpg"  width="100%" height="100%" alt="">

                                <div id="country-id">
                                <CInput
                                        type="text"
                                        autocomplete="text"
                                        Placeholder = "Please type Country Name Here, eg. Afghanistan.."
                                        id="country"
                                />
                                </div>
                                <div id="info">
                                    <div id="info-country">
                                    <h3 class="font-weight-bold">Afghansitan, AFG</h3>
                                        <span class="font-weight-bold font-sm">  Sunday, 20201</span>
                                    </div>
                                    <div id="degree-box">
                                        <h1 class="font-weight-bolder">31 <sup>0</sup> C</h1>
                                    </div>

                                    <div id="weather-status">
                                        <h1>Rain</h1>
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
