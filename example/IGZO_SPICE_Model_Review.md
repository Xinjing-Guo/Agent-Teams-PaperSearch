# A Review of SPICE Compact Models for IGZO Thin-Film Transistors

## 1. Introduction

Amorphous indium-gallium-zinc oxide (a-IGZO) thin-film transistors (TFTs) have emerged as a leading technology for flat-panel displays, flexible electronics, and back-end-of-line (BEOL) integration in advanced CMOS nodes. As circuit complexity grows, accurate SPICE-compatible compact models become essential for bridging device physics and circuit design. This review surveys 26 papers spanning 2008–2025 that address IGZO SPICE modeling, organized by modeling methodology.

## 2. MOSFET SPICE Template-Based Models

### 2.1 SPICE Level 3 Adaptation

The earliest and most widely adopted approach adapts the standard MOSFET SPICE Level=3 model template for a-IGZO TFTs.

**Perumal et al. (2013)** [1] presented a compact model based on the MOSFET SPICE Level=3 template for analog/RF circuit design. The model was fitted to both DC and AC characteristics of a-IGZO TFTs, demonstrating good scalability of drain current across different device dimensions. This work established the Level=3 framework as a practical baseline for IGZO circuit simulation.

**Kandpal and Gupta (2019)** [8] further adapted the SPICE Level 3 model for oxide TFTs, addressing the fundamental difference between MOSFET and TFT conduction mechanisms. Their work provided a systematic parameter extraction methodology applicable to both a-IGZO and ZTO TFTs.

**Shabanpour et al. (2017)** [12] built upon the RPI amorphous TFT (RPI-aTFT) model framework, extending the existing amorphous silicon TFT model to accommodate a-IGZO device characteristics for circuit design applications.

### 2.2 HSPICE Level 61/62 (RPI Models)

**Dubey, Goswami, and Kandpal (2024)** [6] presented a comprehensive CAD model for a-IGZO TFTs by adapting HSPICE Level-61 (RPI a-Si:H TFT model) and Level-62 (RPI poly-Si TFT model). This work provided a complete understanding of the SPICE Level-61 and Level-62 model parameters that must be tuned for a-IGZO TFT simulation, along with comparative analysis of both models' accuracy.

### 2.3 SOI and BSIM Models

**Liu, Verity, Sou, and Gneiting (2024)** [14] proposed the Silicon-on-Insulator (SOI) model as a suitable SPICE model for flexible a-IGZO TFT devices, arguing that it offers unique advantages over traditional TFT SPICE models. The SOI model provides a crucial link between semiconductor process and circuit design.

**An All-Region BSIM TFT Model (2024)** [26] implemented a BSIM-based thin-film transistor model in Verilog-A for display and BEOL 3-D integration applications, providing a comprehensive framework for SPICE circuit simulations.

## 3. Physics-Based Verilog-A Models

### 3.1 Carrier Transport Models

**Jeon, Hur, Kim, and Bae et al. (2011)** [3] reported the first physics-based SPICE model of amorphous oxide semiconductor TFTs using Verilog-A. They demonstrated SPICE simulation of a-IGZO TFT inverters by incorporating the proposed model into circuit simulators, establishing the foundation for physics-based IGZO modeling.

**Kim, Jeon, Kim et al. (2011)** [4] extended this approach with physical parameter-based SPICE models for InGaZnO TFTs applicable to process optimization and robust circuit design. The proposed model successfully reproduced a-IGZO TFT characteristics and load-line diagrams of inverters.

**Ghittorelli, Torricelli, Colalongo, and Kovacs-Vajna (2014)** [2] developed an accurate analytical physical model accounting for the combined contribution of trapped and free charges moving through the a-IGZO film. This model provided deeper insight into the multi-trapping transport mechanism in amorphous oxide semiconductors.

### 3.2 Surface Potential-Based Models

**A New Surface Potential-Based Compact Model (2015)** [21] presented, for the first time, a surface potential-based compact model for a-IGZO TFTs based on multiple trapping-release theory for RFID applications, offering a physically rigorous alternative to threshold-voltage-based approaches.

**Surface Potential-Based Compact Model for IGZO-DRAM (2025)** [20] enabled a TCAD-to-SPICE framework for reliability-aware Design Technology Co-Optimization (DTCO) flow, bridging atomistic simulation and circuit-level analysis for emerging IGZO-based DRAM technology.

