<template>
	<form>
		<div className="w-4/6 m-auto p-2 sm:w-2/6">
			<div>
				<div>
					<Welcome v-if="step === 1" />
					<About
						v-else-if="step === 2"
						v-model:name="contactInfo.name"
						v-model:age="contactInfo.age"
						v-model:country="contactInfo.country"
						v-model:package="contactInfo.package"
						v-model:premium="contactInfo.premium"
					/>
					<Summary :contactInfo="contactInfo" v-else-if="step === 3" />
					<Error v-else />
				</div>

				<div className="m-2 text-center">
					<button
						v-if="step === 1"
						className="bg-black text-white  px-8 py-2 m-2 rounded border-2 border-slate-900"
						@click="step += 1"
					>
						Start
					</button>
					<div v-else-if="step === 2">
						<button
							className="bg-white text-black  px-7 py-2 m-2 rounded border-2 border-slate-900"
							@click="step -= 1"
						>
							Back
						</button>
						<button
							className="bg-black text-white  px-8 py-2 m-2 rounded border-2 border-slate-900"
							v-if="contactInfo.age < 100"
							@click="step += 1"
						>
							Next
						</button>
						<button
							className="bg-black text-white  px-8 py-2 m-2 rounded border-2 border-slate-900"
							v-else
							@click="step = 4"
						>
							Next
						</button>
					</div>
					<div v-else-if="step === 3">
						<button
							className="bg-white text-black px-10 py-2 rounded border-2 border-slate-900"
							@click="step -= 1"
						>
							Back
						</button>
						<button
							className="bg-black text-white  px-10 py-2 m-2 rounded border-2 border-slate-900"
							@click="step = 1"
						>
							Buy
						</button>
					</div>
					<div v-else>
						<button
							className="bg-black text-white  px-8 py-2 m-2 rounded"
							@click="step = 1"
						>
							Ok :(
						</button>
					</div>
				</div>
			</div>
		</div>
	</form>
</template>

<script>
import Welcome from "./components/welcome.vue"
import About from "./components/about.vue"
import Summary from "./components/summary.vue"
import Error from "./components/error.vue"
export default {
	name: "Home",

	components: { Welcome, About, Summary, Error },
	data() {
		return {
			step: 1,
			contactInfo: {
				name: "Yuki Yang",
				age: 30,
				country: "Hong Kong",
				package: "Standard",
				// rate: 1,
				currency: "HKD",
			},
		}
	},
	computed: {},
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
	margin-top: 160px;
}
</style>
