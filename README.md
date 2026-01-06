# 🔐 AES-128 Pipelined Encryption (Verilog)

Hardware-Optimized **AES-128 Encryption Core** using **Deep Pipelining** for high throughput and efficient FPGA resource utilization.

This project presents **two pipelined AES-128 implementations** in Verilog:
- **Variant 1:** LUT-based design optimized for speed  
- **Variant 2:** BRAM-based T-Table design optimized for area efficiency  

---

## 📌 Project Overview

- **Algorithm:** AES-128 (Advanced Encryption Standard)
- **Block Size:** 128 bits
- **Key Size:** 128 bits
- **Rounds:** 10
- **Design Style:** Fully unrolled, deeply pipelined
- **Target Platform:** FPGA (Xilinx-based synthesis results)

The goal of this project is to **maximize throughput** while balancing **area and latency** using architectural optimizations.

---

## 🧠 AES Core Operations

Each AES round consists of the following transformations:

1. **SubBytes** – Byte substitution using Rijndael S-Box  
2. **ShiftRows** – Cyclic row shifting for diffusion  
3. **MixColumns** – Galois Field matrix multiplication  
4. **AddRoundKey** – XOR with round key  
5. **Key Expansion** – Generates round keys from the cipher key  

---

## 🚀 Why Pipelining?

Pipelining improves performance by:
- Dividing AES computation into smaller stages
- Allowing multiple blocks to be processed concurrently
- Producing **one encrypted block per clock cycle** after pipeline fill
- Increasing maximum clock frequency

---

## 🧩 Implementation Variants

### 🔹 Variant 1: LUT-Based AES Pipeline

**Key Features**
- Distributed LUT-based S-Box implementation
- LUT-based GF(2⁸) multiplication (mul2, mul3)
- 19–20 stage pipeline
- Parallel key expansion
- Each AES round split into two pipeline stages

**Pros**
- Very high speed
- Simple control logic
- No BRAM dependency

**Cons**
- Higher LUT utilization

---

### 🔹 Variant 2: BRAM-Based AES Pipeline (T-Tables)

**Key Features**
- BRAM-stored T-Tables (SubBytes + ShiftRows + MixColumns)
- Dual-port BRAM for simultaneous lookups
- Synchronous BRAM reads add one cycle latency
- XOR-fold reduction for shorter critical paths
- Split key expansion pipeline

**Pros**
- ~72% reduction in LUT usage
- Better scalability for large designs
- Balanced area vs performance

**Cons**
- Slightly higher latency due to BRAM access

---

## 📊 Performance Summary

### ⏱ Clock & Throughput

| Metric | Value |
|------|------|
| Clock Period | ~4.67 ns |
| Frequency | ~214 MHz |
| Throughput | **~27.43 Gbps** |
| Output Rate | 1 × 128-bit block / cycle |

---

### 📐 Resource Utilization

#### Variant 1 (LUT-Based)
- Slice LUTs: **18.93%**
- Slice Registers: **5.29%**
- BRAM Usage: **0**
- Initial Latency: ~93.4 ns

#### Variant 2 (BRAM-Based)
- Slice LUTs: **8.15%**
- Slice Registers: **5.29%**
- BRAM Tiles Used: **36**
- Initial Latency: ~98.07 ns

---

## 🧪 Verification

- Functional simulation using standard AES test vectors
- Waveform analysis confirms correct pipeline behavior
- All ciphertext outputs match expected AES-128 results
- Continuous throughput verified after pipeline fill

---

## 🏁 Conclusion

- Achieved **27.4 Gbps throughput** with fully unrolled pipelined AES
- BRAM-based T-Tables significantly reduce LUT utilization
- Design balances **throughput, area, and scalability**
- Suitable for high-performance cryptographic accelerators

---

## 👥 Team

**TEAM I/O Tea ☕**
- Manoj Kumar Mali  
- Manas Dhaketa  
- K. Yashwant Rao  
- Darshana Baruah  
- Gaurav Singh Bora  

---

## 📚 References

- FPGA and ASIC Implementations of AES – ResearchGate  
- AES Key Expansion – Tutorialspoint  
- Pipelined Cryptographic Architectures – ResearchGate  

---

⭐ If you find this project useful, consider giving it a star!
