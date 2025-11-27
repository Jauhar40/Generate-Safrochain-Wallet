# Safrochain Testnet Wallet Generator v2.0

Advanced Cosmos SDK wallet generator untuk Safrochain Testnet. Compatible dengan Keplr Wallet dan menggunakan standar BIP39/BIP44/Bech32.

## ✨ Fitur Utama

- **BIP39 Mnemonic** - Generate 24-word mnemonic phrase (256-bit entropy)
- **BIP44 Derivation Path** - Standard Cosmos path (`m/44'/118'/0'/0/0`)
- **Bech32 Encoding** - Native Cosmos address format
- **Keplr Compatible** - Langsung import ke Keplr Wallet
- **Append Mode** - Data baru ditambahkan tanpa menimpa yang lama
- **Pure Python** - Tidak butuh dependency eksternal yang rumit

## 🔗 Registration

👉 **https://safrochain.com/**

## 📦 Installation

### 1. Install Python
Pastikan Python 3.7+ terinstall:
```bash
python3 --version
```

### 2. Install Dependencies
```bash
pip install ecdsa
```

### 3. Download Script
```bash
git clone https://github.com/Jauhar40/Generate-Safrochain-Wallet.git
cd safrochain-wallet-generator
```

## 🚀 Cara Penggunaan

### Generate Wallet
```bash
python3 generate.py
```

Script akan menanyakan jumlah wallet:
```
Mau berapa wallet? 5
```

### Output Files

Script menghasilkan 3 file dengan mode **APPEND** (data baru ditambahkan ke baris berikutnya):

- **`wallet.txt`** - Alamat wallet (format: `addr_safro...`)
- **`pk.txt`** - Private keys (hex format)
- **`phrase.txt`** - Mnemonic phrases (24 kata)

### Example Output
```
[1/5] addr_safro1qpzry9x8gf2tvdw0s3jn54khce6mua7lmqqqq
[2/5] addr_safro1xyz...abc
[3/5] addr_safro1def...ghi
...

✅ Berhasil generate 5 wallet!
📁 File tersimpan (MODE APPEND - data lama tetap ada):
 - wallet.txt (alamat wallet)
 - pk.txt (private key)
 - phrase.txt (mnemonic/phrase)
```

## 🔐 Import ke Keplr Wallet

### Method 1: Import via Mnemonic (Recommended)
1. Buka Keplr Wallet Extension
2. Klik **"Import existing wallet"**
3. Pilih **"Use recovery phrase or private key"**
4. Copy mnemonic (24 kata) dari `phrase.txt`
5. Paste ke Keplr
6. Set password dan confirm
7. Add Safrochain network (jika belum ada)

### Method 2: Import via Private Key
1. Buka Keplr Wallet
2. Klik **"Import existing wallet"**
3. Pilih **"Use private key"**
4. Copy private key dari `pk.txt`
5. Paste ke Keplr
6. Confirm

## 🛠️ Technical Details

### Cosmos SDK Standards
- **Address Prefix**: `addr_safro` (Safrochain native)
- **Derivation Path**: `m/44'/118'/0'/0/0` (Cosmos standard)
- **Coin Type**: 118 (ATOM/Cosmos)
- **Curve**: SECP256k1 (same as Bitcoin/Ethereum)
- **Encoding**: Bech32 (Cosmos native)

### Mnemonic Generation
- **Entropy**: 256 bits (32 bytes)
- **Word Count**: 24 words (more secure than 12 words)
- **Checksum**: SHA-256 based
- **Wordlist**: BIP39 English (2048 words)

### Key Derivation Flow
```
Mnemonic (24 words)
    ↓
Seed (PBKDF2-HMAC-SHA512)
    ↓
Master Private Key (HMAC-SHA512)
    ↓
Child Keys (BIP44 derivation)
    ↓
Public Key (SECP256k1)
    ↓
Address (SHA256 → RIPEMD160 → Bech32)
```

## 📊 File Format Examples

### wallet.txt
```
addr_safro1qpzry9x8gf2tvdw0s3jn54khce6mua7lmqqqq
addr_safro1abc123def456ghi789jkl012mno345pqr678st
addr_safro1xyz987wvu654tsr321qpo098nml765kji432hg
```

### pk.txt
```
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5z6a7b8c9d0e1f2
1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef
fedcba0987654321fedcba0987654321fedcba0987654321fedcba0987654321
```

### phrase.txt
```
abandon ability able about above absent absorb abstract absurd abuse access accident account accuse achieve acid acoustic acquire across act action actor actress actual
witch collapse practice feed shame open despair creek road again ice least height dream treat reunion gather gym gossip agent excuse write verify
```

## 💡 Use Cases

- **Testnet Testing** - Generate multiple wallets untuk testing
- **Airdrop Farming** - Siapkan multiple addresses untuk airdrop
- **Development** - Testing smart contracts dengan multiple accounts
- **Batch Operations** - Operasi blockchain dalam skala besar

