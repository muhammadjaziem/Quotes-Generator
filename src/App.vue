<template>
	<div class="app">
		
		<Quote :quote="quote" />
		<div class="button-container">
			<button @click="fetchQuote">NEW QUOTES</button>
		</div>
		<QuoteList :quotes="quotes" />
	</div>
</template>

<script>

import Quote from './components/GenerateQuotes.vue';
import QuoteList from './components/StoresQuotes.vue';

export default {
	name: 'App',
	components: {	
		Quote,
		QuoteList
	},
	data() {
		return {
			quote: {
				content: '',
				character: ''
			},
			quotes: []
		}
	},
	created () {
		this.fetchQuote();
	},
	methods: {
		async fetchQuote () {
			const data = await fetch('http://quotable.io/random').then(res => res.json());

			if (this.quote.content) {
				this.quotes = [...this.quotes, this.quote];
			}

			this.quote = {
				character: data.author,
				content: data.content
			}
		}
	}
}
</script>

<style lang="scss">
:root {
	--primary: #ff0000;
	--secondary: #272323a1;
	--dark: #131A26;
	--light: rgb(255, 255, 255);
	--grey: #848484;
}

* {
	margin: 5px; /*create space around elements, outside of any defined borders*/
	padding: 25px;
	box-sizing: border-box; /*allows us to include the padding and border in an element's total width and height*/
	font-family:'Dancing Script', cursive;
	
}

.button-container {
	display: flex;
	justify-content: center;
	padding: 0px 0px;
	margin: 5px auto;

	button {
		border: none;
		outline: none;
		background-color: var(--primary);
		padding: 16px 100px;
		border-radius: 50px 20px;

		color: var(--light);
		font-size: 1.0em;
		font-weight: 700;
		text-transform: uppercase;
		cursor: pointer;
		transition: 0.4s;

		&:hover {
			background-color: var(--secondary);
		}
	}
}
</style>
