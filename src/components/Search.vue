<template>
    <div class="search">
        <h2 class="search__title">Поиск предложений по авиаперелетам</h2>
        <span class="search__description">Пожалуйста, заполните форму</span>

        <form class="search__form" @submit="postPost">
            <div class="search__field">
                <input class="search__input" type="text" v-model="postBody.directions[0].departure_code" id="departure_code" name="departure_code" required/>
                <label class="search__label" for="departure_code">IATA код аэропорта вылета</label>
            </div>
            <div class="search__field">
                <input class="search__input" type="text" v-model="postBody.directions[0].arrival_code" id="arrival_code" name="arrival_code" required/>
                <label class="search__label" for="arrival_code">IATA код аэропорта прилета</label>
            </div>
            <div class="search__field">
                <input class="search__input" type="date" v-model="postBody.directions[0].date" id="date" name="date" min="2019-09-30" required pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}"/>
                <label class="search__label" for="date">Дата вылета</label>
            </div>
            <div class="search__field">
                <input class="search__input" type="text" v-model="postBody.class" id="class" name="class" required/>
                <label class="search__label" for="class">Класс перелета</label>
            </div>
            <button class="search__submit" type="submit">Поиск</button>
        </form>

        <ul class="search__result-list" v-if="offersList.offers">
            <li class="search__result-item" v-for="(item, index) in offersList.offers" :key="index">
                <ResultItem :result="item" :id="index"/>
            </li>
        </ul>

        <div class="search__hidden-value">
            <span>{{ info }}</span>
            <span>{{ responseData }}</span>
            <span>{{ requestId }}</span>
            <span>{{ key }}</span>
            <span>{{ offersList }}</span>
        </div>

    </div>
</template>



<script>
    import axios from 'axios';
    import ResultItem from './ResultItem.vue'

    //const axios = require('axios').default;

    export default {
        name: 'Search',
        components: {
            ResultItem
        },
        data() {
            return {
                info: null,
                responseData: null,
                key: null,
                requestId: null,
                postBody: {
                    directions: [
                        {
                            departure_code: "",
                            arrival_code: "",
                            date: "",
                            time: "M"
                        }
                    ],
                    adult_qnt: 1,
                    child_qnt: 0,
                    infant_qnt: 0,
                    travel_policy_id: 0,
                    one_order_id: 0,
                    passenger_category: "YCD",
                    class: "",
                    direct: true,
                    flexible: true,
                    max_price: 50,
                    airlines: [
                        "SU",
                        "HR"
                    ],
                    fare_types: [
                        "PUB",
                        "NEG"
                    ]
                },
                offersList: {},
                getOffersBody: {
                    status: "inProcess",
                    message: "Нет ошибок",
                    is_round: true,
                    is_multy: false,
                    currency: "RUB",
                    available_currencies: [
                        "EUR",
                        "RUB"
                    ],
                    sort: "price",
                    directions: [
                        {
                            dir_number: 1,
                            date: "2018-04-28",
                            departure_code: "MOW",
                            departure_name: "Москва",
                            departure_country: "RU",
                            arrival_code: "LED",
                            arrival_name: "Санкт-Петербург",
                            arrival_country: "RU"
                        }
                    ],
                    offers: [
                        {
                            carrier_code: "SU",
                            carrier_name: "Аэрофлот",
                            carrier_logo: "https://crm.etm-system.com/images/airline/SU.png",
                            min_price: 5320,
                            offers: [
                                {
                                    min_price: 5320,
                                    segments: [
                                        {
                                            segment_id: 881516214,
                                            buy_id: "839493372_881516214",
                                            is_policy_fail: true,
                                            policy_fail_details: {
                                                leg_fails: [
                                                    {
                                                        leg_num: 1,
                                                        fails: [
                                                            {
                                                                "component_name": "service_class",
                                                                "component_value": "B"
                                                            }
                                                        ]
                                                    }
                                                ],
                                                offer_fails: [
                                                    {
                                                        component_name: "max_price_common",
                                                        component_value: {
                                                            "amount": 1000,
                                                            "currency": "RUB"
                                                        }
                                                    }
                                                ]
                                            },
                                            dir_number: 1,
                                            flight_number: "205",
                                            flight_carrier_code: "SU",
                                            flight_carrier_name: "Аэрофлот",
                                            departure_airport: "VKO",
                                            departure_timestamp: 1524888600,
                                            arrival_airport: "LED",
                                            arrival_timestamp: 1524888600,
                                            duration_formated: "1 ч 20 мин",
                                            duration_minutes: 80,
                                            stops: 0,
                                            flights_info: [
                                                {
                                                    date: "2018-04-28",
                                                    departure_country: "RU",
                                                    departure_city: "Москва",
                                                    departure_airport: "VKO",
                                                    departure_terminal: "string",
                                                    departure_local_time: "08:20",
                                                    departure_timezone: "GMT+03:00",
                                                    arrival_country: "RU",
                                                    arrival_city: "Санкт-Перебург",
                                                    arrival_airport: "LED",
                                                    arrival_terminal: "string",
                                                    arrival_local_time: "09:40",
                                                    arrival_timezone: "GMT+03:00",
                                                    flight_number_print: "SU-205",
                                                    duration_formated: "1 ч 20 мин",
                                                    stop_time: "9 ч 40 мин"
                                                }
                                            ],
                                            tarif: "NVUR",
                                            class: "N",
                                            price: 6975,
                                            baggage: "1PC"
                                        }
                                    ]
                                }
                            ]
                        },
                        {
                            carrier_code: "S7",
                            carrier_name: "S7 Airlines",
                            carrier_logo: "https://crm.etm-system.com/images/airline/S7.png",
                            min_price: 5320,
                            offers: [
                                {
                                    min_price: 5320,
                                    segments: [
                                        {
                                            segment_id: 881516214,
                                            departure_airport: "VKO",
                                            arrival_airport: "LED",
                                            duration_formated: "1 ч 00 мин",
                                            price: 5800,
                                        },
                                        {
                                            segment_id: 881516214,
                                            departure_airport: "VKO",
                                            arrival_airport: "LED",
                                            duration_formated: "1 ч 00 мин",
                                            price: 6000,
                                        }
                                    ]
                                },
                                {
                                    min_price: 3700,
                                    segments: [
                                        {
                                            segment_id: 881516214,
                                            departure_airport: "DME",
                                            arrival_airport: "LED",
                                            duration_formated: "1 ч 10 мин",
                                            price: 3700,
                                            baggage: "1PC"
                                        },
                                        {
                                            segment_id: 881516214,
                                            departure_airport: "DME",
                                            arrival_airport: "LED",
                                            duration_formated: "1 ч 00 мин",
                                            price: 6800,
                                        }
                                    ]
                                },
                            ]
                        }
                    ]
                }
            }
        },
        mounted() {
            axios
                .get('https://crm.etm-system.com/api/login/c6744783c6')
                .then(response => {this.info = response; this.key = this.info.data.etm_auth_key})
        },
        methods: {
            postPost: function(e){
                e.preventDefault();

                axios
                    .post('https://crm.etm-system.com/api/search', {body: this.postBody}, {headers: {'etm-auth-key': this.key}})
                    .then(response => {
                        this.responseData = response;
                        this.requestId = 112;//response.data.request_id - эмуляция ответа запроса
                        if(this.requestId !== null && this.requestId !== undefined){
                            getOffers(this);
                        }
                    });

                function getOffers(context) {
                    axios
                        .get('https://crm.etm-system.com/api/offers?request_id=' + context.requestId, {headers: {'etm-auth-key': context.key}})
                        .then(response => {
                            context.offersList = response;
                            context.offersList = context.getOffersBody;//эмуляция ответа запроса
                        });
                }
            },
        }
    }
