<template>
    <div>
        <v-toolbar>
            <v-btn 
                icon
                to="/?kembali=true">
                <v-icon>
                    mdi-chevron-left
                </v-icon>
            </v-btn>
            <v-toolbar-title>{{ detil.detil.surat_name }}</v-toolbar-title>
        </v-toolbar>
        <v-card dark color="primary">
            <iframe 
                src="https://www.youtube.com/embed/S5cu2LGZIkM?autoplay=1&mute=1"
                style="border:none; width:100%; height:56vh"/>
        </v-card>
        
        <v-card 
            dark 
            color="primary" >
            <template
                v-for="(item, index) in detil.step">

                <v-list-item
                    :key="`header-${index}`"
                    v-on:click="step=index+1;handelReset();handelSetAudio();handelMulai()">
                    <v-list-item-avatar>
                        <v-avatar
                            color="teal darken-4">
                            {{ index+1 }}
                        </v-avatar>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title>{{ item.deskripsi }}</v-list-item-title>
                    </v-list-item-content>
                    <v-list-item-action-text v-if="index==step">
                        Playing
                    </v-list-item-action-text>
                    <v-list-item-icon>
                        <v-icon>mdi-chevron-right</v-icon>
                    </v-list-item-icon>
                </v-list-item>
                <v-divider :key="`divider-${index}`"/>
            </template>
        </v-card>
        
    </div>
</template>
<script>
export default {

    props:['handelSetAudioParent'],
    asyncData: async function({ $axios, params, query }){
        const suratke   = params.id
        console.log(query)
        const detil     = await $axios.$get(`${window.location.origin}/surat/${suratke}.json`)
        return {
            suratke, 
            ke:1,
            detil,
            step: 1,
            mulai:false,
            audio: [],
            audioSekarang: false,
            url: query.url      
        }
    },
    mounted: function(){
        this.handelSetAudio()
        this.handelMulai()
    },
    methods:{
        handelMulai: function(){
            this.mulai          = true;
            this.audioSekarang.play()
            localStorage.setItem('ayatTarget', JSON.stringify(this.detil.detil))
            // var audio = new Audio('/audio/001002.mp3'); // path to file
            // await audio.play();
            
        },
        handelPause: function(){
            this.mulai          = false;
            this.audioSekarang.pause()
        },
        handelReset: function(){
            this.handelPause()
            this.audioSekarang              = this.audio[0]
            this.audioSekarang.currentTime  = 0;
        },
        handelStepBerikutnya: function(){
            this.handelReset()
            this.step   +=1
            this.handelSetAudio()
            this.ke                     = 0;
        },
        handelSetAudio: function(){
            let audio                   = []
            this.detil.step[this.step-1].ayat.map((item, index)=>{
                const audioname           = ('00' + this.suratke).slice(-3)+('00' + item).slice(-3)
                // audio[index]            = new Audio(`${window.location.origin}/audio/${audioname}.mp3`); // path to file
                audio[index]            = new Audio(`https://audio.qurancdn.com/Alafasy/mp3/${audioname}.mp3`); // path to file
                audio[index].onplay     = ()=>{
                    this.audioSekarang  = audio[index]
                }
                audio[index].onended    = ()=>{
                    if(index<this.detil.step[this.step-1].ayat.length-1){
                        audio[index+1].play()
                    }else{
                        this.handelReset()
                        if(this.ke<20){
                            this.ke         += 1
                            this.handelMulai()
                        }
                    }
                }
            })
            this.audio                  = audio
            this.audioSekarang          = audio[0]
            this.handelSetAudioParent(audio[0])
        },
        handelSelesai: function(){
            
        }
    },
    watch:{
        $route(){
            this.handelReset()
        }
    }
}
</script>