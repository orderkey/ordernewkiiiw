<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KIIIWJASTEB Payment</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
    <style>
        body { background-color: #0f172a; color: #f1f5f9; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; }
        .app-container { background-color: #1e293b; max-width: 480px; margin: 0 auto; min-height: 100vh; display: flex; flex-direction: column; box-shadow: 0 0 40px rgba(0,0,0,0.5); position: relative; }
        
        .page { display: none; padding: 24px; flex-direction: column; min-height: 100vh; animation: slideUp 0.4s ease; }
        .active { display: flex; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .plan-card { background-color: #1a2235; border-radius: 16px; padding: 20px; cursor: pointer; border: 2px solid #2d3748; transition: all 0.2s ease; position: relative; overflow: hidden; }
        .plan-card.selected { border-color: #10b981; background-color: #142d2d; box-shadow: 0 0 15px rgba(16, 185, 129, 0.2); }
        
        .badge { font-size: 10px; font-weight: 900; padding: 4px 12px; border-radius: 20px; display: inline-flex; items-center; gap: 4px; margin-bottom: 8px; text-transform: uppercase; }
        .badge-starter { background: #1e3a3a; color: #34d399; }
        .badge-populer { background: #3b2a1a; color: #fbbf24; }
        .badge-premium { background: #2a1a3b; color: #a78bfa; }
        .badge-reseller { background: #1a2e3b; color: #60a5fa; }

        .input-field { background-color: #334155; border: 2px solid transparent; color: white; border-radius: 14px; padding: 16px; width: 100%; outline: none; transition: 0.2s; }
        .input-field:focus { border-color: #6366f1; background-color: #3d4b5f; }

        #overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(15, 23, 42, 0.95); z-index: 1000; flex-direction: column; justify-content: center; align-items: center; }
        .loader { border: 4px solid rgba(255,255,255,0.1); border-top: 4px solid #6366f1; border-radius: 50%; width: 45px; height: 45px; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .qris-section { background-color: rgba(30, 41, 59, 0.5); border: 1px dashed #475569; border-radius: 20px; padding: 20px; text-align: center; }
        .qris-box { background-color: #fff; padding: 15px; border-radius: 20px; display: inline-block; transition: transform 0.2s; cursor: pointer; }
    </style>
</head>
<body>

    <div id="overlay">
        <div class="loader mb-4"></div>
        <p class="text-white font-bold tracking-wider uppercase text-xs">Menyiapkan Konfirmasi...</p>
    </div>

    <div class="app-container">
        
        <!-- HALAMAN 1 -->
        <div id="page-1" class="page active">
            <div class="flex items-center gap-4 mb-8 mt-2">
                <div class="bg-indigo-600 p-3 rounded-2xl">
                    <i class="fa-solid fa-key text-white text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-black text-white tracking-tight">KIIIWJASTEB</h1>
                    <p class="text-indigo-400 text-[10px] font-black uppercase tracking-widest">Beli Key Premium</p>
                </div>
            </div>

            <div class="mb-6">
                <label class="block text-indigo-400 text-[10px] font-black mb-2 uppercase tracking-widest">Nomor WhatsApp</label>
                <input type="tel" id="userPhone" placeholder="08xxxxxxxxxx" class="input-field font-bold">
                <p class="text-[9px] text-slate-500 mt-2">Key/akses akan dikirim ke nomor ini</p>
            </div>

            <p class="text-slate-400 text-[10px] font-black mb-4 uppercase tracking-widest flex items-center gap-2">
                <i class="fa-solid fa-key"></i> PAKET USER
            </p>

            <div class="space-y-3 mb-8">
                <!-- STARTER -->
                <div class="plan-card" onclick="pickItem(this, '7 Jam', '15.000')">
                    <div class="badge badge-starter"><i class="fa-solid fa-bolt"></i> Starter</div>
                    <div class="flex justify-between items-end">
                        <div>
                            <h2 class="text-white text-xl font-black">7 Jam</h2>
                            <p class="text-emerald-500 font-black text-lg">Rp 15.000</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Max 2 email</p>
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Durasi 7 Jam</p>
                        </div>
                    </div>
                </div>

                <!-- POPULER -->
                <div class="plan-card" onclick="pickItem(this, '15 Jam', '20.000')">
                    <div class="badge badge-populer"><i class="fa-solid fa-fire"></i> Populer</div>
                    <div class="flex justify-between items-end">
                        <div>
                            <h2 class="text-white text-xl font-black">15 Jam</h2>
                            <p class="text-emerald-500 font-black text-lg">Rp 20.000</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Max 3 email</p>
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Durasi 15 Jam</p>
                        </div>
                    </div>
                </div>

                <!-- PREMIUM -->
                <div class="plan-card" onclick="pickItem(this, '24 Jam', '25.000')">
                    <div class="badge badge-premium"><i class="fa-solid fa-crown"></i> Premium</div>
                    <div class="flex justify-between items-end">
                        <div>
                            <h2 class="text-white text-xl font-black">24 Jam</h2>
                            <p class="text-emerald-500 font-black text-lg">Rp 25.000</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Max 4 email</p>
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Durasi 24 Jam</p>
                        </div>
                    </div>
                </div>

                <!-- RESELLER -->
                <div class="plan-card" onclick="pickItem(this, 'Reseller', '50.000')">
                    <div class="badge badge-reseller"><i class="fa-solid fa-store"></i> Reseller</div>
                    <div class="flex justify-between items-end">
                        <div>
                            <h2 class="text-white text-xl font-black">Reseller</h2>
                            <p class="text-emerald-500 font-black text-lg">Rp 50.000</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Max 0 email</p>
                            <p class="text-[9px] text-slate-500 uppercase font-bold">Durasi Reseller</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="qris-section mb-8">
                <p class="text-slate-400 text-[10px] font-black uppercase tracking-widest mb-4">METODE PEMBAYARAN QRIS</p>
                <div class="qris-box shadow-xl mb-3" onclick="window.open('https://photos.app.goo.gl/Fx6T4kwXNkv3VvUQ8', '_blank')">
                    <div class="w-32 h-32 flex flex-col items-center justify-center bg-slate-50 border-2 border-indigo-100 rounded-xl">
                        <i class="fa-solid fa-qrcode text-5xl text-indigo-600 mb-1"></i>
                        <span class="text-[8px] font-black text-indigo-900 uppercase">Klik Gambar</span>
                    </div>
                </div>
                <p class="text-indigo-400 text-[10px] font-black uppercase animate-pulse">KETUK UNTUK MEMPERBESAR</p>
            </div>

            <div class="mb-10">
                <label class="block text-slate-400 text-[10px] font-black mb-3 uppercase tracking-widest">Unggah Foto Bukti Transfer</label>
                <div class="bg-slate-800 border-2 border-dashed border-slate-700 rounded-xl flex items-center p-2">
                    <input type="file" id="proofFile" class="hidden" accept="image/*" onchange="updateFileName()">
                    <button onclick="document.getElementById('proofFile').click()" class="bg-indigo-600 px-5 py-3 rounded-lg text-[10px] font-black text-white uppercase active:scale-95 transition">Pilih Foto Bukti</button>
                    <span id="fileName" class="px-4 text-slate-500 text-xs truncate italic">Belum ada file dipilih</span>
                </div>
            </div>

            <button onclick="processPayment()" class="w-full bg-emerald-600 hover:bg-emerald-500 py-5 rounded-2xl font-black text-white text-lg mt-auto mb-6 uppercase tracking-widest shadow-xl shadow-emerald-500/20 active:scale-95 transition-all">
                Konfirmasi Pembayaran
            </button>
        </div>

        <!-- HALAMAN 2 -->
        <div id="page-2" class="page items-center justify-center text-center">
            <div class="bg-emerald-500 w-20 h-20 rounded-full flex items-center justify-center mb-8">
                <i class="fa-solid fa-check text-white text-4xl"></i>
            </div>
            <h1 class="text-3xl font-black text-white mb-2 uppercase tracking-tight">SIAP DIKIRIM!</h1>
            <p class="text-slate-400 text-sm mb-12">Paket: <span id="res-plan" class="text-indigo-400 font-bold"></span></p>

            <div class="bg-slate-800 border border-slate-700 rounded-3xl w-full p-8 mb-8">
                <p class="text-slate-400 text-[10px] font-black uppercase mb-2 tracking-widest">Nomor WhatsApp</p>
                <p id="res-phone" class="text-white text-3xl font-black tracking-widest uppercase truncate">08XX</p>
            </div>

            <button onclick="sendToWA()" class="w-full bg-emerald-600 hover:bg-emerald-500 text-white py-5 rounded-2xl font-black text-sm mb-6 uppercase tracking-widest flex items-center justify-center gap-3 active:scale-95 transition-all">
                <i class="fa-brands fa-whatsapp text-2xl"></i> KIRIM KE WHATSAPP ADMIN
            </button>

            <button onclick="location.reload()" class="text-slate-500 text-[10px] font-black hover:text-indigo-400 uppercase tracking-widest">
                Kembali ke Awal
            </button>
        </div>

    </div>

    <script>
        let selectedData = { name: "", price: "" };
        let waLink = "";
        const ADMIN_NUMBER = "6283827384467";

        function pickItem(el, name, price) {
            document.querySelectorAll('.plan-card').forEach(c => c.classList.remove('selected'));
            el.classList.add('selected');
            selectedData = { name, price };
        }

        function updateFileName() {
            const file = document.getElementById('proofFile').files[0];
            const label = document.getElementById('fileName');
            if(file) {
                label.innerText = file.name;
                label.classList.add('text-indigo-400', 'font-bold');
            }
        }

        function sendToWA() {
            if(waLink) window.open(waLink, '_blank');
        }

        function processPayment() {
            const phone = document.getElementById('userPhone').value.trim();
            const fileInput = document.getElementById('proofFile');
            const file = fileInput.files[0];

            if(!phone || !selectedData.name || !file) {
                Swal.fire({ icon: 'warning', title: 'Data Kurang', text: 'Pilih paket, isi Nomor WhatsApp, dan unggah bukti!', background: '#1e293b', color: '#fff' });
                return;
            }

            document.getElementById('overlay').style.display = 'flex';

            setTimeout(() => {
                document.getElementById('res-plan').innerText = selectedData.name;
                document.getElementById('res-phone').innerText = phone;
                document.getElementById('page-1').classList.remove('active');
                document.getElementById('page-2').classList.add('active');
                document.getElementById('overlay').style.display = 'none';

                const message = `Halo Admin KIIIWJASTEB,\nSaya ingin konfirmasi pembayaran:\n\n📱 *Nomor WhatsApp:* ${phone}\n⏱️ *Durasi:* ${selectedData.name}\n💰 *Harga:* Rp ${selectedData.price}\n\nJIKA SUDAH MENG TRANSFER? HARAP BACA!!\n📎 \`[ HARAP SERTAKAN BUKTI ULANG ]\`\n\nJika sudah proses akan segera di lakukan, harap tunggu admin kiiiw merespon`;
                
                waLink = `https://wa.me/${ADMIN_NUMBER}?text=${encodeURIComponent(message)}`;

                setTimeout(() => {
                    sendToWA();
                }, 1000);
            }, 800);
        }
    </script>
</body>
</html>
