<template>
<div>
	<v-dialog
        v-model="alertKunci"
        persistent
        max-width="300">
        <v-alert
            border="left"
            color="deep-purple accent-4"
            type="info"
            dark>
                Maaf, untuk sementara ayat ini masih dikunci
				<v-btn class="mt-4" block v-on:click="alertKunci=false">Tutup</v-btn>
        </v-alert>
    </v-dialog>
	<v-card dark color="primary" style="height:200px" rounded="0">

	</v-card>
	<v-container style="margin-top:-180px;" class="primary accent2 pb-16">
		<v-card flat color="transparent">
			<h1 class="white--text text-h4">Masjid Nurdjannah</h1>
			<p class="white--text">Layanan digital mesjid nurdjannah SSP salt river</p>
		</v-card>
		<v-card rounded="lg">
			<p class="mb-0 px-4 py-2"><b>Senin, 20 September</b></p>
			<v-divider/>
			<v-card-text class="d-flex align-center">
				<v-row dense>
					<v-col 
						v-for="(item, index) in adzan"
						:key="`item-${index}`"
						class="text-center">
						<v-icon class="success--text">mdi-check-decagram</v-icon><br/>
						<b class="black--text">{{item.nama}}</b> <br/>
						{{item.waktu}}
					</v-col>
				</v-row>
			</v-card-text>
		</v-card>
	<v-row>
		<v-col cols="12">
			<p class="text-overline mb-0 d-flex mt-4" style="align-items:center">
				Kajian Rutin <v-spacer/><v-chip x-small dark class="red">Terbaru</v-chip>
			</p>
			<v-slide-group
				class="">
				<v-slide-item
					v-for="n in 3"
					:key="n">
					<v-card rounded="lg" class="mr-2" to="/kajian/1.png" target="_blank">
						<v-img src="/kajian/1.png" width="200"/>
					</v-card>
				</v-slide-item>
				</v-slide-group>
		</v-col>

		<v-col cols="12">
			<p class="text-overline mb-0 d-flex" style="align-items:center">
				Program Berjalan
			</p>
			<v-card 
				rounded="lg"
				dark 
				color="primary"
				:to="`/program/1`"
				hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-star-check</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Yasinan</v-list-item-title>
						<v-list-item-subtitle>Yasinan setiap malam jumat</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card>
			<v-card 
				rounded="lg"
				class="mt-2"
				dark 
				color="primary"
				:to="`/program/1`"
				hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-star-check</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Pengajian Rutin</v-list-item-title>
						<v-list-item-subtitle>Pengajian rutin 1 bulan sekali</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card>
		</v-col>

		<v-col cols="12">
			<p class="text-overline mb-0 d-flex" style="align-items:center">
				Berita terkini
			</p>
			<v-card 
				rounded="lg"
				dark 
				color="primary"
				:to="`/program/1`"
				hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-avatar>
						 	<img
								src="https://cdn-icons-png.flaticon.com/512/337/337302.png"
								alt="John">
						</v-avatar>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Peresmian DKM Masjid Nurdjanah</v-list-item-title>
						<v-list-item-subtitle>29 September 2022</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-icon>
						<v-icon>mdi-chevron-right</v-icon>
					</v-list-item-icon>
				</v-list-item>
			</v-card>
		</v-col>

		
		
	</v-row>
	</v-container>
	
	<v-dialog
		v-model="fab"
		persistent
		max-width="480">
	<v-card 
		v-if="fab"
		class="card-chat d-flex flex-column justify-content-between"
		flat
		dark
		color="primary">
		<div>
			<v-toolbar color="primary">
				<v-toolbar-title>Onboarding</v-toolbar-title>
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
				@click:append="handelKirimPesan"
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
	<v-dialog
		v-model="fabKeutamaanMenghafalAlquran"
		persistent
		max-width="480">
		<v-carousel 
			height="auto">
			<v-carousel-item>
				<v-card rounded="lg">
					<v-img 
						src="/keutamaan-1.jpeg"/>
				</v-card>
			</v-carousel-item>
			<v-carousel-item>
				<v-card rounded="lg">
					<v-img 
						src="/keutamaan-2.jpeg"/>
				</v-card>
			</v-carousel-item>
		</v-carousel>
	
		<v-btn
			block
			dark
			color="primary"
			v-on:click="fabKeutamaanMenghafalAlquran=false">
			Tutup
		</v-btn>
	</v-dialog>
</div>
</template>
<script>
export default {
	asyncData: async function({ query }){
		
		let userNama	= localStorage.getItem('userNama')
		let step		= userNama?2:1;

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
			fabKeutamaanMenghafalAlquran: false,
			e6: 1,
			suratDipilih: 1,
			youtubeUrl: '',
			adzan: [
				{ nama: 'Subuh', waktu: '04:00'},
				{ nama: 'Dzuhur', waktu: '12:00'},
				{ nama: 'Ashar', waktu: '15:00'},
				{ nama: 'Magrib', waktu: '18:00'},
				{ nama: 'Isya', waktu: '19:00'},
			],
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
		let mode		= 'opsi'
		let opsi		= ["Ok, saya mengerti 😊"]
		if(this.step===1){
			percakapan = [
				'Assalamualaykum ... 😊',
				'Selamat datang di layanan digital masjidnurdjanah',
				"Apa saja fitur yang disediakan ? <br/><br/> 1. Informasi Keuangan<br/>2. Agenda Masjid<br/>3. Jadwal Adzan<br/>4. Hafalan Quran, <br/>4. Todo Muslim",
			]


			percakapan.map((item)=>{
				this.handelKirimPesanDelay(delay, {
					saya: false,
					pesan: item,
					mode: mode,
					opsi: opsi,
				})
				delay	+= 1000
			})
		}else{
			this.fab	= false
		}

		
		
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
			this.fab			= false
			this.step			= 2
			// if(this.step===1){
			// 	this.userNama	= pesan
			// 	localStorage.setItem('userNama', this.userNama)
			// 	this.fab		= false
			// 	this.step		= 2

			// }else if(this.step===2){
			// 	this.fab	= false
			// }

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
