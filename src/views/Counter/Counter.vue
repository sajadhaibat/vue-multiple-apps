<template>
    <CCard>
        <CCardHeader>
            <CIcon name="cil-justify-center"/> <strong>CountDown App </strong>
        </CCardHeader>
        <CCardBody>
            <CJumbotron header="Bootstrap 4" lead="">

                <div class="wrap">
                    <h1>Draft <strong>Countdown</strong></h1>

                    <div class="countdown">
                        <div class="bloc-time hours" data-init-value="24">
                            <span class="count-title">Days</span>

                            <div class="figure days day-1">
                                <span class="top">{{displayDays}}</span>
                                <span class="bottom">{{displayDays}}</span>
                            </div>

                        </div>
                        <div class="bloc-time hours" data-init-value="24">
                            <span class="count-title">Hours</span>

                            <div class="figure hours hours-1">
                                <span class="top">{{displayHours}}</span>
                                <span class="bottom">{{displayHours}}</span>
                            </div>

                        </div>

                        <div class="bloc-time min" data-init-value="0">
                            <span class="count-title">Minutes</span>

                            <div class="figure min min-1">
                                <span class="top">{{displayMins}}</span>
                                <span class="bottom">{{displayMins}}</span>
                            </div>
                        </div>

                        <div class="bloc-time sec" data-init-value="0">
                            <span class="count-title">Seconds</span>

                            <div class="figure sec sec-1">
                                <span class="top">{{displaySecs}}</span>
                                <span class="bottom">{{displaySecs}}</span>
                            </div>

                        </div>
                    </div>
                </div>
            </CJumbotron>
        </CCardBody>
    </CCard>



</template>

<script>
    export default {
        name: "Counter",
        data(){
            return {
                displayDays: 0,
                displayHours: 0,
                displayMins: 0,
                displaySecs: 0,
            }
        },
        computed: {

        },
        mounted(){
            this.showRemaining();
        },
        methods:{
            _seconds: () => 1000,
            _minutes(){
                return this._seconds() * 60;
            },
            _hours(){
                return this._minutes() * 60;
            },
            _days(){
                return this._hours() * 24;
            },
            formatNum(num){
                return (num < 10) ? '0' + num : num;
            },
          showRemaining(){
                setInterval(() => {
                    const now = new Date();
                    var end = new Date(2021, 1, 20, 16, 10, 10, 10);
                    var distance = end.getTime() - now.getTime();
                    if( distance < 0){
                        end.setDate(now.getMonth()  + 60);
                         distance = end.getTime() - now.getTime();
                    }

                    const days = Math.floor(distance / this._days());
                    const hours = Math.floor((distance % this._days()) / this._hours());
                    const minutes = Math.floor((distance % this._hours()) / this._minutes());
                    const seconds = Math.floor((distance % this._minutes()) / this._seconds());
                    this.displayDays = this.formatNum(days);
                    this.displayHours = this.formatNum(hours);
                    this.displayMins = this.formatNum(minutes);
                    this.displaySecs = this.formatNum(seconds);
                }, 1000);
          }
        },
    }
</script>

