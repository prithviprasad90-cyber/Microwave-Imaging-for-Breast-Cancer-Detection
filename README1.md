# 🩺 Microwave Imaging for Breast Cancer Detection

> B.Tech Seminar Report — Electronics and Communication Engineering  
> APJ Abdul Kalam Technological University  
> Rajagiri School of Engineering and Technology, Kochi — 2019  
> **Author:** Prithvi Prasad (RET17EC117)

---

## 📌 Overview

This project explores **Ultrawide Band (UWB) Microwave Imaging** as a safe, low-cost, and accurate alternative to conventional breast cancer detection methods such as X-ray mammography and MRI.

The core idea is that **malignant tumour tissue and normal breast tissue have significantly different electrical properties**. By transmitting microwave signals through the breast and analyzing the scattered returns, a tumour can be detected and localized — even at an early stage (as small as 2mm radius).

---

## ❓ Why Microwave Imaging?

| Method | Limitation |
|---|---|
| X-ray Mammography | High false positive & negative rates; ionizing radiation; unsafe for repeated use |
| MRI | High sensitivity but too many false positives; expensive |
| **UWB Microwave Imaging** | ✅ Safe, non-ionizing, low-cost, high contrast |

---

## ⚙️ How It Works

### Physical Principle

- **Malignant tumours** have **high water content** → large microwave scattering cross-section
- **Normal fatty breast tissue** has **low water content** → low microwave absorption → good for backscatter measurement
- Tumour vascularization further enhances scattering
- Normal tissue ≈ fat (electrically); Tumour ≈ muscle (electrically)

This contrast allows microwave signals to "see" the tumour inside the breast.

### System Architecture

A transmitting antenna sends a **Gaussian UWB pulse** into the breast. Multiple receiving antennas capture the scattered signals. Signal processing then isolates the tumour response and reconstructs its location.

![Breast Model with Transmitter and Receivers](fig1_1_breast_model_intro.png)
*Figure 1: Breast model showing the transmitter and surrounding receivers*

---

## 🧱 Breast Model (CST Microwave Studio)

The simulation was built in **CST Microwave Studio**, a professional electromagnetic simulation tool.

**Model Specifications:**
- Hemispherical breast model — **50 mm radius**
- Contains breast tissue only (no skin layer or glandular structures, for simplicity)
- **4 horn antennas** placed symmetrically around the breast at equal heights
  - Antenna 1 → Transmitter
  - Antennas 2, 3, 4 → Receivers
- Tumour: **spherical, 2 mm radius**, placed at coordinates **(−10, 10, 10)**

![CST Breast Model with 4 Antennas](fig4_1_breast_model_cst.png)
*Figure 2: 3D breast model with four horn antennas (Ant 1–4) constructed in CST Microwave Studio*

---

## 🧪 Simulation

The simulation was run in two stages:

**Stage 1 — Without Tumour**
- Antenna 1 transmits a **5 GHz bandwidth Gaussian pulse**
- Antennas 2–4 record received signals → this is the **baseline**

**Stage 2 — With Tumour**
- A 2 mm spherical tumour is added at (−10, 10, 10)
- Same pulse transmitted and responses re-recorded

**Tumour Signal Extraction**
- Subtract Stage 1 from Stage 2 → isolates the **tumour scattering signature**

![Simulation Setup with Tumour](fig6_1_breast_model_simulation.png)
*Figure 3: Breast model with tumour (highlighted in red) used in CST simulation*

---

## 📈 Simulation Results

The peak signal amplitudes (tumour response) were observed at:

| Receiver Antenna | Peak Time |
|---|---|
| Antenna 2 | 2.423 ns |
| Antenna 3 | 2.778 ns |
| Antenna 4 | 2.423 ns |

Antenna 3 shows a later peak because it is positioned farther from the tumour — consistent with the geometry of the model.

### Signal Graphs

**Antenna 1 → Antenna 2:**

![Signal Result Antenna 2](fig6_2_signal_antenna2.png)
*Figure 4: Received signal at Antenna 2 — with and without tumour*

**Antenna 1 → Antenna 3:**

![Signal Result Antenna 3](fig6_3_signal_antenna3.png)
*Figure 5: Received signal at Antenna 3 — with and without tumour*

---

## 🧠 Signal Processing — Delay-and-Sum Algorithm

After extracting the tumour signal, the **confocal Delay-and-Sum (DAS)** algorithm reconstructs where inside the breast the tumour is located.

**How it works:**
1. Scan every possible focal point (x, y, z) inside the breast
2. For each focal point, calculate the expected time delay to each receiver
3. Time-shift all received signals accordingly and sum them
4. Where the summed energy is **maximum** → that's the tumour location

This is conceptually similar to focusing a lens — when you focus on the right point, the image sharpens.

---

## ✅ Conclusion

- The **Delay-and-Sum algorithm** successfully detected and localized a **2 mm tumour** inside the simulated breast
- More receiver antennas = better image definition
- This approach is a **safe, non-ionizing, low-cost** alternative to existing detection methods

### Future Work
- Automate time-delay calculation without prior knowledge of tumour position
- Add loss equalization to compensate for signal attenuation through tissue
- Extend to full **3D imaging** using antennas on multiple planes

---

## 🛠️ Tools & Technologies

- **CST Microwave Studio** — 3D electromagnetic simulation
- **UWB Signal Processing** — Delay-and-Sum (confocal) beamforming
- **Gaussian Pulse** — 5 GHz bandwidth transmitted signal

---

## 📚 References

1. Zhao Wang et al. — *Medical Application of Microwave Imaging*, 2014
2. Elise C. Fear et al. — *Breast Tumour Detection*
3. S. Gabriel et al. — *The Dielectric Properties of Biological Tissues*
4. Hooi Been Lim et al. — *Confocal Microwave Imaging for Breast Cancer Detection: Delay-Multiply-and-Sum Image Reconstruction Algorithm*, IEEE 2008

---

## 👤 Author

**Prithvi Prasad**  
B.Tech — Electronics and Communication Engineering  
Rajagiri School of Engineering and Technology, Kochi  
APJ Abdul Kalam Technological University — 2019

> Guide: Ms. Deepthy G S  
> Head of Department: Dr. Rithu James  
> Seminar Coordinator: Dr. Sreekumar G
