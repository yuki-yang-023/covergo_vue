<template>
	<div className="p-2 text-4xl font-black sm:p-8 text-center">
		Tell us about yourself
	</div>
	<div class="p-2 w-4/6 m-auto">
		<div className="my-4">
			<lable for="name" className="text-left">Name</lable>
			<input
				:value="name"
				@input="changeName"
				type="text"
				placeholder="Add text"
				className="p-2 border-2 rounded-lg w-full"
				required
			/>
		</div>
		<div className="my-4">
			<lable for="age">Age</lable>
			<input
				:value="age"
				@input="changeAge"
				type="number"
				placeholder="Add number"
				className="p-2 border-2 rounded-lg w-full"
				min="1"
				required
			/>
		</div>
		<div className="my-4">
			<lable for="location">Where do you live</lable>
			<select
				@input="changeCountry"
				v-model="selected"
				className="p-2 border-2 rounded-lg w-full"
				required
			>
				<option value="Hong Kong">Hong Kong</option>
				<option value="USA">USA</option>
				<option value="Australia">Australia</option>
			</select>
		</div>
		<div className="m-2">
			<input
				type="radio"
				@change="changeRate($event)"
				name="package"
				value=" Standard"
				className="my-4 mr-2"
				required
				checked
			/>
			<label for="Standard">Standard</label><br />
			<input
				type="radio"
				@change="changeRate($event)"
				name="package"
				value="Safe (+250HKD, 50%)"
				className="my-4 mr-2"
				required
			/>
			<label for="Safe">Safe (+250HKD, 50%)</label><br />
			<input
				type="radio"
				@change="changeRate($event)"
				name="package"
				value="Super Safe (+375HKD, 75%)"
				className="my-4 mr-2"
				required
			/>
			<label for="Super">Super Safe (+375HKD, 75%)</label>
		</div>
		<div className="my-10 font-black">
			Your Premium is: {{ 10 * age * rate }} {{ currency }}
		</div>
	</div>
</template>

<script>
export default {
	name: "About",
	data() {
		return {
			rate: 1,
			selected: this.country,
			currency: "HKD",
		}
	},

	components: {},
	props: {
		name: String,
		age: Number,
		country: String,
		package: String,
		premium: String,
	},
	emits: [
		"update:name",
		"update:age",
		"update:country",
		"update:package",
		"update:premium",
	],
	methods: {
		changeName(e) {
			this.$emit("update:name", e.target.value)
		},
		changeAge(e) {
			this.$emit("update:age", e.target.value)
		},
		changeCountry(e) {
			this.$emit("update:country", e.target.value)
			if (e.target.value == "Hong Kong") {
				this.currency = "HKD"
				this.selected = "Hong Kong"
			} else if (e.target.value == "USA") {
				this.currency = "USD"
				this.selected = "USA"
			} else {
				this.currency = "AUD"
				this.selected = "Australia"
			}
			this.$emit("update:premium", 10 * this.age * this.rate + this.currency)
		},
		changeRate(e) {
			this.$emit("update:package", e.target.value)
			if (e.target.value == "Standard") this.rate = 1
			else if (e.target.value == "Safe (+250HKD, 50%)") {
				this.rate = 2
			} else this.rate = 3

			this.$emit("update:premium", 10 * this.age * this.rate + this.currency)
		},
	},
}
</script>