## 🔄 Append Mode Explained

Script ini menggunakan **APPEND MODE**, bukan overwrite mode:
```python
# Generate pertama (5 wallet)
python3 generate.py
# Output: wallet.txt berisi 5 addresses

# Generate kedua (3 wallet)
python3 generate.py
# Output: wallet.txt sekarang berisi 8 addresses (5 lama + 3 baru)
```

**Keuntungan:**
- Data lama tetap aman
- Tidak perlu backup setiap kali generate
- Bisa generate batch secara bertahap

## ⚠️ Security Warning

**CRITICAL - BACA INI:**

1. **JANGAN PERNAH** commit atau upload file berikut ke GitHub:
   - `wallet.txt`
   - `pk.txt`
   - `phrase.txt`

2. **JANGAN SHARE** private key atau mnemonic phrase kepada siapapun

3. **BACKUP** file dengan aman (encrypted storage recommended)

4. **GUNAKAN** di environment yang aman (offline recommended)

5. **MNEMONIC = FULL ACCESS** - Siapapun yang punya mnemonic punya kontrol penuh atas wallet

### Tambahkan ke `.gitignore`:
```gitignore
# Wallet files - NEVER COMMIT
wallet.txt
pk.txt
phrase.txt

# Python cache
__pycache__/
*.pyc
*.pyo
*.pyd
.Python

# Virtual environment
venv/
env/
ENV/
```

## 🐛 Troubleshooting

### Error: Library 'ecdsa' belum terinstall
```bash
pip install ecdsa
```

### Error: Invalid address format
- Pastikan script menggunakan prefix yang benar (`addr_safro`)
- Check apakah Safrochain network sudah ditambahkan ke Keplr

### Wallet tidak muncul di Keplr
- Pastikan mnemonic di-copy dengan benar (24 kata, tidak ada extra spaces)
- Pastikan Safrochain network sudah terdaftar di Keplr
- Try import via private key jika mnemonic tidak work

### File tidak ter-generate
- Check permission folder (read/write access)
- Pastikan script di-run dari directory yang benar
- Check disk space available

## 🎯 Best Practices

1. **Test dulu** - Generate 1 wallet, test import ke Keplr
2. **Backup immediately** - Copy file ke secure location
3. **Verify** - Import wallet ke Keplr dan check address match
4. **Organize** - Gunakan naming convention untuk multiple batch
5. **Clean up** - Delete file setelah backup (jangan tinggalkan di public folder)

## 📖 Example Workflow
```bash
# 1. Install dependencies
pip install ecdsa

# 2. Generate wallets
python3 generate.py
# Input: 10

# 3. Verify output files
ls -la wallet.txt pk.txt phrase.txt

# 4. Backup to secure location
cp wallet.txt ~/secure-backup/safro-wallet-$(date +%Y%m%d).txt
cp pk.txt ~/secure-backup/safro-pk-$(date +%Y%m%d).txt
cp phrase.txt ~/secure-backup/safro-phrase-$(date +%Y%m%d).txt

# 5. Import to Keplr
# Use mnemonic from phrase.txt

# 6. Clean up (optional)
# rm wallet.txt pk.txt phrase.txt
```

## 🔍 Address Validation

Untuk verify address yang di-generate:
- Address harus dimulai dengan `addr_safro`
- Panjang address sekitar 44-46 karakter (setelah prefix)
- Format: `addr_safro1` + 39-41 karakter (lowercase alphanumeric)

Example valid address:
```
addr_safro1qpzry9x8gf2tvdw0s3jn54khce6mua7lmqqqq
```

## 🌐 Safrochain Network Info

- **Network Name**: Safrochain Testnet
- **RPC Endpoint**: https://rpc.testnet.safrochain.com
- **REST Endpoint**: https://rest.testnet.safrochain.com
- **Explorer**: https://safrochain.com/

Untuk info network terbaru, kunjungi: https://safrochain.com/

## 📋 Requirements Summary

- Python 3.7+
- Library: `ecdsa`
- OS: Linux, macOS, Windows (any)
- Disk Space: Minimal (<1MB per 1000 wallets)

## ⚖️ License

MIT License - Free to use

## ⚠️ Disclaimer

Tool ini dibuat untuk **Safrochain Testnet**. Author tidak bertanggung jawab atas:
- Kehilangan aset akibat penggunaan yang tidak aman
- Kesalahan user dalam backup atau import
- Penyalahgunaan tool untuk tujuan illegal
- Perubahan network configuration dari Safrochain

**Selalu backup mnemonic phrase dengan aman. Mnemonic = Full Access to Your Wallet.**

---

## 📞 Support

- **Website**: https://safrochain.com/
- **Documentation**: https://docs.safrochain.com/
- **Issues**: Open issue di GitHub repository

**Happy Testing on Safrochain! 🚀**

---

**Register Now:** https://safrochain.com/