### 3.3 Large-Signal and Noise Models

**Vatsyayan and Dayeh (2023)** [11] developed a comprehensive model covering large signal, small signal, and noise characteristics for dual-gate amorphous-IGZO TFTs, providing a complete framework for analog circuit design where noise performance is critical.

**Hernandez-Barrios et al. (2020)** [13] proposed the Analytical Full Capacitance Model (AFCM) for dynamic simulation of a-IGZO TFT circuits, addressing transient behavior that static DC models cannot capture.

## 4. Compact Models for Specific Applications

### 4.1 Flexible and Strain-Aware Models

**Wan Zaidi, Costa, Munzenrieder et al. (2018)** [5] developed a flexible IGZO TFT SPICE model capable of predicting strain effects, and designed active strain-compensation circuits for bendable active matrix arrays. This work is critical for emerging flexible display and sensor applications.

**Kim, Seo, Jang et al. (2021)** [7] presented reliability-aware SPICE-compatible compact modeling of IGZO inverters on a flexible PET substrate with ALD Al₂O₃ gate insulator, addressing threshold voltage shift under mechanical stress.

### 4.2 Display Applications

**Baek and Kanicki (2012)** [16] modeled current-voltage characteristics for double-gate a-IGZO TFTs and their application to active-matrix LCDs, providing a model specifically validated for display driver circuits.

**Shao, Lei, Huang et al. (2019)** [15] developed a unified SPICE-compatible compact model validated with CNT, IGZO, and organic TFTs for flexible hybrid IoT design, demonstrating cross-technology applicability.

### 4.3 IGZO-Based Memory Devices

**Kim, Lee, Yang et al. (2022)** [9] introduced a compact SPICE model of a two-terminal memristor with Pd/Ti/IGZO/p⁺-Si structure, systematically separating short- and long-term memory components modulated by IGZO oxygen content.

**Jang, Min, Kim et al. (2020)** [10] developed a highly reliable physics-based SPICE compact model of IGZO memristors, considering the dependence on electrode metals and deposition sequence with non-quasi-statically updated Schottky barrier heights.

**Saha et al. (2019)** [19] proposed a SPICE compact model based on non-quasi-statically updated Schottky barriers for IGZO memristors with Pd/IGZO/Mo structure, combining thermionic emission and hopping transport.

**Physics-Based α-IGZO TFTs Compact Modeling with 2T0C DRAM Cell (2025)** [22] incorporated charge transport mechanisms such as percolation and Variable-Range Hopping (VRH) with neural network augmentation for 2T0C DRAM applications.

### 4.4 Ferroelectric Devices

**Rafiq et al. (2025)** [25] presented the first SPICE-compatible compact model of ferroelectric diodes with BE/HZO/IGZO/TE structure, incorporating modified Schottky barrier and hopping models for on/off-mode operation.

## 5. Emerging Approaches

### 5.1 Neural Network-Augmented Models

**Eom et al. (2024)** [24] proposed a neural compact modeling framework that used I-V characteristics of 1000 amorphous IGZO TFT devices with different properties obtained through fully calibrated TCAD simulations, enabling flexible model parameter selection with high accuracy and fast SPICE simulation.

### 5.2 Automated Parameter Extraction

**Almeida and Fino (2025)** [18] demonstrated fully automatic evaluation of IGZO-TFT model parameters, reducing the labor-intensive manual fitting process that has been a major bottleneck in compact model deployment.

### 5.3 Review and Unified Frameworks

**Iniguez, Nathan, Kloes et al. (2021)** [23] provided a review of compact modeling solutions for organic and amorphous oxide TFTs integrated into industry standard simulation tools, discussing model validity and standardization challenges.

**Bestelink et al. (2020)** [17] developed compact source-gated transistor analog circuits in polysilicon and InGaZnO for ubiquitous sensors, demonstrating current mirrors with excellent copying performance.

### 5.4 Degradation and Reliability

**Kim, Seo, and Choi (2019)** [18b] proposed a TCAD degradation model for IGZO TFTs under high drain bias stress, using spatial distribution of physical parameters to model the oxygen vacancy mechanism.

## 6. Chronological Evolution

