# InterCoder

Ferramenta web para análise de **confiabilidade entre codificadores** em projetos de análise de conteúdo. Calcula o **alpha de Krippendorff** e o coeficiente de **Brennan-Prediger** diretamente no navegador — sem instalação, sem servidor, sem que seus dados saiam do computador.

**[▶ Abrir o app](https://SEU-USUARIO.github.io/intercoder/)**

---

## O que faz

- Carrega múltiplos arquivos CSV (um por codificador) via drag-and-drop
- Detecta automaticamente o tipo de cada variável (binária, numérica, categórica, texto)
- Gera e testa **todas as combinações possíveis** de codificadores
- Exibe tabela colorida com alpha de Krippendorff, Brennan-Prediger, concordância bruta e % positivo
- Alerta automaticamente para variáveis com prevalência baixa (< 15%), que tendem a subestimar o alpha
- Gera gráfico de barras com linha de referência em 0.667
- Exporta resultados em CSV

## Métricas calculadas

| Métrica | Descrição |
|---------|-----------|
| **Alpha de Krippendorff** | Confiabilidade nominal ajustada por chance via matriz de coincidência |
| **Brennan-Prediger** | Alternativa ao alpha que usa chance fixa (1/k); menos sensível ao paradoxo da prevalência |
| **Concordância bruta** | % de unidades em que **todos** os codificadores da combinação concordaram |
| **% Positivo** | Prevalência da categoria positiva; valores < 15% geram aviso |

### Quando usar Brennan-Prediger?

Quando uma variável binária tem prevalência muito baixa (poucas marcações positivas), o alpha de Krippendorff pode ser artificialmente baixo — mesmo que os codificadores concordem na prática. Nesses casos, o Brennan-Prediger (que usa probabilidade de chance fixa = 1/k) é uma medida mais informativa.

---

## Formato dos arquivos CSV

- Um arquivo por codificador
- Todos os arquivos devem conter as **mesmas colunas de codificação** (nomes idênticos)
- Colunas de metadados (ID, data, texto, links) podem estar presentes — o usuário as desmarca na tela de configuração
- Variáveis binárias: valores `TRUE`/`FALSE`, `0`/`1`, ou `Sim`/`Não`
- Variáveis categóricas: strings de texto (ex: `Positivo`, `Negativo`, `Neutro`)
- Encoding recomendado: UTF-8

---

## Hospedar no GitHub Pages (fork em 2 minutos)

1. **Faça um fork** deste repositório clicando em **Fork** no canto superior direito
2. No repositório forkado, vá em **Settings → Pages**
3. Em **Source**, selecione `Deploy from a branch`
4. Em **Branch**, escolha `main` e a pasta `/ (root)`
5. Clique em **Save**
6. Aguarde ~1 minuto. O app estará disponível em `https://SEU-USUARIO.github.io/NOME-DO-REPO/`

O app é um único arquivo `index.html` — não há build, não há dependências para instalar.

---

## Usar localmente (sem internet)

```bash
# Com Python (qualquer versão moderna):
python3 -m http.server 8080
# Abra http://localhost:8080 no navegador

# Com Node.js:
npx serve .
```

> **Atenção:** abrir `index.html` diretamente como `file://` pode bloquear o carregamento dos scripts CDN em alguns navegadores. Use um servidor local.

---

## Privacidade

Os dados dos CSVs **nunca saem do seu computador**. Todo o processamento ocorre no JavaScript do navegador. Não há servidor, não há telemetria, não há cookies de rastreamento.

---

## Referências

- Krippendorff, K. (2004). *Content Analysis: An Introduction to Its Methodology* (2nd ed.). Sage.
- Brennan, R. L., & Prediger, D. J. (1981). Coefficient kappa: Some uses, misuses, and alternatives. *Educational and Psychological Measurement, 41*(3), 687–699.
- Zapf, A. et al. (2016). Measuring inter-rater reliability for nominal data — which coefficients and confidence intervals are appropriate? *BMC Medical Research Methodology, 16*, 93.
