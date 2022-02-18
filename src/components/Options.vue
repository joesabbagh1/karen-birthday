<template>
  <v-container v-if="!nextPage">
		<v-row>
			<Opening />
		</v-row>
		<v-row align="center" justify="center" style="height:100vh">
			<v-col cols="3" v-for="(option, i ) in options" :key="option.title" align="center">
					<v-img v-if="!option.dialog" :src="closedDoor" width="150px" @click.stop="option.dialog = true" />
					<v-dialog
						width="800px"
						v-model="option.dialog"
					>
						<v-card>
							<v-container class="pa-10">
								<v-row>
									<v-col>
										<div class="text-h3 text-center px-10 pb-10">
											{{option.title}}
										</div>
										<div v-html="option.text" />
										<template v-if="i===0">
											<div class="pt-8 pb-3 font-weight-medium">
												The AirBnb:
											</div>
											<div>
												<v-row>
													<v-col cols="4">
														<v-img :src="require('../assets/1-1.jpeg')"></v-img>
													</v-col>
													<v-col cols="4">
														<v-img :src="require('../assets/1-2.jpeg')"></v-img>
													</v-col>
													<v-col cols="4">
														<v-img :src="require('../assets/1-3.jpeg')"></v-img>
													</v-col>
												</v-row>
											</div>
											<div class="text-h5 font-weight-medium pt-16">
												Museums you can visit on Sunday:
											</div>
											<div class="pt-8 pb-3 font-weight-medium">
												Saint-Laurent Archaeological Museum
											</div>
											<div >
												<v-img :src="require('../assets/1-4.jpeg')"></v-img>
											</div>
											<div class="pt-8 pb-3 font-weight-medium">
												Musee de l'Ancien Eveche
											</div>
											<div>
												<v-img :src="require('../assets/1-5.jpeg')"></v-img>
											</div>
											<div class="pt-8 pb-3 font-weight-medium">
												Le Couvent Sainte-Cécile
											</div>
											<div>
												<v-img :src="require('../assets/1-6.jpeg')"></v-img>
											</div>
										</template>
										<template v-if="i===1">
											<v-row class="pt-7">
												<v-col>
													<v-img :src="require('../assets/2-1.jpeg')"></v-img>
													<div class="pt-3">
														{{heart}}
													</div>
												</v-col>
											</v-row>
										</template>
										<template v-if="i===2">
											<div class="pt-3 pb-3 font-weight-medium">
												Castillo de Annecy: 
											</div>
											<div >
												<v-img :src="require('../assets/3-1.jpeg')"></v-img>
											</div>
											<div class="pt-8 pb-3 font-weight-medium">
												Le Palais de I'Île:
											</div>
											<div >
												<v-img :src="require('../assets/3-2.jpeg')"></v-img>
											</div>
											<div class="pt-8 pb-3 font-weight-medium">
												Annecy Old Town:
											</div>
											<div >
												<v-img :src="require('../assets/3-3.jpeg')"></v-img>
											</div>
										</template>
									</v-col>
								</v-row>
							</v-container>
						</v-card>
					</v-dialog>
				<v-img v-if="option.dialog" :src="openDoor" width="150px" />
				<div class="pt-5">
					<v-btn color="pink lighten-1" class="white--text" @click="love(i)">
						{{option.selected ? 'are you sure?'  : 'select?' }}
					</v-btn>
				</div>
			</v-col>
		</v-row>
  </v-container>
	<v-container v-else>
		<v-row align="center" style="height:100vh">
			<v-col align="center">
				<div class="text-h4">
					{{thankYou}}
				</div>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import Vue from 'vue'
import VueConfetti from 'vue-confetti'
import Opening from './Opening.vue'

Vue.use(VueConfetti)

export default {
	components: {
        Opening,
    },

	data(){
		return{
			closedDoor: require('../assets/closed.png'),
			openDoor: require('../assets/open.png'),
			buttonText:['select?','are you sure?'],
			heart:'Choose this option <3',
			thankYou:'thank you for coming <3',
			nextPage:false,
			options:[
				{title:'In the heart of Grenoble', dialog: false, selected: false, text:'Getaway from your toxic household to a Serena Free space. We are opting for a stay in, in an Airbnb followed by a Day of slow strolls and maybe museums. This would consist of quality to be taking care of yourself and your mental health. We would cook dinner on Saturday and have a relaxing time alone (maybe playing sims but debatable). This is option is if you feel like going out but staying in. Feel free to add any idea/plan because you know best <3'},
				{title:'What about a little spa day?', dialog: false, selected: false, text:'I am taking you to the highest form of self-care by taking you to the Hammam where you chill and get pampered you who deserves the very very best.<br><br>Do you wanna look like that? '},
				{title:'Annecy planning ', dialog: false, selected: false, text:'Annecy would have been great this weekend but weather is fucked up. So, I invite to plan the trip with me<3 every single detail and would be treating you throughout the trip<br><br>So, say yes and accept!<br><br> Things include:<br><br>'},
				{title:'Games and activities with friends', selected: false, dialog: false, text:'Last but really least, game day with friends. I am giving you the choice to wait on your unreliable friends for the next weekend and book a fun activity to do! I have few in mind that you will most definitely like and I will not be disclosing further. (no I don’t ski) <br><br> You would also expect a small thing in the mail that I have already chosen. <br><br> Would love for you to have the most fun so I would understand this one <3 '},
			]
		}
	},

	methods:{
		changeDoorStatus(i){
			this.options[i].doorClosed = !this.options[i].doorClosed
		},
		
		love(i){
			if(this.options[i].selected){
				this.nextPage = true
				this.$confetti.start({
					particles: [
						{
							type: 'heart',
							size: '20',
						},
					],
					defaultColors: [
						'red',
						'pink',
						'#ba0000'
					],
					defaultDropRate: 8
				});
			}
			this.options[i].selected = true
		}
	}

}
</script>

<style>
.door{
	width: 150px;
	height: 200px;
}
</style>