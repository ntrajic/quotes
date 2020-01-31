<template>
    <div class="container">
        <app-header :quoteCount="quotes.length" :maxQuotes="maxQuotes"></app-header>
        <app-new-quote @quoteAdded="newQuote"></app-new-quote>
        <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuoteInParent"></app-quote-grid>
        <div class="row">
            <div class="col-sm-12 text-center">
                <div class="alert alert-info">Info: Click on a Quote to delete it!
                    <button @click="delQuoteOk = !delQuoteOk">
                        <span class="vue-green">X</span>
                    </button>
                    <p>Copyright 2020, M.Schwartzmüller</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import QuoteGrid from './components/QuoteGrid.vue';
    import NewQuote from './components/NewQuote.vue';
    import Header from './components/Header.vue';

    export default {
        data: function () {
            return {
                delQuoteOk: false,
                quotes: [
                    'Just a Quote that BOC rocks! Please add yours, up to ten per day.'
                ],
                maxQuotes: 10
            }
        },
        methods: {
            newQuote(quote) {
                if (this.quotes.length >= this.maxQuotes) {
                    return alert('Please delete Quotes first! You have reached the max quota for today.');
                }
                this.quotes.push(quote);
            },
            deleteQuoteInParent(index) {
                console.log("InParent: delQuoteOk=", this.delQuoteOk);
                if (this.delQuoteOk) {
                    this.quotes.splice(index, 1);
                }
            }
        },
        components: {
            appQuoteGrid: QuoteGrid,
            appNewQuote: NewQuote,
            appHeader: Header
        }
    }
</script>

<style>
</style>