| Period    | Key Development                                                                                                                                                                   |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2008–2011 | First physics-based SPICE models via Verilog-A [3][4]; subgap density of states modeling                                                                                          |
| 2012–2013 | MOSFET SPICE Level=3 template adaptation [1]; double-gate models for displays [16]                                                                                                |
| 2014–2015 | Analytical physical models with trapped/free charges [2]; surface potential-based models [21]                                                                                     |
| 2017–2019 | RPI-aTFT extensions [12]; strain-aware flexible models [5]; oxide TFT Level 3 adaptation [8]; IGZO memristor models [10][19]                                                      |
| 2020–2021 | Dynamic AFCM simulation [13]; reliability-aware models [7]; unified TFT models for IoT [15]; review papers [23]                                                                   |
| 2022–2023 | IGZO memristor with oxygen content [9]; comprehensive noise models [11]                                                                                                           |
| 2024–2025 | HSPICE Level-61/62 comparison [6]; SOI/BSIM models [14][26]; neural compact models [24]; auto parameter extraction [18]; IGZO-DRAM TCAD-to-SPICE [20]; ferroelectric devices [25] |

## 7. Conclusion

Over the past 15 years, IGZO SPICE compact modeling has evolved from simple adaptations of silicon MOSFET templates to sophisticated physics-based, application-specific, and AI-augmented models. The field shows three clear trends: (1) increasing physical accuracy through surface potential and multi-trapping models; (2) expanding application scope from displays to DRAM, memristors, and ferroelectric devices; and (3) integration of machine learning for automated parameter extraction and neural compact models. Key open challenges include standardization of IGZO compact models across EDA tools, reliability modeling under combined electrical and mechanical stress, and scalable models for sub-100nm IGZO devices in BEOL integration.

## References

[1] C. Perumal, K. Ishida, R. Shabanpour, et al., "A Compact a-IGZO TFT Model Based on MOSFET SPICE Level=3 Template for Analog/RF Circuit Designs," _IEEE Electron Device Lett._, vol. 34, no. 11, pp. 1391–1393, 2013.

[2] M. Ghittorelli, F. Torricelli, L. Colalongo, and Z.M. Kovacs-Vajna, "Accurate Analytical Physical Modeling of Amorphous InGaZnO Thin-Film Transistors Accounting for Trapped and Free Charges," _IEEE Trans. Electron Devices_, vol. 61, no. 12, pp. 4105–4112, 2014.

[3] Y.W. Jeon, I.S. Hur, Y.S. Kim, M.K. Bae, et al., "Physics-Based SPICE Model of a-InGaZnO Thin-Film Transistor Using Verilog-A," _J. Semicond. Technol. Sci._, vol. 11, no. 3, pp. 153–161, 2011.

[4] D.H. Kim, Y.W. Jeon, S. Kim, Y. Kim, Y.S. Yu, et al., "Physical Parameter-Based SPICE Models for InGaZnO Thin-Film Transistors Applicable to Process Optimization and Robust Circuit Design," _IEEE Electron Device Lett._, vol. 33, no. 1, pp. 59–61, 2012.

[5] W.M.H. bin Wan Zaidi, J. Costa, et al., "Flexible IGZO TFT SPICE Model and Design of Active Strain-Compensation Circuits for Bendable Active Matrix Arrays," _IEEE Electron Device Lett._, vol. 39, no. 9, pp. 1314–1317, 2018.

[6] D. Dubey, M. Goswami, and K. Kandpal, "Adaptation and Comparative Analysis of HSPICE Level-61 and Level-62 Model for a-IGZO Thin Film Transistors," _Int. J. Numer. Model._, vol. 37, e3210, 2024.

[7] J.H. Kim, Y. Seo, J.T. Jang, S. Park, D. Kang, J. Park, et al., "Reliability-Aware SPICE Compatible Compact Modeling of IGZO Inverters on a Flexible Substrate," _Appl. Sci._, vol. 11, no. 11, p. 4838, 2021.

[8] K. Kandpal and N. Gupta, "Adaptation of a Compact SPICE Level 3 Model for Oxide Thin-Film Transistors," _J. Comput. Electron._, vol. 18, pp. 1023–1032, 2019.

[9] D. Kim, H.J. Lee, T.J. Yang, W.S. Choi, C. Kim, S.J. Choi, et al., "Compact SPICE Model of Memristor with Barrier Modulated Considering Short- and Long-Term Memory Characteristics by IGZO Oxygen Content," _Micromachines_, vol. 13, no. 10, p. 1630, 2022.

