# 🛰️ AGV Intelligent Traffic Control System (Fuzzy + Gemini AI)

## 1. Identificação do Grupo
* **Instituição:** Fundação Salvador Arena (FTT)
* **Curso:** Engenharia de Controle e Automação
* **Grupo:** Grupo 05
* **Integrantes:**
    * Bruno Eduardo
    * Rafael Bognar Soares da Silva
    * João Soares
    * William Balieiro

## 2. Área Problema Selecionada
* [x] **Logística Autônoma: Coordenação de AGVs e Otimização de Rotas**

---

## 3. Diagnóstico e Definição do Agente
Nesta etapa (Milestone 2), o projeto evoluiu de um diagnóstico teórico para um **modelo computacional funcional**. O agente agora processa telemetria em tempo real e justifica suas ações via IA Generativa.

* **Contexto:** Logística industrial 4.0 e controle dinâmico de tráfego de AGVs.
* **Problema:** Ineficiência de sistemas de tráfego rígidos que não consideram variáveis contínuas (velocidade/distância).
* **Solução:** Um sistema híbrido que utiliza **Lógica Fuzzy** para decisão instantânea e a **API do Gemini** para análise preditiva.

### Modelagem PEAS
| Componente | Descrição |
| :--- | :--- |
| **Performance (P)** | Zero colisões, redução de tempo de espera e preservação da vida útil dos componentes. |
| **Ambiente (E)** | Cruzamento industrial simulado com suporte a telemetria dinâmica. |
| **Atuadores (A)** | Semáforo inteligente (Verde/Amarelo/Vermelho) e Sistema de Alerta de Manutenção. |
| **Sensores (S)** | Distância (LiDAR), Velocidade (Encoder) e Prioridade da Carga (RFID/TAG). |

---

## 4. Arquitetura do Sistema

O motor de decisão do agente é composto por duas camadas:

### A. Camada de Decisão (Lógica Fuzzy)
Utilizamos a biblioteca `scikit-fuzzy` para processar a incerteza dos sensores:
* **Fuzzificação:** Conversão de valores reais em conjuntos nebulosos (*Perto, Médio, Longe* / *Baixa, Alta*).
* **Inferência:** Base de regras especialistas que cobrem 100% dos cenários possíveis.
* **Defuzzificação:** Geração do valor de Urgência (0 a 100%) via método do centroide.

### B. Camada de Interpretação e Manutenção (Gemini AI)
A API do **Gemini 2.5 Flash** recebe os outputs do motor Fuzzy e gera:
1.  **Análise de Segurança:** Explicação física do porquê da decisão (cinemática e risco).
2.  **Diagnóstico de Desgaste:** Estimativa de estresse em freios e pneus baseada no perfil de condução.
3.  **Protocolo Preditivo:** Sugestões de calibração de sensores e trocas de componentes.

---

## 5. Dashboard Interativo
O projeto implementa um Dashboard de alta performance no Google Colab:
* **Sliders Dinâmicos:** Controle manual de Distância, Velocidade e Prioridade.
* **Superfície de Decisão 3D:** Visualização do gradiente de risco em tempo real.
* **Otimização por Cache:** Renderização instantânea para garantir responsividade total (sem lag).

---

## 6. Estrutura do Repositório
```text
/
├── notebooks/
│   └── controle_agv_fuzzy_gemini.ipynb  # Notebook principal (Código Fonte)
├── docs/
│   ├── funcoes_pertinencia.png           # Gráficos da arquitetura Fuzzy
│   └── mapa_decisao_3d.png              # Screenshot da superfície de risco
├── README.md                            # Documentação Completa
└── requirements.txt                     # Dependências do projeto
```
---

## 7. Instruções para Execução

* Acesse o notebook na pasta '/notebooks' via Google Colab.
* Insira sua CHAVE_API do Google AI Studio na seção de configuração.
* Vá em Ambiente de Execução > Executar Tudo.

Utilize os sliders para simular cenários e clique no botão "Gerar Análise Profunda" para obter o relatório da IA.

---

### 📊 Evidências de Testes

| Cenário 1 | Cenário 2 | Cenário 3 | Cenário 4 | Cenário 5 |
| :---: | :---: | :---: | :---: | :---: |
| ![C1](Docs/1.png) | ![C2](Docs/2.png) | ![C3](Docs/3.png) | ![C4](Docs/4.png) | ![C5](Docs/5.png) |

---
### 📦 Bibliotecas e Dependências

| Biblioteca | Versão | Função no Projeto |
| :--- | :---: | :--- |
| `numpy` | `< 2.0` | Processamento matemático e suporte a matrizes (essencial para o motor Fuzzy). |
| `scikit-fuzzy` | Atual | Implementação da Lógica Nebulosa (Fuzzificação, Regras e Defuzzificação). |
| `google-generativeai`| Atual | Integração com o Gemini AI para geração de relatórios e análise preditiva. |
| `matplotlib` | Atual | Geração de gráficos 2D e da superfície de decisão 3D. |
| `ipywidgets` | Atual | Criação dos elementos interativos do Dashboard (sliders e botões). |


##  Etapa 3: Inteligência Evolutiva e Preditiva
**Abordagem Escolhida:** Redes Neurais Artificiais (RNA).

**Justificativa:** Implementamos uma rede neural do tipo MLP (Multi-Layer Perceptron) para que o agente pudesse aprender com o histórico de operações. Enquanto a lógica Fuzzy (Etapa 2) atua como um sistema especialista rígido, a RNA permite prever níveis de urgência com base em padrões complexos identificados no treinamento, permitindo uma tomada de decisão mais fluida e adaptativa.

**Métricas de Desempenho:**
* Utilizado o gráfico de **Loss Curve** para demonstrar a convergência do aprendizado.
* O modelo atingiu uma acurácia (R²) superior a 95% na simulação de cenários de risco.

**Fluxo de Dados:**
Sensores -> Rede Neural (Predição) -> Comparação com Lógica Fuzzy -> Relatório Gemini.
