<template>
<div>
	<v-dialog
        v-model="alertKunci"
        persistent
        max-width="300"
        >
        <v-alert
            border="left"
            color="deep-purple accent-4"
            type="info"
            dark>
                Maaf, untuk sementara ayat ini masih dikunci
				<v-btn class="mt-4" block v-on:click="alertKunci=false">Tutup</v-btn>
        </v-alert>
    </v-dialog>
	<v-card dark color="primary" style="height:100px" rounded="0">

	</v-card>
	<v-container style="margin-top:-100px" class="teal lighten-5">
		<v-card>
			<v-card-text class="d-flex align-center">
				<div class="mr-2" style="width:150px">
					<v-card color="teal lighten-4" elevation="0">
						<v-card-title class="d-block text-truncate">{{ userNama }}</v-card-title>
						<v-card-subtitle>Level: pemula </v-card-subtitle>
						<v-card-subtitle>Target: 10 ayat per hari</v-card-subtitle>
					</v-card>
				</div>
				<div class="grow">
					<v-list-item dense class="pl-0">
						<v-list-item-title>
							Hafalan Ayat
						</v-list-item-title>
						<v-list-item-action-text>
							{{ ayatDihafal }}/6236
						</v-list-item-action-text>
					</v-list-item>
					<v-progress-linear :value="(ayatDihafal/6236)*100" height="10" rounded stream/>
					<v-list-item dense class="pl-0">
						<v-list-item-title>
							Hafalan Surat
						</v-list-item-title>
						<v-list-item-action-text>
							{{ suratDihafal }}/114
						</v-list-item-action-text>
					</v-list-item>
					<v-progress-linear :value="(suratDihafal/114)*100" height="10" rounded stream/>
					<v-list-item dense class="pl-0">
						<v-list-item-title>
							Hafalan Juz
						</v-list-item-title>
						<v-list-item-action-text>
							{{ juzDihafal}}/30
						</v-list-item-action-text>
					</v-list-item>
					<v-progress-linear :value="(juzDihafal/30)*100" height="10" rounded stream/>
				</div>
			</v-card-text>
		</v-card>
	<v-row>
		<v-col cols="12">
			
		</v-col>

		<v-col cols="12"
			v-if="surat.length>0">
			<p class="text-overline mb-0">Terakhir dihafal</p>
			<v-card 
				dark 
				color="primary"
				:to="`/surat/${ayatTarget.id}`"
				hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-star-check</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>{{ ayatTarget.surat_name }}</v-list-item-title>
						<v-list-item-subtitle>{{ ayatTarget.count_ayat }} ayat</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card>
		</v-col>

		<v-col cols="12">
			<p class="text-overline mb-0">Juz 30</p>
			<v-card 
				v-for="(item, index) in surat"
				:key="index"
				dark 
				color="primary" 
				class="mb-4">
				<v-list-item
					v-on:click="handelMasukSurat(item)">
					<v-list-item-avatar>
						<v-avatar
							color="teal darken-4">
							{{ item.id }}
						</v-avatar>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>{{ item.surat_name }}</v-list-item-title>
						<v-list-item-subtitle>{{ item.surat_terjemahan }} - {{item.count_ayat}} Ayat</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
						{{ item.surat_text }}
					</v-list-item-action-text>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card>
			<!-- <v-card dark color="primary" class="mb-4">
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-decagram</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Alfatihah</v-list-item-title>
						<v-list-item-subtitle>7 ayat</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card> -->
		</v-col>
		
	</v-row>
	</v-container>
	<v-btn
		v-model="fab"
		fab
		dark
		color="primary"
		bottom
		right
		absolute
		class="mb-16"
		v-on:click="fab=true">
		<v-icon>
			mdi-chat
		</v-icon>
	</v-btn>
	<v-dialog
		v-model="fab"
		persistent
		max-width="480">
	<v-card 
		v-if="fab"
		class="card-chat d-flex flex-column justify-content-between"
		flat>
		<div>
			<v-toolbar>
				<v-toolbar-title>Nazmi - BOT Asisten Hafalan</v-toolbar-title>
			</v-toolbar>
		</div>
		<v-card-text class="card-chat-percakapan flex-grow-1 px-0">
			<v-list-item dense
				v-for="(item, index) in percakapan"
				:key="index"
				:class="`mt-1 ${item.saya?'ml-8 justify-end':'mr-8'}`">
				<v-card 
					dark 
					:color="item.saya?'primary':'grey darken-3'" 
					class="pa-2">
					<div v-html="item.pesan"></div>
				</v-card>	
			</v-list-item>
			
		</v-card-text>
		
		<div>
			<v-text-field
				v-if="percakapan.length===0 || percakapan[percakapan.length-1].mode==='teks'"
				outlined
				hide-details=""
				placeholder="Ketik balasan disini ..."
				dense
				append-icon="mdi-send"
				:click:append="handelKirimPesan"
				v-model="pesan"
				v-on:keyup.enter="handelKirimPesan"/>

			<div v-else>
				<v-card elevation="5" dark color="primary">
					<v-list-item-group>
					<v-list-item 
						v-for="(item, index) in percakapan[percakapan.length-1].opsi"
						:key="index"
						dense
						v-on:click="pesan=item; handelKirimPesan(); mode='teks'">
						<v-list-item-title>{{ item }}</v-list-item-title>
						<v-list-item-action>
							<v-icon>
								mdi-chevron-right
							</v-icon>
						</v-list-item-action>
					</v-list-item>
				</v-list-item-group>
				</v-card>
			</div>
		</div>
	</v-card>
	</v-dialog>
