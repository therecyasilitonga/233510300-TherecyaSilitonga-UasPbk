<template>
  <div class="register-page">
    <div class="register-card bounce-in">
      <h1>Daftar</h1>
      <form @submit.prevent="register">
        <input v-model="username" type="text" placeholder="Username" required />
        <input v-model="password" type="password" placeholder="Password" required />
        <input v-model="confirmPassword" type="password" placeholder="Konfirmasi Password" required />
        <button type="submit" class="glow-button">Daftar</button>
      </form>
      <p v-if="error" class="error shake">{{ error }}</p>
      <p class="login-text">
        Sudah punya akun?
        <router-link to="/login" class="login-link">Login</router-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      confirmPassword: '',
      error: ''
    };
  },
  methods: {
    register() {
      if (this.password !== this.confirmPassword) {
        this.error = 'Konfirmasi password tidak cocok.';
        return;
      }

      // Simpan data ke localStorage
      const userData = {
        username: this.username,
        password: this.password
      };
      localStorage.setItem('user', JSON.stringify(userData));

      alert('Pendaftaran berhasil! Silakan login.');
      this.$router.push('/login');
    }
  }
};
</script>


<style scoped>
.register-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #064e3b, #065f46);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Inter', sans-serif;
}

.register-card {
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(18px);
  padding: 2.5rem 2rem;
  border-radius: 24px;
  max-width: 400px;
  width: 100%;
  text-align: center;
  color: #d1fae5;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
  animation: fadeInUp 0.8s ease;
}

@keyframes fadeInUp {
  0% {
    opacity: 0;
    transform: translateY(30px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

input {
  width: 100%;
  padding: 0.9rem;
  margin-bottom: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.12);
  color: #ecfdf5;
  font-size: 1rem;
  transition: all 0.3s ease;
}

input:focus {
  outline: none;
  background-color: rgba(255, 255, 255, 0.22);
  box-shadow: 0 0 12px rgba(34, 197, 94, 0.5);
  transform: scale(1.03);
}

input::placeholder {
  color: #bbf7d0;
}

.glow-button {
  width: 100%;
  padding: 0.85rem;
  background: linear-gradient(135deg, #10b981, #059669);
  color: white;
  border: none;
  border-radius: 16px;
  font-size: 1.05rem;
  font-weight: 600;
  cursor: pointer;
  box-shadow: 0 8px 22px rgba(16, 185, 129, 0.4);
  transition: all 0.3s ease;
}

.glow-button:hover {
  background: linear-gradient(135deg, #059669, #047857);
  box-shadow: 0 12px 28px rgba(5, 150, 105, 0.5);
  transform: translateY(-2px);
}

.error {
  color: #f87171;
  margin-top: 1rem;
  font-weight: 500;
  animation: shake 0.4s ease;
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  20%, 60% { transform: translateX(-5px); }
  40%, 80% { transform: translateX(5px); }
}

.login-text {
  margin-top: 1.25rem;
  font-size: 0.95rem;
  color: #bbf7d0;
}

.login-link {
  color: #6ee7b7;
  text-decoration: underline;
  margin-left: 0.25rem;
  font-weight: 500;
  transition: color 0.3s ease;
}

.login-link:hover {
  color: #a7f3d0;
}
</style>
