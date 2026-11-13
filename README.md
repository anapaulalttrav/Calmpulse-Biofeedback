# 🫀 CalmPulse — Biofeedback Acessível para Saúde Mental

<p align="center">
  <img src="https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow" alt="Status">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/ODS-3%20(Saúde%20e%20Bem--Estar)-blue" alt="ODS 3">
  <img src="https://img.shields.io/badge/Hardware-Arduino%20%7C%20ESP32-red" alt="Hardware">
  <img src="https://img.shields.io/badge/Institution-FMU-purple" alt="FMU">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino">
  <img src="https://img.shields.io/badge/ESP32-00979D?style=for-the-badge&logo=espressif&logoColor=white" alt="ESP32">
  <img src="https://img.shields.io/badge/Health-❤️-red?style=for-the-badge" alt="Saúde">
  <img src="https://img.shields.io/badge/Open%20Source-✅-brightgreen?style=for-the-badge" alt="Open Source">
</p>

---

## 📖 Sobre o Projeto

O **CalmPulse** é um dispositivo de **biofeedback de baixíssimo custo** desenvolvido para monitoramento e intervenção breve em quadros de **ansiedade aguda e estresse**. O sistema utiliza sensores fisiológicos para detectar picos de estresse e aciona automaticamente um protocolo de **respiração guiada (técnica 4-7-8)** com feedback visual (LEDs) e tátil (vibração).

O projeto é **open-source**, está alinhado ao **ODS 3 — Saúde e Bem-Estar** da ONU.

🎯 **Objetivo principal:** Democratizar o acesso à tecnologia de biofeedback, hoje restrita a equipamentos clínicos que custam mais de **R$ 5.000**.

---

## 🧠 Fundamentação Científica

### 1. Ansiedade, Crise de Pânico e Batimentos Cardíacos

A relação entre ansiedade e elevação da frequência cardíaca é amplamente documentada na literatura científica. Durante uma crise de ansiedade ou pânico, o **Sistema Nervoso Simpático** é ativado, resultando em taquicardia, sudorese e hiperventilação.

> *"A taquicardia é um dos sintomas fisiológicos mais prevalentes durante crises de ansiedade e pânico, sendo um marcador objetivo da ativação do eixo simpático-adrenal."*
> — **American Psychological Association (APA), 2022**

**Referências científicas:**
- 📄 **APA (2022)** — *Diagnostic and Statistical Manual of Mental Disorders (DSM-5-TR)*. American Psychiatric Association. [Link](https://doi.org/10.1176/appi.books.9780890425787)
- 📄 **Conrad, A. et al. (2007)** — *Cardiac and respiratory patterns during panic attacks*. Biological Psychology, 74(2), 241-249. [Link](https://doi.org/10.1016/j.biopsycho.2006.09.005)
- 📄 **Meuret, A. E. et al. (2011)** — *Hyperventilation in panic disorder and asthma: empirical evidence and clinical implications*. International Journal of Psychophysiology, 78(1), 68-79. [Link](https://doi.org/10.1016/j.ijpsycho.2010.05.006)

### 2. Biofeedback e Respiração Guiada (Técnica 4-7-8)

O biofeedback é reconhecido pela **Associação Americana de Psicologia (APA)** como uma intervenção baseada em evidências para ansiedade. A técnica de respiração **4-7-8** (inspirar 4s, segurar 7s, expirar 8s) ativa o **Sistema Nervoso Parassimpático**, reduzindo a frequência cardíaca e promovendo regulação emocional.

> *"Intervenções de biofeedback respiratório demonstraram eficácia significativa na redução de sintomas de ansiedade e na regulação da variabilidade da frequência cardíaca (HRV)."*
> — **Lehrer, P. M. et al. (2020)** — *Heart Rate Variability Biofeedback: How and Why Does It Work?*

**Referências científicas:**
- 📄 **Lehrer, P. M. et al. (2020)** — *Heart Rate Variability Biofeedback*. Frontiers in Psychology, 11, 1845. [Link](https://doi.org/10.3389/fpsyg.2020.01845)
- 📄 **Zaccaro, A. et al. (2018)** — *How Breath-Control Can Change Your Life: A Systematic Review on Psycho-Physiological Correlates of Slow Breathing*. Frontiers in Human Neuroscience, 12, 353. [Link](https://doi.org/10.3389/fnhum.2018.00353)
- 📄 **Goessl, V. C. et al. (2017)** — *The effect of heart rate variability biofeedback training on stress and anxiety: a meta-analysis*. Psychological Medicine, 47(15), 2578-2586. [Link](https://doi.org/10.1017/S0033291717001003)

### 3. SpO2 como Ferramenta de Reestruturação Cognitiva

Um dos diferenciais do CalmPulse é o uso da **oxigenação sanguínea (SpO2)** como âncora terapêutica. Durante crises de pânico, a SpO2 permanece estável (97-99%), mesmo com a sensação subjetiva de falta de ar. Mostrar esse dado em tempo real funciona como **reestruturação cognitiva**: *"Meu corpo está oxigenado, estou seguro, é apenas adrenalina."*

---

## 🏗️ Arquitetura do Sistema

O CalmPulse foi arquitetado seguindo um modelo de **Sistemas Embarcados de Tempo Real**, dividido em três camadas principais: Aquisição Fisiológica, Processamento Lógico e Feedback Multissensorial.

### 📊 High-Level Data Flow
```text
[ Paciente ] 
    │ (Dados Fisiológicos)
    ▼
🟢 BioCapture Array (Sensores) ──► 🟡 CorePulse Logic (MCU) ──► 🔵 CalmSync Actuators (Atuadores)
    (MAX30100)               (Arduino UNO)         (LEDs + Vibração + OLED)

