<template>
  <v-container>
		<v-row align="center" justify="center" style="height:100vh">
			<v-col cols="3" v-for="(option ) in options" :key="option.title" align="center">
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
									</v-col>
								</v-row>
							</v-container>
						</v-card>
					</v-dialog>
				<v-img v-if="option.dialog" :src="openDoor" width="150px" />
				<v-btn text @click="love">
					select?
				</v-btn>
			</v-col>
		</v-row>
  </v-container>
</template>

<script>
import Vue from 'vue'
import VueConfetti from 'vue-confetti'

Vue.use(VueConfetti)

export default {
	computed:{
	},

	data(){
		return{
			closedDoor: require('../assets/closed.png'),
			openDoor: require('../assets/open.png'),
			buttonText:['select?','are you sure?'],
			options:[
				{title:'Games and activities with friends', dialog: false, text:'Last but really least, game day with friends. I am giving you the choice to wait on your unreliable friends for the next weekend and book a fun activity to do! I have few in mind that you will most definitely like and I will not be disclosing further. (no I don’t ski) <br><br> You would also expect a small thing in the mail that I have already chosen. <br><br> Would love for you to have the most fun so I would understand this one <3 '},
				{title:'In the heart of Grenoble', dialog: false, text:'Getaway from your toxic household to a Serena Free space. We are opting for a stay in, in an Airbnb followed by a Day of slow strolls and maybe museums. This would consist of quality to be taking care of yourself and your mental health. We would cook dinner on Saturday and have a relaxing time alone (maybe playing sims but debatable). This is option is if you feel like going out but staying in. Feel free to add any idea/plan because you know best <3'},
				{title:'What about a little spa day?', dialog: false, text:'I am taking you to the highest form of self-care by taking you to the Hammam where you chill and get pampered you who deserves the very very best.<br><br>Do you wanna look like that? '},
				{title:'ydo', dialog: false, text:''},
			]
		}
	},

	methods:{
		changeDoorStatus(i){
			this.options[i].doorClosed = !this.options[i].doorClosed
		},
		start() {
        this.$confetti.start();
      },
			love(){
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
	}

}
</script>

<style>
.door{
	width: 150px;
	height: 200px;
}
</style>