<template>
    <div>
        <v-card dark color="primary" style="height:200px" rounded="0">

	</v-card>
	<v-container style="margin-top:-180px; height:100vh" class="primary accent2 pb-16">
		<v-card flat color="transparent">
			<h1 class="white--text text-h4">Masjid Nurdjanah</h1>
			<p class="white--text">Jl. Ciuyah No.50, Padaasih, Kec. Cisarua, Kabupaten Bandung Barat, Jawa Barat 40551</p>
		</v-card>
        <v-card>
            <v-card>
                <v-list-item
                    to="/info/keuangan">
                    <v-list-item-avatar>
                        <v-icon>mdi-cash-sync</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title>Keuangan</v-list-item-title>
                        <v-list-item-subtitle>Laporan Keuangan</v-list-item-subtitle>
                    </v-list-item-content>
                    <v-list-item-action-text>
                        <v-icon>mdi-chevron-right</v-icon>
                    </v-list-item-action-text>
                </v-list-item>
                <v-divider/>
                <v-list-item
                    to="/info/dkm">
                    <v-list-item-avatar>
                        <v-icon>mdi-account-group</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title>DKM</v-list-item-title>
                        <v-list-item-subtitle>List anggota DKM</v-list-item-subtitle>
                    </v-list-item-content>
                    <v-list-item-action-text>
                        <v-icon>mdi-chevron-right</v-icon>
                    </v-list-item-action-text>
                </v-list-item>
            </v-card>
        </v-card>
	    <v-row>
		
            <!-- <v-col cols="12">
                <p class="text-overline mb-0 d-flex mt-4" style="align-items:center">
                    Lokasi
                </p>

                <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3961.329340810223!2d107.55907511530022!3d-6.851067968929867!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e68e5bfdb2f8b05%3A0x44d9c34c1116bfe5!2sSSP%20Salt%20River!5e0!3m2!1sen!2sid!4v1662942370739!5m2!1sen!2sid" width="100%" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                <v-btn 
                    href="https://g.page/Sspsalt river?share"
                    target="_blank"
                    block>
                    <v-icon left>mdi-google-maps</v-icon>
                    Buka Maps
                </v-btn>
                -->

            
            </v-col>
    
            
        </v-row>
	</v-container>
    </div>
</template>