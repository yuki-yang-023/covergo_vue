<template>
	<div className="p-2 text-4xl font-black sm:p-8 text-center">Summary</div>
	<div class="p-2 w-3/6 m-auto">
		<div className="m-4">
			<lable for="name">Name: </lable>
			{{ contactInfo.name }}
		</div>
		<div className="m-4">
			<lable for="age">Age: </lable>
			{{ contactInfo.age }}
		</div>
		<div className="m-4">
			<lable for="location">Where do you live: </lable>
			{{ contactInfo.country }}
		</div>
		<div className="m-4">
			<lable for="location">Package: </lable>
			{{ contactInfo.package }}
		</div>
		<div className="m-4">
			<lable for="premium">Premium: {{ contactInfo.premium }}</lable>
		</div>
	</div>
</template>

<script>
export default {
	name: "Summary",
	data() {
		return {
			step: 1,
			age: 1,
			country: "Hong Kong",
			package: "Standard",
			rate: 1,
			currency: "HKD",
		}
	},
	methods: {
		checkForm: function (e) {
			if (this.name && this.age) {
				return true
			}

			this.errors = []

			if (!this.name) {
				this.errors.push("Name required.")
			}
			if (!this.age) {
				this.errors.push("Age required.")
			}

			e.preventDefault()
		},
	},
	props: {
		contactInfo: Object,
	},
}
</script>
