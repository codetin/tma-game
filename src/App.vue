<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import WebApp from '@twa-dev/sdk'
import { ref } from 'vue'

let count = ref(0)
function call() {
	WebApp.showAlert(`Hello World! Current count is ${count}`)
	WebApp.openTelegramLink('https://t.me/share/url?text=%F0%9F%9A%80%F0%9F%9A%80%F0%9F%9A%80%E5%BC%80%E5%A7%8B%E6%B5%8B%E8%AF%95%E6%88%91%E7%9A%84%E9%93%BE%E6%8E%A5%E5%90%A7%0A&url=https://t.me/teletest3721_bot/game?startapp=3JRL8T')
}

function invite() {
	WebApp.openLink('https://t.me/share/url?text=%F0%9F%9A%80%F0%9F%9A%80%F0%9F%9A%80%E5%BC%80%E5%A7%8B%E6%B5%8B%E8%AF%95%E6%88%91%E7%9A%84%E9%93%BE%E6%8E%A5%E5%90%A7%0A&url=https://t.me/teletest3721_bot/game?startapp=3JRL8T')
}
console.log(WebApp.version)
console.log(JSON.stringify(WebApp.initDataUnsafe))
console.log("-----------------")
console.log(WebApp.initData)
console.log("-----------------")
console.log(WebApp.initDataUnsafe.start_param ? WebApp.initDataUnsafe.start_param : "")
// console.log(atob(WebApp.initDataUnsafe.start_param))
const init_data = WebApp.initData as string;
try {
	let url = `http://localhost:3000/login?initdata=${init_data}`;
	fetch(url, {
		method: "GET",
		headers: {
			"Content-Type": "application/json",
		},
	}).then((res) => {
		const jsonResponse = await res.json(); // 等待解析 JSON
		const uid = jsonResponse.data.uid; // 访问 data.uid
		console.log(uid); // 打印 data
		console.log(jsonResponse.data); // 打印 data
	});
} catch (error) {
	console.log(error);
}


function init() {
	if (!WebApp) {
		return
	}
	if (Number(WebApp.version) < 7.0) {
		return
	}
	if (!WebApp.initDataUnsafe) {
		return
	}
	if (!WebApp.initDataUnsafe.user) {
		return
	}
</script>

<template>
	<header>
		<img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

		<div class="wrapper">
			<HelloWorld msg="1" />
			{{ count }}
			<div style="font-size: xx-large;">1</div>
			<button @click="call">分享链接</button>
			<button @click="invite">邀请好友</button>
		</div>
	</header>

	<RouterView />
</template>

<style scoped>
header {
	line-height: 1.5;
	max-height: 100vh;
}

.logo {
	display: block;
	margin: 0 auto 2rem;
}

nav {
	width: 100%;
	font-size: 12px;
	text-align: center;
	margin-top: 2rem;
}

nav a.router-link-exact-active {
	color: var(--color-text);
}

nav a.router-link-exact-active:hover {
	background-color: transparent;
}

nav a {
	display: inline-block;
	padding: 0 1rem;
	border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
	border: 0;
}

@media (min-width: 1024px) {
	header {
		display: flex;
		place-items: center;
		padding-right: calc(var(--section-gap) / 2);
	}

	.logo {
		margin: 0 2rem 0 0;
	}

	header .wrapper {
		display: flex;
		place-items: flex-start;
		flex-wrap: wrap;
	}

	nav {
		text-align: left;
		margin-left: -1rem;
		font-size: 1rem;

		padding: 1rem 0;
		margin-top: 1rem;
	}
}
</style>
