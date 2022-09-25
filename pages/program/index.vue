<template>
    <div>
	<v-card dark color="primary" style="height:200px" rounded="0">

	</v-card>
	<v-container style="margin-top:-180px; height:100vh" class="primary accent2 pb-16">
		<v-card flat color="transparent">
			<h1 class="white--text text-h4">Program</h1>
			<p class="white--text">Berikut program program Masjid Nurdjanah</p>
		</v-card>
		<v-card rounded="lg">
			<p class="mb-0 px-4 py-2"><b>Program Berjalan</b></p>
			<v-divider/>
			<v-card-text>
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
				class="mt-2 mb-16"
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
	<v-row class="pb-16 mb-16">
		<v-col cols="12">
		</v-col>

		<v-col cols="12">
			<p class="text-overline mb-0 d-flex" style="align-items:center">
				Semua Program
			</p>
			<v-card 
				rounded="lg">
				<v-card-text>
					<p dir="auto">Perumusan Program Kerja :<br>
DKM Nurdjanah sebagai Lembaga yang dipercaya masyarakat untuk memakmurkan Masjid Nurdjanah, memiliki program kerja sebagai berikut :<br>
<br>
1. TAHUNAN<br>
a. Pengelolaan Zakat Mal.<br>
b. Haflah Ramadhan<br>
- Menyediakan tazil/buka puasa<br>
- Shalat Tarawih Berjama&rsquo;ah<br>
- Kultum<br>
- Safari Ramadhan<br>
- Kuliah Subuh<br>
- Tadarus Al-Qur&rsquo;an<br>
- Peringatan Nuzulul Qur&rsquo;an<br>
- I&rsquo;tikaf (malam-malam ganjil di bulan Ramadhan)<br>
c. Kegiatan Idul Fitri<br>
- Pengelolaan Zakat Fitrah<br>
- Takbiran<br>
- Pelaksanaan Sholat Idul Fitri<br>
- Halal Bi Halal<br>
d. Kegaitan Idul Adha<br>
- Takbiran<br>
- Pelaksanaan Sholat Idul Adha<br>
- Pengelolaan Hewan Qurban<br>
e. Pelaksanaa Peringatan Hari Besar Islam lainnya<br>
- Peringatan Tahun Baru Hijriyah<br>
- Peringatan Maulid Nabi Muhammad SAW<br>
- Peringatan Isra Mi&rsquo;raj Nabi Muhammad SAW<br>
- Peringatan Malam Nisfu Sya&rsquo;ban<br>
<br>
2. BULANAN<br>
a. Pengajian Bulanan<br>
b. Bedah Kitab/Sharing Agama (melibatkan DKM/Ulama di lingkungan Ciuyah/Padaasih<br>
<br>
3. MINGGUAN<br>
a. Pelaksanaan Shalat Jum&rsquo;at<br>
b. Penyediaan konsumsi Jum&rsquo;at setelah Sholat Jum&rsquo;at<br>
c. Yasinan<br>
d. Gema Marhaba (Simtuduror/Berjanji/Rawi)<br>
e. Pengajian (ibu-ibu Majelis Ta&rsquo;lim)<br>
f. Pelatihan Qiroat<br>
<br>
4. HARIAN<br>
a. Shalat Fardlu berjama&rsquo;ah<br>
b. Pengajian Al-Qur&rsquo;an<br>
- Iqro<br>
- Juz Amma<br>
- Al-Qur&rsquo;an<br>
- Tadarus Al-Qur&rsquo;an<br>
c. Pendidikan Agama (TPA.sejenisnya)<br>
<br>
5. KEGIATAN INSIDENTAL<br>
a. Silaturahmi antar DKM/Ulama di Lingkungan Cisarua/Padaasih<br>
b. Santunan anak Yatim<br>
c. Pelatihan mengkafani dan memandikan mayit<br>
d. Aplikasi ibadah dalam masyarakat (kebersihan lingkungan, dll)<br>
e. Pemberangkatan ibadah haji/umroh untuk para Ustad/Imam/Marboth/Muadzin (Program Jangka Panjang)</p>
				</v-card-text>
			</v-card>
			 
		</v-col>
 
		
	</v-row>
	</v-container>
    </div>
</template>