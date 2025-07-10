<template>
  <div class="max-w-3xl mx-auto p-6">
    <h1 class="text-2xl font-bold mb-4">Checkout</h1>

    <div v-if="cart.items.length === 0">
      <p class="text-gray-600">Tidak ada produk untuk checkout</p>
    </div>

    <div v-else class="space-y-6">
      <!-- Daftar Item -->
      <div class="cart-list">
  <div
    v-for="item in cart.items"
    :key="item.id"
    class="cart-item"
  >
    <img :src="item.gambar" :alt="item.nama" class="product-image" />
    <div class="item-info">
      <h3 class="font-bold text-lg">{{ item.nama }}</h3>
      <p>{{ item.quantity }} x Rp {{ item.harga.toLocaleString('id-ID') }}</p>
    </div>
  </div>
</div>


      <hr class="my-4 border-gray-400" />

      <p class="text-xl font-semibold">
        Total Bayar: Rp {{ cart.totalPrice.toLocaleString('id-ID') }}
      </p>

      <!-- Form Pembayaran -->
      <form @submit.prevent="prosesPembayaran" class="space-y-4">
        <!-- Select Metode Pembayaran -->
<div>
  <label class="block text-sm font-medium text-white mb-1">Pilih Metode Pembayaran:</label>
  <div class="relative">
    <select v-model="metode" class="modern-select">
      <optgroup label="Kartu">
        <option value="kartu-bri">💳 Kartu BRI</option>
        <option value="kartu-bca">💳 Kartu BCA</option>
        <option value="kartu-bni">💳 Kartu BNI</option>
        <option value="kartu-mandiri">💳 Kartu Mandiri</option>
      </optgroup>
      <option value="virtual">🏦 Virtual Account</option>
      <option value="cod">🚚 COD (Bayar di Tempat)</option>
      <option value="qris">📱 QRIS</option>
    </select>
  </div>
</div>

<!-- Tombol Konfirmasi -->
<button
  type="submit"
  class="confirm-button"
>
  ✅ Konfirmasi Pembayaran
</button>

        <div v-if="metode.startsWith('kartu')" class="space-y-2">
          <input v-model="kartu.nama" placeholder="Nama di Kartu" class="w-full border p-2 rounded" />
          <input v-model="kartu.nomor" placeholder="Nomor Kartu" class="w-full border p-2 rounded" />
          <div class="flex space-x-2">
            <input v-model="kartu.exp" placeholder="MM/YY" class="w-1/2 border p-2 rounded" />
            <input v-model="kartu.cvv" placeholder="CVV" class="w-1/2 border p-2 rounded" />
          </div>
        </div>

        
      </form>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import { ref } from 'vue'
import { useCartStore } from '../store/cartStore'

const cart = useCartStore()
const router = useRouter()
const metode = ref('')
const kartu = ref({
  nama: '',
  nomor: '',
  exp: '',
  cvv: ''
})

function prosesPembayaran() {
  if (!metode.value) {
    alert('Pilih metode pembayaran terlebih dahulu.')
    return
  }

  if (metode.value.startsWith('kartu')) {
    if (!kartu.value.nama || !kartu.value.nomor || !kartu.value.exp || !kartu.value.cvv) {
      alert('Lengkapi semua data kartu.')
      return
    }
  }

  alert('Pembayaran berhasil dengan metode: ' + metode.value)
  cart.clearCart()
  router.push('/beranda')
}
</script>

<style scoped>



.cart-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1rem;
}

.cart-item {
  display: flex;
  background: #7b9a81; /* bg-gray-800 */
  border: 1px solid #838a71; /* border-gray-700 */
  border-radius: 12px;
  padding: 1rem;
  gap: 1rem;
  align-items: center;
  color: #f0fdf4; /* text-green-50 */
}

.product-image {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 8px;
  flex-shrink: 0;
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);
  transition: transform 0.3s ease;
}

.product-image:hover {
  transform: scale(1.05);
}

.item-info {
  flex-grow: 1;
}

input {
  outline: none;
}

input,
select {
  outline: none;
  background-color: #f1f5f9;
  border: 1px solid #cbd5e1;
  transition: all 0.3s ease;
}

input:focus,
select:focus {
  border-color: #22c55e;
  box-shadow: 0 0 0 3px rgba(34, 197, 94, 0.3);
  background-color: #fff;
}

select.modern-select {
  background-image: linear-gradient(to right, #d1fae5, #f0fdf4);
  font-weight: 500;
  color: #065f46;
}

select.modern-select option {
  padding: 0.5rem;
}

/* Modern Select Dropdown */
.modern-select {
  width: 100%;
  padding: 0.75rem 1rem;
  background-color: #f9fafb;
  color: #1f2937;
  font-size: 1rem;
  font-weight: 500;
  border-radius: 10px;
  border: 1px solid #cbd5e1;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg fill='none' stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' viewBox='0 0 24 24'%3E%3Cpath d='M19 9l-7 7-7-7'%3E%3C/path%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 0.75rem center;
  background-size: 1.25rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.modern-select:focus {
  outline: none;
  border-color: #10b981;
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.3);
  background-color: white;
  color: #111827;
}

/* Tombol Konfirmasi Modern */
.confirm-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1.5rem;
  background: linear-gradient(to right, #10b981, #059669);
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.4);
  transition: all 0.3s ease;
  font-size: 1rem;
  margin-top: 1rem;
}

.confirm-button:hover {
  background: linear-gradient(to right, #059669, #047857);
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 16px rgba(5, 150, 105, 0.4);
}



</style>


