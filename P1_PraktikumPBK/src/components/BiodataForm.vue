<template>
  <div class="container">
    <div class="header">
      <h1>📚 Form Biodata Mahasiswa</h1>
      <p>Silakan lengkapi data diri Anda dengan benar</p>
    </div>
    
    <div class="form-container">
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="nama">Nama Lengkap *</label>
          <input 
            type="text" 
            id="nama" 
            v-model="formData.nama"
            placeholder="Masukkan nama lengkap Anda"
            required
          >
        </div>

        <div class="form-row">
          <div class="form-group">
            <label for="tanggalLahir">Tanggal Lahir *</label>
            <input 
              type="date" 
              id="tanggalLahir" 
              v-model="formData.tanggalLahir"
              required
            >
          </div>
          
          <div class="form-group">
            <label for="tempatLahir">Tempat Lahir *</label>
            <input 
              type="text" 
              id="tempatLahir" 
              v-model="formData.tempatLahir"
              placeholder="Kota tempat lahir"
              required
            >
          </div>
        </div>

        <div class="form-group">
          <label for="tempatTinggal">Tempat Tinggal Saat Ini *</label>
          <textarea 
            id="tempatTinggal" 
            v-model="formData.tempatTinggal"
            placeholder="Alamat lengkap tempat tinggal saat ini"
            required
          ></textarea>
        </div>

        <div class="form-group">
          <label for="universitas">Universitas *</label>
          <input 
            type="text" 
            id="universitas" 
            v-model="formData.universitas"
            placeholder="Nama universitas"
            required
          >
        </div>

        <div class="form-row">
          <div class="form-group">
            <label for="jurusan">Jurusan *</label>
            <input 
              type="text" 
              id="jurusan" 
              v-model="formData.jurusan"
              placeholder="Nama jurusan"
              required
            >
          </div>
          
          <div class="form-group">
            <label for="programStudi">Program Studi *</label>
            <input 
              type="text" 
              id="programStudi" 
              v-model="formData.programStudi"
              placeholder="Nama program studi (contoh: Teknik Informatika)"
              required
            >
          </div>
        </div>

        <div class="form-group">
          <label for="alasanMasuk">Alasan Masuk Jurusan Tersebut *</label>
          <textarea 
            id="alasanMasuk" 
            v-model="formData.alasanMasuk"
            placeholder="Ceritakan alasan Anda memilih jurusan ini..."
            required
          ></textarea>
        </div>

        <button type="submit" class="submit-btn">
          🚀 Simpan Data
        </button>
      </form>

      <Transition name="fade">
        <div v-if="showResult" class="result-card">
          <h3>📋 Data yang Tersimpan:</h3>
          <div class="result-item">
            <span class="result-label">Nama Lengkap:</span>
            <span class="result-value">{{ submittedData.nama }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Tempat, Tanggal Lahir:</span>
            <span class="result-value">{{ submittedData.tempatLahir }}, {{ formatDate(submittedData.tanggalLahir) }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Tempat Tinggal:</span>
            <span class="result-value">{{ submittedData.tempatTinggal }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Universitas:</span>
            <span class="result-value">{{ submittedData.universitas }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Jurusan:</span>
            <span class="result-value">{{ submittedData.jurusan }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Program Studi:</span>
            <span class="result-value">{{ submittedData.programStudi }}</span>
          </div>
          <div class="result-item">
            <span class="result-label">Alasan Masuk:</span>
            <span class="result-value">{{ submittedData.alasanMasuk }}</span>
          </div>
        </div>
      </Transition>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BiodataForm',
  data() {
    return {
      formData: {
        nama: 'Jasmine Aisha Melindra Fitri',
        tanggalLahir: '2005-08-12',
        tempatLahir: 'Pekanbaru',
        tempatTinggal: 'Jl. Ayu Sari No.1A',
        universitas: 'Universitas Islam Riau',
        jurusan: 'Teknik',
        programStudi: 'Teknik Informatika',
        alasanMasuk: 'Karena pilihan terakhir, awalnya saya memilih dokter tapi tidak lulus, makanya sekarang milih IT saja'
      },
      submittedData: {},
      showResult: false
    }
  },
  methods: {
    submitForm() {
      // Copy data form ke submittedData
      this.submittedData = { ...this.formData };
      this.showResult = true;
      
      // Scroll ke hasil
      this.$nextTick(() => {
        const resultCard = this.$el.querySelector('.result-card');
        if (resultCard) {
          resultCard.scrollIntoView({ 
            behavior: 'smooth',
            block: 'start'
          });
        }
      });
    },
    formatDate(dateString) {
      if (!dateString) return '';
      
      const date = new Date(dateString);
      const options = { 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric' 
      };
      
      return date.toLocaleDateString('id-ID', options);
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.header {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  color: white;
  text-align: center;
  padding: 30px;
}

.header h1 {
  font-size: 2.5rem;
  margin-bottom: 10px;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.header p {
  font-size: 1.1rem;
  opacity: 0.9;
}

.form-container {
  padding: 40px;
}

.form-group {
  margin-bottom: 25px;
  position: relative;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #333;
  font-size: 1rem;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 12px 15px;
  border: 2px solid #e1e5e9;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: #f8f9fa;
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  outline: none;
  border-color: #4facfe;
  background: white;
  box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
  transform: translateY(-2px);
}

.form-group textarea {
  min-height: 120px;
  resize: vertical;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.submit-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 15px 40px;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  width: 100%;
  margin-top: 20px;
}

.submit-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);
}

.submit-btn:active {
  transform: translateY(-1px);
}

.result-card {
  background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
  border-radius: 15px;
  padding: 25px;
  margin-top: 30px;
  border-left: 5px solid #ff6b6b;
}

.result-card h3 {
  color: #333;
  margin-bottom: 20px;
  font-size: 1.5rem;
}

.result-item {
  display: flex;
  margin-bottom: 12px;
  padding: 8px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}

.result-item:last-child {
  border-bottom: none;
}

.result-label {
  font-weight: 600;
  color: #555;
  min-width: 180px;
}

.result-value {
  color: #333;
  flex: 1;
}

@media (max-width: 768px) {
  .form-row {
    grid-template-columns: 1fr;
  }
  
  .header h1 {
    font-size: 2rem;
  }
  
  .form-container {
    padding: 20px;
  }
  
  .result-item {
    flex-direction: column;
  }
  
  .result-label {
    min-width: auto;
    margin-bottom: 5px;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>