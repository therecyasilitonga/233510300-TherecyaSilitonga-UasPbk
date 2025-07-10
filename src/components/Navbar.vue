<template>
  <nav class="navbar">
    <div class="logo">
      <img src="/images/logo.png" alt="Logo" />
      <span>Toko Perabot Nusantara</span>
    </div>
    <div class="nav-links">
      <router-link to="/beranda">Beranda</router-link>
      <router-link to="/produk">Produk</router-link>
      <router-link to="/keranjang">Keranjang</router-link>
      <router-link to="/checkout">Checkout</router-link>
      <button v-if="isLoggedIn" @click="logout">Logout</button>
      <router-link v-else to="/login" class="login-link">Login</router-link>
    </div>
  </nav>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

export default {
  setup() {
    const router = useRouter();
    const isLoggedIn = ref(false);

    onMounted(() => {
      // Ambil status login dari localStorage saat komponen dimuat
      isLoggedIn.value = localStorage.getItem('isLoggedIn') === 'true';
    });

    const logout = () => {
      localStorage.removeItem('isLoggedIn');
      isLoggedIn.value = false;
      router.push('/login');
    };

    return { isLoggedIn, logout };
  }
};
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(to right, #14532d, #166534); /* dark green gradient */
  backdrop-filter: blur(12px);
  padding: 1rem 2rem;
  border-bottom-left-radius: 16px;
  border-bottom-right-radius: 16px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  animation: slideDown 0.7s ease;
  position: sticky;
  top: 0;
  z-index: 1000;
}

@keyframes slideDown {
  0% {
    transform: translateY(-100%);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: bold;
  font-size: 1.4rem;
  color: #d1fae5;
  text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
}

.logo img {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  box-shadow: 0 0 12px rgba(16, 185, 129, 0.5);
  transition: transform 0.3s ease;
}

.logo img:hover {
  transform: rotate(6deg) scale(1.05);
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.nav-links a,
.nav-links .login-link {
  color: #ecfdf5;
  text-decoration: none;
  font-weight: 500;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  position: relative;
  transition: all 0.3s ease;
}

.nav-links a::after,
.nav-links .login-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  height: 2px;
  width: 0%;
  background-color: #bbf7d0;
  transition: width 0.3s ease;
}

.nav-links a:hover::after,
.nav-links .login-link:hover::after {
  width: 100%;
}

.nav-links a:hover,
.nav-links .login-link:hover {
  color: #a7f3d0;
  transform: translateY(-1px);
}

button {
  background: linear-gradient(to right, #ef4444, #dc2626);
  color: #fff;
  padding: 0.5rem 1rem;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 6px 14px rgba(239, 68, 68, 0.4);
  transition: all 0.3s ease;
}

button:hover {
  background: linear-gradient(to right, #f87171, #f43f5e);
  transform: scale(1.05);
  box-shadow: 0 8px 20px rgba(252, 165, 165, 0.4);
}
</style>
