# 🔬 Guia Técnico: Sensor MAX30100

> **Projeto:** CalmPulse – Biofeedback Acessível para Saúde Mental  
> **Instituição:** FMU – Bacharelado em Ciência da Computação  
> **ODS:** 3 – Saúde e Bem-Estar

---

## 📑 Índice

1. [Introdução](#1-introdução)
2. [Anatomia Circulatória](#2-anatomia-circulatória)
3. [Princípio da PPG](#3-princípio-da-fotopletismografia-ppg)
4. [Especificações Técnicas](#4-especificações-técnicas)
5. [Pinout e Conversor de Nível Lógico](#5-pinout-e-conversor-de-nível-lógico)
6. [Biblioteca MAX30100lib](#6-biblioteca-max30100lib)
7. [Código de Referência](#7-código-de-referência)
8. [Troubleshooting](#8-troubleshooting)

---

## 1. Introdução

O **MAX30100** é um módulo integrado de oximetria e batimento cardíaco. Combina LEDs (vermelho e infravermelho), fotodetector e conversor ADC em um único chip.

> ⚠️ **Atenção Técnica:** O MAX30100 opera com lógica de **1,8V**, enquanto o Arduino Nano trabalha com **5V**. O CalmPulse utiliza um **conversor de nível lógico bidirecional** para comunicação I2C segura.

---

## 2. Anatomia Circulatória

| Propriedade | 🩸 Veias | ❤️ Artérias |
|---|---|---|
| Sentido de circulação | Dos tecidos ao coração | Do coração ao corpo |
| Oxigenação | Pobre em O₂ (desoxihemoglobina) | Rica em O₂ (oxihemoglobina) |
| Espessura da parede | Pouco espessa | Muito espessa |
| Pressão | Menor | Maior |
| Absorção de luz predominante | **Luz vermelha** (~660 nm) | **Luz infravermelha** (~940 nm) |

---

## 3. Princípio da PPG

A fotopletismografia mede variações no volume sanguíneo através da absorção de luz. O algoritmo calcula:

$$
R = \frac{AC_{red}/DC_{red}}{AC_{IR}/DC_{IR}} \quad \Rightarrow \quad SpO2 = A - B \cdot R
$$

---

## 4. Especificações Técnicas

| Parâmetro | Valor |
|---|---|
| Tensão de alimentação | 2,94V a 3,6V |
| Consumo em operação | < 600 µA |
| LEDs | Vermelho (660 nm) + IR (940 nm) |
| Corrente dos LEDs | 0 mA a 50 mA (configurável) |
| Faixa SpO2 | 50% a 100% |
| Faixa BPM | 30 a 250 bpm |
| Interface | I2C |

---

## 5. Pinout e Conversor de Nível Lógico

### Pinout do MAX30100

| Pino | Função |
|---|---|
| **VIN** | Alimentação (3,3V ou 5V) |
| **GND** | Terra |
| **SDA** | Dados I2C |
| **SCL** | Clock I2C |
| **INT** | Interrupção (opcional) |

### 📡 Esquema com Conversor Bidirecional

```text
Arduino Nano          Conversor 5V↔3V3       MAX30100
─────────────         ─────────────────       ────────
     5V ─────────────► HV                     
    GND ─────────────► GND ──────────────────► GND
     A4 ─────────────► SDA1 ─────────────────► SDA
     A5 ─────────────► SCL1 ─────────────────► SCL
                    LV ◄──── 3,3V ────────────► VIN