<style scoped>
    .wrap {
        position: relative;
        bottom: 0;
        top: 0;
        left: 0;
        right: 0;
        margin: auto;
        height: 310px;
    }

    a {
        text-decoration: none;
        color: #1a1a1a;
    }

    h1 {
        margin-bottom: 60px;
        text-align: center;
        font: 300 2.25em "Lato";
        text-transform: uppercase;
    }
    h1 strong {
        font-weight: 400;
        color: #ea4c4c;
    }

    h2 {
        margin-bottom: 80px;
        text-align: center;
        font: 300 0.7em "Lato";
        text-transform: uppercase;
    }
    h2 strong {
        font-weight: 400;
    }

    .countdown {
        width: 600px;
        margin: 0 auto;
    }
    .countdown .bloc-time {
        float: left;
        margin-right: 35px;
        text-align: center;
    }
    .countdown .bloc-time:last-child {
        margin-right: 0;
    }
    .countdown .count-title {
        display: block;
        margin-bottom: 15px;
        font: normal 0.94em "Lato";
        color: #1a1a1a;
        text-transform: uppercase;
    }
    .countdown .figure {
        position: relative;
        text-align: center;
        float: left;
        height: 110px;
        width: 120px;
        margin-right: 10px;
        background-color: #fff;
        border-radius: 8px;
        -moz-box-shadow: 0 3px 4px 0 rgba(0, 0, 0, 0.2), inset 2px 4px 0 0 rgba(255, 255, 255, 0.08);
        -webkit-box-shadow: 0 3px 4px 0 rgba(0, 0, 0, 0.2), inset 2px 4px 0 0 rgba(255, 255, 255, 0.08);
        box-shadow: 0 3px 4px 0 rgba(0, 0, 0, 0.2), inset 2px 4px 0 0 rgba(255, 255, 255, 0.08);
    }
    .countdown .figure:last-child {
        margin-right: 0;
    }
    .countdown .figure > span {
        position: absolute;
        left: 0;
        right: 0;
        margin: auto;
        font: normal 5.94em/107px "Lato";
        font-weight: 700;
        color: #de4848;
    }
    .countdown .figure .top:after, .countdown .figure .bottom-back:after {
        content: "";
        position: absolute;
        z-index: -1;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    }
    .countdown .figure .top {
        z-index: 3;
        background-color: #f7f7f7;
        transform-origin: 50% 100%;
        -webkit-transform-origin: 50% 100%;
        -moz-border-radius-topleft: 10px;
        -webkit-border-top-left-radius: 10px;
        border-top-left-radius: 10px;
        -moz-border-radius-topright: 10px;
        -webkit-border-top-right-radius: 10px;
        border-top-right-radius: 10px;
        -moz-transform: perspective(200px);
        -ms-transform: perspective(200px);
        -webkit-transform: perspective(200px);
        transform: perspective(200px);
        /*display: inline-flex;*/
        /*text-align: center;*/
    }
    .countdown .figure .bottom {
        z-index: 1;
        /*display: flex;*/
        /*text-align: center;*/
    }
    .countdown .figure .bottom:before {
        content: "";
        position: absolute;
        display: block;
        top: 0;
        left: 0;
        width: 100%;
        height: 50%;
        background-color: rgba(0, 0, 0, 0.02);
    }
    .countdown .figure .bottom-back {
        z-index: 2;
        top: 0;
        height: 50%;
        overflow: hidden;
        background-color: #f7f7f7;
        -moz-border-radius-topleft: 10px;
        -webkit-border-top-left-radius: 10px;
        border-top-left-radius: 10px;
        -moz-border-radius-topright: 10px;
        -webkit-border-top-right-radius: 10px;
        border-top-right-radius: 10px;
    }
    .countdown .figure .bottom-back span {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        margin: auto;
    }
    .countdown .figure .top, .countdown .figure .top-back {
        height: 50%;
        overflow: hidden;
        -moz-backface-visibility: hidden;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
    }
    .countdown .figure .top-back {
        z-index: 4;
        bottom: 0;
        background-color: #fff;
        -webkit-transform-origin: 50% 0;
        transform-origin: 50% 0;
        -moz-transform: perspective(200px) rotateX(180deg);
        -ms-transform: perspective(200px) rotateX(180deg);
        -webkit-transform: perspective(200px) rotateX(180deg);
        transform: perspective(200px) rotateX(180deg);
        -moz-border-radius-bottomleft: 10px;
        -webkit-border-bottom-left-radius: 10px;
        border-bottom-left-radius: 10px;
        -moz-border-radius-bottomright: 10px;
        -webkit-border-bottom-right-radius: 10px;
        border-bottom-right-radius: 10px;
    }
    .countdown .figure .top-back span {
        position: absolute;
        top: -100%;
        left: 0;
        right: 0;
        margin: auto;
    }
</style>