[10] J.T. Jang, J. Min, D. Kim, J. Park, S.J. Choi, D.M. Kim, et al., "A Highly Reliable Physics-Based SPICE Compact Model of IGZO Memristor Considering the Dependence on Electrode Metals and Deposition Sequence," _Solid-State Electron._, vol. 166, p. 107764, 2020.

[11] R. Vatsyayan and S.A. Dayeh, "A Comprehensive Large Signal, Small Signal, and Noise Model for IGZO Thin Film Transistor Circuits," _IEEE J. Electron Devices Soc._, 2023.

[12] R. Shabanpour, T. Meister, K. Ishida, et al., "A Transistor Model for a-IGZO TFT Circuit Design Built Upon the RPI-aTFT Model," in _Proc. IEEE Int. Conf. Electron Devices Solid-State Circuits (EDSSC)_, 2017.

[13] Y. Hernandez-Barrios, J.N. Gaspar-Angeles, M. Estrada, B. Iniguez, and A. Cerdeira, "Dynamic Simulation of a-IGZO TFT Circuits Using the Analytical Full Capacitance Model (AFCM)," _IEEE J. Electron Devices Soc._, vol. 9, pp. 110–117, 2020.

[14] X.J. Liu, D. Verity, A. Sou, and T. Gneiting, "Application of SOI Compact Model to a-IGZO Technology," in _Proc. IEEE Int. Flexible Electronics Technology Conf. (IFETC)_, pp. 1–3, 2024.

[15] L. Shao, T. Lei, T.C. Huang, S. Li, T.Y. Chu, et al., "Compact Modeling of Thin-Film Transistors for Flexible Hybrid IoT Design," _IEEE Trans. Electron Devices_, vol. 66, no. 9, pp. 3817–3824, 2019.

[16] G. Baek and J. Kanicki, "Modeling of Current-Voltage Characteristics for Double-Gate a-IGZO TFTs and Its Application to AMLCDs," _J. Soc. Inf. Display_, vol. 20, no. 5, pp. 237–244, 2012.

[17] E. Bestelink, K.M. Niang, G. Bairaktaris, L. Maiolo, et al., "Compact Source-Gated Transistor Analog Circuits for Ubiquitous Sensors," _IEEE Sensors J._, vol. 20, no. 22, pp. 13484–13493, 2020.

[18] C. Almeida and M.H. Fino, "Fully Automatic Evaluation of IGZO-TFT Model Parameters," in _Proc. YEF-ECE_, pp. 169–174, 2025.

[19] D. Saha, A. Mandal, M. Kar, D. Ghosal, S. Bhattacharya, and A. Kundu, "SPICE Compact Model of IGZO Memristor Based on Non-Quasi Statically Updated Schottky Barrier Height," in _Proc. IEEE Int. Conf. Nanotechnol. (NANO)_, 2019.

[20] "Surface Potential-Based Compact Model for IGZO-DRAM Enables the TCAD-to-SPICE Framework for Reliability-Aware DTCO Flow," in _Proc. IEEE EDTM_, 2025.

[21] "A New Surface Potential-Based Compact Model for a-IGZO TFTs in RFID Applications," 2015.

[22] "Physics-Based α-IGZO TFTs Compact Modeling and Neural Network Application with 2T0C DRAM Cell," _IEEE Access_, 2025.

[23] B. Iniguez, A. Nathan, A. Kloes, et al., "New Compact Modeling Solutions for Organic and Amorphous Oxide TFTs," _IEEE J. Electron Devices Soc._, vol. 9, pp. 604–613, 2021.

[24] S. Eom, H. Yun, H. Jang, K. Cho, S. Lee, et al., "Neural Compact Modeling Framework for Flexible Model Parameter Selection with High Accuracy and Fast SPICE Simulation," _Adv. Intell. Syst._, vol. 6, 2300435, 2024.

[25] M. Rafiq, M.S. Nazir, A. Naseer, Y.S. Chauhan, and S. Sahay, "A SPICE-Compatible Compact Model of Ferroelectric Diode (BE/HZO/IGZO/TE)," _IEEE J. Exploratory Solid-State Comput. Devices Circuits_, 2025.

[26] "An All-Region BSIM Thin-Film Transistor Model for Display and BEOL 3-D Integration Applications," _IEEE Electron Device Lett._, 2024.
