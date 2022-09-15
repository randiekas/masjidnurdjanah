<template>
    <div>
        <v-card dark color="primary" style="height:200px" rounded="0">

	</v-card>
	<v-container style="margin-top:-180px;" class="primary accent2 pb-16">
		<v-card flat color="transparent">
			<h1 class="white--text text-h4">Todo</h1>
			<p class="white--text">Challenge mengikuti todo muslim, dan rasakan perubahanya dalam 40 hari.</p>
		</v-card>
        <v-alert class="primary accent">
            Disclaimer<br/>
            <small>Dengan fitur todo ini, bukan maksud kami untuk menggurui. todo ini adalah ajakan kebaikan semata</small>
        </v-alert>
	<v-row>
		
		<v-col cols="12">
			<p class="text-overline mb-0 d-flex" style="align-items:center">
				Rutin Pagi
			</p>
			<v-card 
				rounded="lg"
				dark 
				color="primary"
                hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-check-decagram</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Bagun Pagi</v-list-item-title>
						<v-list-item-subtitle>Bangun pagi dibawah jam 10 sangatlah baik</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
                        04:30
                    </v-list-item-action-text>
				</v-list-item>
                <v-divider/>
                <v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-checkbox-blank-circle-outline</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Mandi Subuh</v-list-item-title>
						<v-list-item-subtitle>Mandi sebelum shalat subuh sangatlah dianjurkan</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
                        05:30
                    </v-list-item-action-text>
				</v-list-item>
                <v-divider/>
                <v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-checkbox-blank-circle-outline</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Membaca Ayat Al-Quran</v-list-item-title>
						<v-list-item-subtitle>Membaca Surat Al-quran</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
                        06:30
                    </v-list-item-action-text>
				</v-list-item>
			</v-card>

            <p class="text-overline mb-0 d-flex mt-4" style="align-items:center">
				Rutin Tambahan
			</p>
			<v-card 
				rounded="lg"
				dark 
				color="primary"
                hover>
				<v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-check-decagram</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>Bersedekah</v-list-item-title>
						<v-list-item-subtitle>Bersedekah rutin harian</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
                        04:30
                    </v-list-item-action-text>
				</v-list-item>
                <v-divider/>
                <v-list-item>
					<v-list-item-avatar>
						<v-icon>mdi-checkbox-blank-circle-outline</v-icon>
					</v-list-item-avatar>
					<v-list-item-content>
						<v-list-item-title>3S</v-list-item-title>
						<v-list-item-subtitle>Saling Sapa Senyum kepada umum</v-list-item-subtitle>
					</v-list-item-content>
					<v-list-item-action-text>
                        05:30
                    </v-list-item-action-text>
				</v-list-item>
               
			</v-card>
		
		</v-col>
 
		
	</v-row>
	</v-container>
    </div>
</template>