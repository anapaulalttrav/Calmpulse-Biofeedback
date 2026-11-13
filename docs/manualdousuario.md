# 📘 Manual do Usuário — CalmPulse

> **Importante:** O CalmPulse é um protótipo educacional da FMU, desenvolvido no âmbito de um projeto de extensão universitária. Ele **não substitui** acompanhamento psicológico ou psiquiátrico.

---

## 🎯 Para Quem É Este Manual?

- Voluntários do piloto clínico
- Estudantes de Psicologia que aplicarão a intervenção
- Usuários finais que desejam treinar respiração guiada
- Integrantes da equipe técnica que montarão o hardware

---

## 📊 Status Atual do Projeto

O CalmPulse está em desenvolvimento iterativo. Este manual reflete a **Fase 1 (atual)**. As fases futuras estão sinalizadas ao longo do documento.

| Fase | Componente | Status |
|---|---|---|
| **Fase 1 (Atual)** | MAX30100 (BPM + SpO2) | ✅ Funcionando |
| **Fase 1 (Atual)** | Conversor de nível lógico | ✅ Funcionando |
| **Fase 1 (Atual)** | Arduino Uno | ✅ Funcionando |
| **Fase 1 (Atual)** | Painel Web (respiração na tela) | ✅ Funcionando |
| **Fase 2 (Futura)** | Sensor GSR | 🚧 Em desenvolvimento |
| **Fase 3 (Futura)** | Anel NeoPixel (LEDs) | 📅 Planejado |
| **Fase 3 (Futura)** | Motor de vibração | 📅 Planejado |
| **Fase 3 (Futura)** | Display OLED 0.96" | 📅 Planejado |

> 💡 **Nota:** Na Fase 1, a respiração guiada (4-7-8) é exibida **no painel web** (tela do computador/celular), pois os atuadores físicos (LEDs e vibração) ainda estão em fase de integração.

---

## 📦 Itens Necessários

### ✅ Atuais (Fase 1)
- 1x Módulo MAX30100
- 1x Conversor de nível lógico bidirecional (4 canais)
- 1x Arduino Uno
- 1x Protoboard + jumpers
- 1x Cabo USB (dados + energia)

### 📅 Futuros (Fases 2 e 3)
- 1x Sensor GSR (Resposta Galvânica da Pele)
- 1x Anel NeoPixel (16 LEDs)
- 1x Motor de vibração + transistor 2N2222 + diodo 1N4007
- 1x Display OLED 0.96" I2C

---

## 🔌 Como Montar o Dispositivo (Fase 1)

### Passo 1: Conectar o Conversor de Nível Lógico
- **HV** → 5V do Arduino Uno
- **LV** → 3,3V do Arduino Uno
- **GND** → GND comum

### Passo 2: Conectar o MAX30100
- **VIN** → 3,3V (saída LV do conversor)
- **GND** → GND
- **SDA** → Canal 1 do conversor (que vai ao **A4** do Arduino Uno)
- **SCL** → Canal 2 do conversor (que vai ao **A5** do Arduino Uno)

> ⚡ **Por que o conversor?** O MAX30100 opera com lógica de 1,8V. Ligado diretamente ao Arduino Uno (5V), a comunicação I2C não é reconhecida.

### Passo 3: Alimentação Segura
- ⚠️ **Nunca** use o Arduino conectado à tomada enquanto o sensor está em contato com a pele.
- Use power bank ou notebook **desconectado da tomada**.

### 📅 Passo 4 (Futuro): Conectar os Atuadores
> *Aguardando Fase 3.* Quando o NeoPixel, o motor e o OLED forem integrados, as ligações serão:
> - **NeoPixel DIN** → D6 (com resistor 330Ω)
> - **Motor de vibração** → D5 (via transistor)
> - **OLED SDA/SCL** → A4/A5 (mesmo barramento I2C)

---

## 🚀 Como Usar (Fase 1)

### 1. Inicialização
Conecte o Arduino Uno ao computador e abra o **Painel Web** (`web-simulation/index.html` no Chrome/Edge).

### 2. Calibração (30 segundos)
- Posicione o dedo indicador sobre o MAX30100
- Fique sentado, em silêncio, sem mexer a mão
- Aguarde a mensagem "Linha de base calibrada"

### 3. Monitoramento
O painel exibirá em tempo real:
- **BPM** (Frequência Cardíaca)
- **SpO2** (Oxigenação)

> 📅 *Na Fase 2, o painel também exibirá o Índice de Estresse (0-100) calculado com o sensor GSR.*

### 4. Respiração Guiada (via Tela)
Clique em **"Iniciar Respiração Guiada"** no painel web e siga o LED virtual na tela:
- 🔵 **Azul (Inspire 4s):** o círculo expande
- 🟣 **Roxo (Segure 7s):** o círculo permanece cheio
- 🟢 **Verde (Expire 8s):** o círculo contrai

> 📅 *Na Fase 3, esse mesmo ritmo será reproduzido pelos LEDs físicos (NeoPixel) e pela vibração.*

### 5. Reavaliação
Após 4 ciclos, observe seus sinais no painel para confirmar a melhora (BPM tendendo a baixar).

---

## 💡 Dica de Grounding (Reestruturação Cognitiva)

> *"Se você sente falta de ar, mas a SpO2 está entre 97-99%, seu corpo está oxigenado. Isso é apenas adrenalina. Você está seguro."*

---

## ⚠️ Contraindicações

**NÃO use o CalmPulse se você:**
- Tem doença cardíaca, arritmia ou usa marca-passo
- Está grávida (consulte seu médico antes)
- Tem asma, DPOC ou doença respiratória
- Tem episódios frequentes de tontura ou desmaio
- Está em crise de ansiedade intensa no momento

---

## 🆘 Troubleshooting Rápido

| Problema | Solução |
|---|---|
| SpO2 sempre 0 | Pressione o dedo com mais firmeza |
| BPM muito alto | Afaste o dedo — pode estar captando luz ambiente |
| Comunicação I2C falha | Confirme HV=5V e LV=3,3V no conversor |
| Sensor não é reconhecido | Verifique SDA=A4 e SCL=A5 no Arduino Uno |

> 📅 *Na Fase 3, serão adicionados itens de troubleshooting para NeoPixel, motor e OLED.*

---

## 📅 Roadmap — Próximas Fases

| Fase | Objetivo | Previsão |
|---|---|---|
| **Fase 2** | Integrar sensor GSR e cálculo do Índice de Estresse | Dezembro 2026 |
| **Fase 3** | Integrar NeoPixel, motor de vibração e OLED | Janeiro 2027 |
| **Piloto** | Aplicação clínica com voluntários (Psicologia FMU) | Fevereiro 2027 |
| **1.0.0** | Relatório técnico e artigo científico | Junho 2027 |

---

## 📞 Suporte Acadêmico

Para dúvidas sobre o projeto, entre em contato com a equipe do CalmPulse ou através dos orientadores:

- **Prof. Roberto Pallesi** (FMU)
- **Prof.ª Silvia Fiacador** (FMU)

---

> 🌊 **CalmPulse** — *"Do código à calma: tecnologia acessível a serviço da saúde mental."*