</script>



<style>
    .search {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 60px auto;
    }
    .search__description {
        display: inline-block;
        margin-top: 15px;
        margin-bottom: 20px;
    }
    .search__form {
        background-color: #42b983;
        border-radius: 5px;
        width: 640px;
        padding: 40px 20px;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .search__field {
        display: flex;
        flex-direction: column-reverse;
        width: 140px;
        margin: 0 10px;
    }
    .search__input {
        height: 16px;
        padding: 12px 15px;
        font-size: 16px;
        border-radius: 5px;
        background-color: #fff;
        outline: none;
        border: none;
        box-shadow: none;
        position: relative;
    }
    input[type=date]::-webkit-inner-spin-button {
        display: none;
    }
    input[type=date]::-webkit-calendar-picker-indicator {
        width: 10px;
        height: 8px;
        background-color: rgba(0,0,0,0);
        position: absolute;
        z-index: 2;
        right: 5px;
        top: 14px;
        outline: none;
    }
    .search__label {
        color: #fff;
        font-size: 13px;
        font-weight: 500;
        margin-bottom: 10px;
    }
    .search__submit {
        margin-top: 40px;
        width: 180px;
        height: 50px;
        border-radius: 5px;
        background-color: #2c3e50;
        padding: 0;
        text-align: center;
        line-height: 50px;
        border: none;
        font-weight: bold;
        font-size: 18px;
        color: #fff;
        outline: none;
    }
    .search__hidden-value {
        opacity: 0;
        position: absolute;
        z-index: -99;
    }
    .search__result-list {
        width: 680px;
        margin-top: 40px;
    }
    .search__result-item {
        min-height: 60px;
        border-bottom: 1px solid #e0e0e0;
    }

</style>
