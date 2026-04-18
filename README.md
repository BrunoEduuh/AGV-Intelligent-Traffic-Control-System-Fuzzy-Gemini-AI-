# 🛰️ AGV Intelligent Traffic Control System (Fuzzy + Gemini AI)

## 📌 Descrição do Projeto
Este projeto implementa um sistema de controle de tráfego para Veículos Autônomos (AGVs) em cruzamentos industriais. O sistema utiliza **Lógica Fuzzy** para tomar decisões em ambientes de incerteza e a **API do Gemini 2.5 Flash** para realizar análises interpretativas e diagnósticos de manutenção preditiva.

## 🧠 Arquitetura Lógica

### 1. Entradas (Sensores)
* **Distância (0-50m):** Proximidade do AGV em relação ao cruzamento.
* **Velocidade (0-5m/s):** Velocidade atual de aproximação.
* **Prioridade (1-10):** Nível de criticidade da carga transportada.

### 2. Processamento (Motor Fuzzy)
O sistema utiliza o motor de inferência de Mamdani para calcular a **Urgência de Passagem (0-100%)**. 


**Regras de Inferência Principais:**
* SE distância é PERTO OU velocidade é ALTA, ENTÃO urgência é ALTA.
* SE distância é MÉDIA E prioridade é ALTA, ENTÃO urgência é ALTA.
* SE distância é LONGE E velocidade é BAIXA, ENTÃO urgência é BAIXA.

### 3. Análise Interpretativa (IA Gerativa)
O output do sistema Fuzzy é enviado para o **Google Gemini**, que atua como um Engenheiro Especialista, gerando:
* Explicação técnica do nível de risco.
* Diagnóstico de desgaste de componentes (freios e pneus).
* Sugestões estratégicas de manutenção.

## 📊 Exemplos de Logs de Saída

### Cenário 1: Aproximação Crítica
* **Dados:** Distância: 5m | Velocidade: 4.5m/s | Prioridade: 10
* **Fuzzy:** Urgência de 92.4% (Sinal Vermelho)
* **Gemini:** "Risco iminente de colisão. A energia cinética elevada em curta distância exige frenagem de emergência. Recomendado check-up imediato nas pastilhas de freio."

### Cenário 2: Fluxo Normal
* **Dados:** Distância: 40m | Velocidade: 2.0m/s | Prioridade: 3
* **Fuzzy:** Urgência de 24.1% (Sinal Verde)
* **Gemini:** "Operação dentro dos parâmetros de segurança. Desgaste mecânico nominal."
