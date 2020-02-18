<template>
  <div class="container">
    <div class = "form_dropdown">
      <h2>Masukkan Alamat Pribadi Anda</h2>
      <input type="text" placeholder="Nama" v-model="iNama"/>
      <br>
      <textarea v-model="textAlamat" placeholder="Alamat"></textarea>
      <br>
      <select class="drop-item" v-model="pilih_provinsi">
          <option value="">-- Pilih Provinsi --</option>
          <option v-for="(index, province) in data_lokasi" :value="province" :key="index">
            {{ province }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kota" :disabled="kota.length == 0">
          <option value="">-- Pilih Kabupaten / Kota --</option>
          <option v-for="(index, city) in kota" :value="city" :key="index">
            {{ city }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kecamatan" :disabled="kecamatan.length == 0">
          <option value="">-- Pilih Kecamatan --</option>
          <option v-for="kec in kecamatan" :value="kec" :key="kec">{{ kec }}</option>
      </select>
      <p>Your result will be automatically shown at the card below</p>
    </div>
    <div class = "hasil">
      <h3>Preview Alamat</h3>
      <p v-if="pilih_provinsi&&pilih_kota&&pilih_kecamatan">
          Nama {{iNama}}, Alamat {{textAlamat}},
          Kecamatan {{ pilih_kecamatan }}, {{ pilih_kota }}, Provinsi {{ pilih_provinsi }}
          <br /><br />
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    iNama: '',
    textAlamat:'',
    kota: [],
    kecamatan: [],
    pilih_provinsi: '',
    pilih_kota: '',
    pilih_kecamatan: '',
    data_lokasi: {
      'Bali': {
        'Kabupaten Badung':['Abiansemal', 'Kuta', 'Mengwi', 'Petang'],
        'Kabupaten Buleleng':['Banjar', 'Gerokgak', 'Sawan', 'Tejakula'],
        'Kabupaten Gianyar':['Blahbatu', 'Gianyar', 'Sukawati', 'Tampaksiring', 'Ubud'],
        'Kabupaten Tabanan':['Baturiti', 'Kediri', 'Marga', 'Penebel', 'Tabanan'],
        'Kota Denpasar':['Denpasar Barat', 'Denpasar Timur', 'Denpasar Selatan', 'Denpasar Utara'],
      },
      'Banten ': {
        'Kota Tangerang': ['Benda', 'Cibodas', 'Ciledug'],
        'Kota Cilegon': ['Cibeber', 'Cilegon', 'Citangkil'],
        'Kota Serang': ['Cipocok Jaya', 'Curug', 'Kasemen'],
        'Kabupaten Pandeglang': ['Cadasari', 'Kaduhejo', 'Mandalawangi'],
      },
      'Daerah Khusus Ibukota Jakarta': {
        'Kota Jakarta Utara': ['Tanjung Priok', 'Kelapa Gading', 'Penjaringan'],
        'Kota Jakarta Timur': ['Cakung', 'Jatinegara', 'Kramat Jati'],
        'Kota Jakarta Barat': ['Cengkareng', 'Kebon Jeruk', 'Kalideres'],
        'Kota Jakarta Selatan': ['Kebayoran Baru', 'Mampang Prapatan', 'Setiabudi'],
      },
      'Jawa Barat': {
        'Kota Bandung': ['Buahbatu', 'Gedebage', 'Sukajadi'],
        'Kota Cirebon': ['Harjamukti', 'Kejaksan', 'Pekalipan'],
        'Kota Bogor': ['Bogor Barat', 'Bogor Selatan', 'Bogor Utara'],
        'Kota Tasikmalaya': ['Cibeureum', 'Cipedes', 'Indihiang'],
        'Kabupaten Purwakarta': ['Bojong', 'Cibatu', 'Jatiluhur', 'Kiarapedes'],
        'Kabupaten Tasikmalaya': ['Bojongasih', 'Ciawi', 'Jamanis', 'Kadipaten'],
      },
      'Daerah Istimewa Yogyakarta': {
        'Kota Yogyakarta': ['Gondokusuman', 'Kotagede', 'Pakualaman'],
        'Kabupaten Sleman': ['Kalasan', 'Prambanan', 'Sleman'],
        'Kabupaten Bantul': ['Imogiri', 'Pajangan', 'Sedayu'],
        'Kabupaten Gunung Kidul': ['Karangmojo', 'Purwosari', 'Wonosari'],
        'Kabupaten Kulon Progo': ['Galur', 'Kalibawang', 'Pengasih', 'Wates'],
      },
      'Jawa Tengah': {
        'Kabupaten Banjarnegara': ['Banjarmangu', 'Batur', 'Kalibening'],
        'Kota Semarang': ['Gajahmungkur', 'Semarang Timur', 'Tembalang'],
        'Kota Surakarta': ['Banjarsari', 'Jebres', 'Pasar Kliwon'],
        'Kabupaten Sragen': ['Kedawung', 'Miri', 'Sambirejo'],
        'Kabupaten Purbalingga': ['Bobotsari', 'Karanganyar', 'Rembang'],
        'Kabupaten Tegal': ['Adiwerna', 'Bumijawa', 'Kramat', 'Warureja'],
      },
      'Jawa Timur': {
        'Kota Surabaya': ['Gubeng', 'Rungkut', 'Wiyung'],
        'Kota Malang': ['Blimbing', 'Kedungkandang', 'Klojen', 'Lowokwaru', 'Sukun'],
        'Kabupaten Malang': ['Ampelgading', 'Bululawang', 'Dampit', 'Kepanjen', 'Karangploso'],
        'Kabupaten Mojokerto': ['Bangsal', 'Kutorejo', 'Mojosari', 'Pacet', 'Pungging'],
        'Kabupaten Nganjuk': ['Bagor', 'Baron', 'Berbek'],
        'Kabupaten Sidoarjo': ['Balongbendo', 'Buduran', 'Candi', 'Krembung'],
        'Kabupaten Tulungagung' : ['Boyolangu', 'Gondang', 'Kedungwaru', 'Ngunut'],
      },
      'Papua': {
        'Kabupaten Asmat': ['Agast', 'Atsj', 'Suru-suru', 'Joerat'],
        'Kabupaten Jayapura':['Sentani', 'Depapre', 'Waibu', 'Yapsi'],
        'Kabupaten Merauke':['Merauke', 'Okaba', 'Ulilin', 'Tabonji'],
        'Kota Jayapura':['Jayapura Utara', 'Jayapura Selatan', 'Abepura', 'Muara Tami', 'Heram'],
      },
    },
  }),
  watch: {
    iNama() {
      return
    },
    textAlamat() {
      return
    },
    pilih_provinsi() {
      this.kota = [];
      this.kecamatan = [];
      this.pilih_kota = '';
      this.pilih_kecamatan = '';
      if (this.pilih_provinsi.length > 0) {
        this.kota = this.data_lokasi[this.pilih_provinsi];
      }
    },
    pilih_kota() {
      this.kecamatan = [];
      this.pilih_kecamatan = '';
      if (this.pilih_kota.length > 0) {
        this.kecamatan = this.data_lokasi[this.pilih_provinsi][this.pilih_kota];
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin: 50px;
}
.form_dropdown {
  padding: 20px;
  width: 700px;
  margin-bottom: 10px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  border-radius: 5px;
  text-align: center;
  background-color: #f5f5f5;
  margin-left: auto;
  margin-right: auto;
}
.hasil {
  width: 700px;
  padding: 20px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  border-radius: 5px;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}
.drop-item {
  width: 600px;
  margin: 10px;
  padding: 10px;
}
input{
  width: 580px;
  margin: 10px;
  padding: 10px
}
textarea{
  width: 580px;
  margin: 10px;
  padding: 10px
}
</style>