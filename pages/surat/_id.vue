<template>
    <div class="pb-12">
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
        <v-card dark color="primary" class="pb-5 pt-5">
            <v-card-title class="justify-center text-center">
                {{ detil.detil.surat_terjemahan }}
            </v-card-title>
            <v-card-subtitle class="text-center">{{ detil.detil.count_ayat }} Ayat</v-card-subtitle>
        </v-card>
        <v-stepper
            v-model="step"
            vertical
            editable>
            <template v-for="(item, index) in detil.step">
                <v-stepper-step
                    :key="`header-${index}`"
                    :complete="index+1<step"
                    :step="index+1">
                    {{ item.deskripsi }}
                    <small>Ulangi sebanyak 20x</small>
                </v-stepper-step>
                <v-stepper-content 
                    :key="index"
                    :step="index+1">
                    
                    <v-card
                        color="grey lighten-3"
                        class="mb-4">
                        <v-card-text>
                            <div v-for="(row, key) in item.ayat" :key="key">
                                <v-list-item dense>
                                    <v-list-item-content>
                                        <h2 class="text-h5 text-right"><small><v-avatar
                                            size="16"
                                            style="font-size:8px"
                                            color="teal lighten-1"
                                            class="white--text">
                                            {{ row }}
                                        </v-avatar></small>
                                        {{ detil.ayat[row-1] && detil.ayat[row-1].aya_text }} </h2>
                                    </v-list-item-content>
                                </v-list-item>
                                <v-divider
                                    v-if="key<item.ayat.length-1"/>
                            </div>
                        </v-card-text>
                    </v-card>
                    <v-card outlined flat class="mt-n5">
                        <v-list-item 
                            dense
                            v-if="mulai"
                            v-on:click="handelPause()">
                            <v-list-item-avatar>
                                <v-icon>mdi-pause</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Pause audio
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-list-item 
                            dense
                            v-else
                            v-on:click="handelMulai()">
                            <v-list-item-avatar>
                                <v-icon>mdi-play</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Mulai sesi hafalan
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-divider/>
                        <v-list-item dense>
                            <v-list-item-avatar>
                                <v-icon>mdi-repeat-once</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Pengulangan ke 
                                </v-list-item-title>
                            </v-list-item-content>
                            <v-list-item-action-text>
                                <v-avatar
                                    size="24"
                                    color="teal lighten-1"
                                    class="white--text">
                                    {{ ke }}
                                </v-avatar>
                            </v-list-item-action-text>
                        </v-list-item>
                        <v-divider/>
                        <v-list-item 
                            dense
                            v-on:click="ke=1;handelReset()">
                            <v-list-item-avatar>
                                <v-icon>mdi-repeat</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Ulangi sesi ini
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-divider/>
                        <v-list-item 
                            v-if="step<detil.step.length"
                            dense
                            v-on:click="handelStepBerikutnya()">
                            <v-list-item-avatar>
                                <v-icon>mdi-check-decagram</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Sudah hafal, masuk ke sesi berikutnya
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                        <v-list-item 
                            v-else
                            dense
                            to="/?kembali=true">
                            <v-list-item-avatar>
                                <v-icon>mdi-check-decagram</v-icon>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title>
                                    Sudah hafal semua, pilih surat lain
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                    
                </v-stepper-content>
            </template>  

        </v-stepper>
    </div>
</template>
<script>
export default {

    props:['handelSetAudioParent'],
    asyncData: async function({ $axios, params }){
        const suratke   = params.id
        const detil     = await $axios.$get(`${window.location.origin}/surat/${suratke}.json`)
        return {
            suratke, 
            ke:1,
            detil,
            step: 1,
            mulai:false,
            audio: [],
            audioSekarang: false
        }
    },
    mounted: function(){
        this.handelSetAudio()
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