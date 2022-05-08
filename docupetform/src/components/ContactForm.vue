<template>
	<el-row justify="center">
		<el-col :xs="24" :sm="16" :md="14">
			<el-card>
				<el-form v-model="form" label-position="top" size="large">
					<PawProgress :max="7" :active="2" />

					<h1>Tell us about your pet</h1>

					<el-form-item label="Whats your pets's name?" prop="name">
						<el-input v-model="form.name" placeholder="Monte" />
					</el-form-item>

					<el-form-item label="Whats your pets's type?">
						<el-radio-group v-model="form.type" @change="filterType">
							<el-radio label="Cat" />
							<el-radio label="Dog" />
						</el-radio-group>
					</el-form-item>

					<el-form-item label="What breed are they?">
						<el-autocomplete
							v-model="form.breed"
							:suffix-icon="Search"
							:fetch-suggestions="querySearch"
							:trigger-on-focus="true"
							clearable
							class="w-100"
						/>
					</el-form-item>

					<el-row v-if="form.breed == `Can't find it?`">
						<el-col :span="20" :offset="2">
							<div>
								<el-form-item label="Choose One">
									<el-radio-group
										class="radio-group--inner"
										v-model="form.chooseAnswer"
									>
										<el-radio label="I don't know" />
										<el-radio label="It's a mix" />
									</el-radio-group>
								</el-form-item>

								<el-form-item v-if="form.chooseAnswer == `It's a mix`">
									<el-input
										v-model="form.mix"
										placeholder="Collie, poodle, lab"
									/>
								</el-form-item>
							</div>
						</el-col>
					</el-row>

					<el-form-item label="What gender are they?">
						<el-radio-group v-model="form.gender">
							<el-radio-button label="Female" />
							<el-radio-button label="Male" />
						</el-radio-group>
					</el-form-item>

					<el-form-item class="justify-content--center">
						<el-button
							type="primary"
							@click="onSubmit"
							round
							:disabled="isDisabled"
						>
							Continue
						</el-button>
					</el-form-item>
				</el-form>
			</el-card>
		</el-col>
	</el-row>
</template>
<script setup>
import { Search } from "@element-plus/icons-vue";
import PawProgress from "./PawProgress.vue";
</script>
<script>
export default {
	/* eslint-disable */
	name: "ContactForm",
	components: PawProgress,
	data: () => ({
		form: {
			name: "",
			type: "",
			breed: "",
			chooseAnswer: "",
			mix: "",
			gender: "",
		},
		petTypeFilter: [],
		petBreedList: [{ type: "Unknown", value: "Can't find it?" }],
	}),
	computed: {
		isDisabled() {
			if (
				!this.form.name ||
				!this.form.type ||
				!this.form.breed ||
				!this.form.gender ||
				(this.form.breed == `Can't find it?` && !this.form.chooseAnswer) ||
				(this.form.chooseAnswer == `It's a mix` && !this.form.mix)
			) {
				return true;
			}
		},
	},
	methods: {
		// list of pets
		loadPets() {
			return [
				{ type: "Dog", value: "Golden Retriever" },
				{ type: "Dog", value: "Labrador Retriever" },
				{ type: "Dog", value: "English Bulldog" },
				{ type: "Dog", value: "French Bulldog" },
				{ type: "Dog", value: "German Shepherd" },
				{ type: "Dog", value: "Beagle" },
				{ type: "Dog", value: "Rottweiler" },
				{ type: "Cat", value: "Exotic Shorthair" },
				{ type: "Cat", value: "Ragdoll" },
				{ type: "Cat", value: "British Shorthair" },
				{ type: "Cat", value: "Persian" },
				{ type: "Cat", value: "Maine Coon" },
				{ type: "Cat", value: "American Shorthair" },
				{ type: "Cat", value: "Sphynx" },
			];
		},

		// filter list based on pet type
		filterType(type, callback) {
			this.petTypeFilter = [...this.petBreedList];
			this.form.breed = "";

			const results = this.petTypeFilter.filter(
				this.createFilter(type, "type")
			);

			// keep first object and append results after
			this.petTypeFilter = [...this.petTypeFilter.splice(0, 1), ...results];
		},

		// filter through pet type
		querySearch(queryString, callback) {
			this.form.chooseAnswer = "";
			this.form.mix = "";

			const results = queryString
				? this.petTypeFilter.filter(this.createFilter(queryString, "value"))
				: this.petTypeFilter;

			//call callback function to return matching breeds
			callback(results);
		},

		// return matching type and breeds
		createFilter(queryString, property) {
			return (breed) => {
				return (
					breed[property].toLowerCase().indexOf(queryString.toLowerCase()) === 0
				);
			};
		},

		// submit handler
		onSubmit() {
			console.log(this.form);
		},
	},
	mounted() {
		this.petBreedList.push(...this.loadPets());
	},
};
</script>
<style></style>
