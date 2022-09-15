<template>
    <div>
        <v-card dark color="primary" style="height:200px" rounded="0">

	</v-card>
	<v-container style="margin-top:-180px; height:95vh" class="primary accent2">
		<v-card flat color="transparent">
			<h1 class="white--text text-h4">Program</h1>
			<p class="white--text">Berikut program program Masjid Nurdjanah</p>
		</v-card>
		<v-card>
			<p class="mb-0 px-4 py-2"><b>Program Berjalan</b></p>
			<v-divider/>
			<v-card-text>
				<v-card 
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
			</v-card-text>
		</v-card>
	<v-row>
		<v-col cols="12">
		</v-col>

		<v-col cols="12">
			<p class="text-overline mb-0 d-flex" style="align-items:center">
				Semua Program
			</p>
			<v-card 
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
 
		
	</v-row>
	</v-container>
    </div>
</template>