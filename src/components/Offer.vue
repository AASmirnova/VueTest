<template>
    <div class="offer">
        <div class="offer__info">
            <span class="offer__info-property">Аэропорт вылета</span>
            <span class="offer__info-value">{{offer.departure_airport}}</span>
        </div>
        <div class="offer__info">
            <span class="offer__info-property">Аэропорт прилета</span>
            <span class="offer__info-value">{{offer.arrival_airport}}</span>
        </div>
        <div class="offer__info">
            <span class="offer__info-property">Время в пути</span>
            <span class="offer__info-value">{{offer.duration_formated}}</span>
        </div>
        <div class="offer__info">
            <span class="offer__info-property">Цена билета</span>
            <span class="offer__info-value">{{offer.price}}</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Offer',
        props: {
            offer: {
                type: Object,
                required: true
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .offer {
        display: flex;
        width: calc(100% - 80px);
        padding: 15px 40px;
        align-items: flex-start;
        border-bottom: 1px solid #f2f2f2;
    }
    .offer:before {
        counter-increment: offers;
        content: counter(offers);
        position: relative;
        font-size: 16px;
        display: inline-block;
        min-width: 70px;
        margin-right: 20px;
    }
    .offer__info {
        width: 120px;
        margin-right: 15px;
    }
    .offer__info-property {
        font-size: 13px;
        display: inline-block;
        width: 100%;
        margin-bottom: 10px;
    }
    .offer__info-value {
        font-size: 15px;
        font-weight: 600;
        display: inline-block;
        width: 100%;
    }
</style>