</div>
</template>
<script>
export default {
	asyncData: async function({ query }){
		
		let userNama	= localStorage.getItem('userNama')
		let step		= userNama?5:1;

		let ayatDihafal	= localStorage.getItem('ayatDihafal')||0
		let ayatTarget	= JSON.parse(localStorage.getItem('ayatTarget'))||{
								"id": 1,
								"surat_name": "Al-Fatihah",
								"surat_text": " \u0627\u0644\u0641\u0627\u062a\u062d\u0629",
								"surat_terjemahan": "Pembukaan",
								"count_ayat": 7
							}
		let suratDihafal= localStorage.getItem('suratDihafal')||0
		let juzDihafal	= localStorage.getItem('juzDihafal')||0

		const surat		= []
		const fab		= query.kembali?false:true
		return {
			userNama,
			step,

			ayatDihafal,
			ayatTarget,
			suratDihafal,
			juzDihafal,
			surat,
			fab,
		}
	},
	data: function(){
		return {
			percakapan: [],
			pesan: '',
			alertKunci: false
		}
	},
	mounted: function(){
		let delay		= 500;
		let percakapan 	= []
		let mode		= 'teks'
		let opsi		= []
		if(this.step===1){
			percakapan = [
				'Assalamualaykum ... 😊',
				'perkenalkan, saya Nazmi',
				'Nazmi adalah virtual asisten untuk membantu kakak menghafal al-quran 👼👼👼',
				'kalau boleh tau, nama kakak siapa ?',
			]
		}else{
			percakapan = [
				'Assalamualaykum ... 😊',
				`Halo kak ${this.userNama}`,
				'Selamat datang kembali di tahfidzdigital',
				`Terakhir kakak sedang menghafal surat ${this.ayatTarget.surat_name}`,
				`Yuk kita lanjutkan kembali hafalanya 👼👼👼`,
			]
			mode		= "opsi"
			opsi		= ["😊 Lanjutkan hafalan"]
		}

		percakapan.map((item)=>{
			this.handelKirimPesanDelay(delay, {
				saya: false,
				pesan: item,
				mode: mode,
				opsi: opsi,
			})
			delay	+= 1000
		})
		
		this.handelLoadDataSurat()
	},
	watch:{
		percakapan: function(){
			setTimeout(()=>{
				const chatarea	= document.querySelector(".card-chat-percakapan")
				if(chatarea){
					chatarea.scrollTo(0, chatarea.scrollHeight+10000)
				}
			}, 50)
		},
	},
	methods:{
		handelKirimPesanDelay: function(delay=0, pesan){
			setTimeout(()=>{
				this.percakapan.push(pesan)
			}, delay)
		},
		handelKirimPesan: function(){
			this.percakapan.push({
				saya: true,
				pesan: this.pesan,
				mode: 'teks',
				opsi: [],
			})
			
			this.handelResponBot(this.pesan)
			this.pesan	= ""
		},
		handelResponBot:function(pesan){
			if(this.step===1){

				this.userNama	= pesan
				// localStorage.setItem('userNama', pesan)

				this.handelKirimPesanDelay(1000, {
					saya: false,
					pesan: "Halo kak "+this.userNama,
					mode: 'teks',
					opsi: [],
				})

				this.handelKirimPesanDelay(2000, {
					saya: false,
					pesan: "Ok, sebelum memulai menghafal, ijinkan nazmi menginformasikan, manfaat dan motivasi untuk jadi penghafal alquran ya 😊",
					mode: 'opsi',
					opsi: ['ok nazmi, susahkah menghafal alquran ?'],
				})

				this.step	= 2
			}else if(this.step===2){

				this.handelKirimPesanDelay(1000, {
					saya: false,
					pesan: "Enggak kok, belajar alquran itu mudah lho ...",
					mode: 'teks',
					opsi: [],
				})

				this.handelKirimPesanDelay(2000, {
					saya: false,
					pesan: "Allah SWT Berfirman: ",
					mode: 'teks',
					opsi: ['Ok nazmi, lanjutkan'],
				})

				this.handelKirimPesanDelay(3000, {
					saya: false,
					pesan: "Dan sungguh, telah Kami mudahkan Al-Qur’an untuk peringatan, maka adakah orang yang mau mengambil pelajaran? <br/> <br/> QS Al-Qamar: 17",
					mode: 'opsi',
					opsi: ['Ok nazmi, apa manfaat menghafal alquran ?'],
				})
				

				this.step	= 3

			}else if(this.step===3){
				
				this.handelKirimPesanDelay(500, {
					saya: false,
					pesan: "Ok, nazmi jelasin ya, berikut fadhilah menghafal alquran",
					mode: 'opsi',
					opsi: ['belum nazmi, lanjutkan'],
				})

				this.handelKirimPesanDelay(1000, {
					saya: false,
					pesan: "Mendapatkan syafaat di hari kiamat <br/> <br/> “Bacalah Al Qur’an, karena ia akan datang pada hari kiamat sebagai syafa’at bagi shahibul Qur’an” (HR. Muslim  804)",
					mode: 'teks',
					opsi: ['belum nazmi, lanjutkan'],
				})

				this.handelKirimPesanDelay(2000, {
					saya: false,
					pesan: "Mendapatkan pertolongan Allah <br/><br/> Allah menegaskan bahwa siapa yang menolong Allah, maka Allah akan menolongya. (Q.S. Muhammad: 7). <br/> <br/> Menghafal Al-Quran adalah salah satu bentuk menolong Allah; yaitu memperjuangankan agama Islam.",
					mode: 'teks',
					opsi: ['belum nazmi, lanjutkan'],
				})

				this.handelKirimPesanDelay(3000, {
					saya: false,
					pesan: "Menambah kenikmatan dalam Shalat <br/> <br/> Seorang hafidz akan menikmati shalat yang ia lakukan, baik ia sebagai imam maupun ma’mum.",
					mode: 'teks',
					opsi: ['belum nazmi, lanjutkan'],
				})

				this.handelKirimPesanDelay(4000, {
					saya: false,
					pesan: "Kerenkan manfaatnya ?, sudah siap memulai menghafal alquran bareng nazmi ? 😊",
					mode: 'opsi',
					opsi: ['Ok, mulai sekarang'],
				})

				this.step	= 4

			}else if(this.step===4){
				
				this.handelKirimPesanDelay(1000, {
					saya: false,
					pesan: "Sebelumnya nazmi mau informasikan, <br/> <br/> Kakak akan mendapatkan challenge menghafal 10 ayat per hari, lalu diulang-ulang di dalam shalat 5 waktu yaaa",
					mode: 'opsi',
					opsi: ['Ok 😊, mulai'],
				})

				localStorage.setItem('userNama', this.userNama)
				this.fab	= false
				this.step	= 5

			}else if(this.step===5){
				
				this.fab	= false

			}

		},

		handelLoadDataSurat: async function(){
			this.surat 	= (await this.$axios.$get(`${window.location.origin}/surat.json`)).reverse()
		},

		handelMasukSurat: function(item){
			if(item.tersedia){
				this.$router.push(`/surat/${item.id}`)
			}else{
				this.alertKunci	= true
			}
		}
	},
	
}
</script>

<style scoped>
.card-chat{
	height:70vh;
	display:none
}
.card-chat-percakapan{
	overflow:auto;
}

/* total width */
html::-webkit-scrollbar, .card-chat-percakapan::-webkit-scrollbar{
    background-color: #fff !important;
    width: 16px !important;
}

/* background of the scrollbar except button or resizer */
html::-webkit-scrollbar-track, .card-chat-percakapan::-webkit-scrollbar-track {
    background-color: #fff !important;
}

/* scrollbar itself */
html::-webkit-scrollbar-thumb, .card-chat-percakapan::-webkit-scrollbar-thumb{
    background-color: #babac0 !important;
    border-radius: 16px !important;
    border: 4px solid #fff !important;
}

/* set button(top and bottom of the scrollbar) */
html::-webkit-scrollbar-button, .card-chat-percakapan::-webkit-scrollbar-button::-webkit-scrollbar-button{
    display:none !important;
}

</style>
