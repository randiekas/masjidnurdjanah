<template>
<v-app light>
	<v-bottom-navigation fixed>
		<v-btn to="/">
			<span>Beranda</span>
			<v-icon>mdi-square-rounded-badge-outline</v-icon>
		</v-btn>

		<v-btn to="/program">
			<span>Program</span>
			<v-icon>mdi-star-outline</v-icon>
		</v-btn>
		
		<v-btn to="/hafalan">
			<span>Hafalan</span>
			<v-icon>mdi-book-open-outline</v-icon>
		</v-btn>

		

		<v-btn 
			to="/todo"
			value="nearby">
			<span>Todo</span>

			<v-icon>mdi-check-circle-outline</v-icon>
		</v-btn>

		<v-btn 
			to="/info"
			value="nearby">
			<span>Info</span>

			<v-icon>mdi-information-outline</v-icon>
		</v-btn>

	</v-bottom-navigation>
	<v-main>
		<div>
			<nuxt-child
				:handelSetAudioParent="handelSetAudioParent"/>
		</div>
	</v-main>
</v-app>
</template>

<script>
export default {
	data () {
			return {
				audio: false,
			}
	},
	methods:{
		handelSetAudioParent: function(audio){
			this.audio	= audio
		}
	},
	watch:{
		$route:function({ name }){
			if(name!='surat-id' && this.audio){
				this.audio.pause()
			}
		}
	}
}
</script>
<style scoped>
.page-mobile{
	width: 100%;
    max-width: 480px;
    margin: 0 auto;
    background-color: #f5f5f5;
    height: 100%;
    min-height: 100vh;
    padding-bottom: 40px;
    position: relative;
}
.v-btn--active{
	color: #796EF9 !important;
	background: #C6E6FF!important;
}
</style>