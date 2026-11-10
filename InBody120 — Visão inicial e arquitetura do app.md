# InBody120 — Visão inicial e arquitetura do app

Oct 28, 2026 · @João Serafini

Li 1 relatório **InBody120** real no seu PC e, agora, os 3 laudos mais antigos direto do Google Drive (nov/2025, fev e jun/2026). Os dados medidos são **fato observado**; a dinâmica ao longo do tempo é **hipótese** e está sinalizada como tal.

## Evolução — 3 exames (nov/2025 → jun/2026)

Os 3 laudos mostram uma **recomposição corporal real**: peso e gordura caíram de forma consistente e o IMC saiu de sobrepeso (26,4) para a faixa normal (24,1). O ponto de atenção é a **massa muscular**, que caiu \~1,7 kg entre nov e fev e só recuperou parte depois.

&#91;embedded content: 3 laudos InBody120 do Drive · nov/2025 a jun/2026\]

**Índices ao longo dos 3 exames**

| Indicador | Nov/25 | Fev/26 | Jun/26 | Referência |
| --- | --- | --- | --- | --- |
| % Gordura (PGC) | 28,3 | 26,8 | 25,2 | — |
| IMC | 26,4 | 24,3 | 24,1 | 18,5–25,0 |
| Gordura visceral (nível) | 10 | 8 | a confirmar | ≤ 9 |
| Cintura-quadril (WHR) | 0,92 | 0,88 | 0,87 | ≤ 0,90 |
| Taxa metabólica basal (kcal) | 1619 | 1544 | 1564 | — |
| Pontuação InBody | 67 | 67 | 69 | — |

**Fato × lacuna:** o nível de **gordura visceral do 3º exame saiu ilegível no OCR** — um exemplo real do fluxo que você props: o app marcaria esse campo como faltante e pediria para você digitar. Todos os outros campos foram lidos e as somas conferem.

> Base: 3 laudos do Drive (`2025-11-21`, `2026-02-24`, `2026-06-15`). O 4º (`2026-10-22`) entra quando você quiser e vira o 4º ponto das curvas.

## Acesso aos dados (resolvido)

**Fato observado.** Os 3 laudos mais antigos ficavam no Google Drive. O connector agora está conectado e eu li os 3 direto da pasta (titular confirmado: Maurício Barros). No projeto só vieram 3 imagens — que são screenshots das suas próprias instruções, não dados de exame.

**O que consegui ler.** Pelo seu computador vinculado (`pc-mau-raizen`) localizei e li 1 laudo InBody120 real, que uso como amostra fiel do formato:

| Item | Valor |
| --- | --- |
| Arquivo | `06012026_2025-11-21-Bioimpedância.pdf` |
| Local | `Documents\Docs_Pessoais_Digitalizados\Maurício\Exames Médicos\Nutricionista-Dra.Hewelyn\` |
| Pessoa / ID | MAURICIO DA SI… · ID 211125-1 |
| Data do exame | 21/11/2025 06:59 |
| Equipamento | InBody120 (software LookinBody120 5.0.0.0) |

Para avançar, preciso de uma destas opções (qualquer uma serve):

1. Habilitar o connector do Google Drive na sua conta claude.ai (eu leio os 3 arquivos direto da pasta);
2. Anexar aqui os 3 PDFs mais antigos; ou
3. Baixar os 3 PDFs para uma pasta do PC (ex.: a mesma `Exames Médicos`) e me avisar — eu já tenho acesso às suas pastas `Downloads` e `Documents`.

> Observação: o laudo que li é do Maurício. Confirme se o acompanhamento é dele ou seu — isso define de quem são as 3 medições iniciais.

## Parte 1 — O que o arquivo contém

Cada laudo InBody120 é **uma folha A4, uma única medição** de um instante. É um documento estruturado em blocos fixos — ou seja, dá para transformar em um registro de banco de dados com campos previsíveis. Os valores abaixo são **fatos observados** da amostra de 21/11/2025.

**Identificação e metadados do laudo**

| Campo | Valor na amostra |
| --- | --- |
| ID | 211125-1 |
| Nome | MAURICIO DA SI… (truncado no laudo) |
| Altura | 175 cm |
| Idade | 68 |
| Sexo | Masculino |
| Data / Hora | 21/11/2025 06:59 |
| Equipamento / versão | InBody120 · LookinBody120 5.0.0.0 · S/N F325000182 |

**Métricas principais** (valor medido e a faixa de referência que o próprio laudo imprime para o perfil da pessoa)

| Bloco | Campo | Sigla | Valor | Faixa de referência |
| --- | --- | --- | --- | --- |
| Composição | Água Corporal Total | TBW | 42,4 L | 37,9–46,3 |
| Composição | Proteína | — | 11,3 kg | 10,2–12,4 |
| Composição | Minerais | — | 4,16 kg | 3,50–4,28 |
| Composição | Massa de Gordura | BFM | 22,8 kg | 8,1–16,2 |
| Composição | Peso | — | 80,7 kg | 57,3–77,5 |
| Obesidade | IMC | BMI | 26,4 kg/m² | 18,5–25,0 |
| Obesidade | Percentual de Gordura | PGC/PBF | 28,3 % | — |
| Músculo | Massa Muscular Esquelética | SMM | 32,1 kg | 28,8–35,2 |
| Músculo | Massa Livre de Gordura | FFM | 57,9 kg | 51,5–63,0 |
| Metabolismo | Taxa Metabólica Basal | TMB/BMR | 1619 kcal | 1703–1999 |
| Risco | Relação Cintura-Quadril | WHR | 0,92 | 0,80–0,90 |
| Risco | Nível de Gordura Visceral | VFL | 10 | 1–9 |
| Resumo | Grau de Obesidade | — | 120 % | 90–110 |
| Resumo | Pontuação InBody | — | 67 / 100 | — |

**Controle sugerido** (metas que o aparelho calcula): Peso ideal 68,1 kg · Controle de Peso −12,6 kg · Controle de Gordura −12,6 kg · Controle Muscular 0,0 kg.

**Análise segmentar** — massa magra e gordura por região do corpo, cada uma com valor, % do ideal e classificação (Abaixo / Normal / Acima):

| Segmento | Massa magra | Classe | Gordura | Classe |
| --- | --- | --- | --- | --- |
| Braço esquerdo | 3,16 kg (99,1%) | Normal | 1,5 kg (252,8%) | Acima |
| Braço direito | 3,24 kg (101,6%) | Normal | 1,5 kg (244,6%) | Acima |
| Tronco | 25,5 kg (95,9%) | Normal | 12,4 kg (289,6%) | Acima |
| Perna esquerda | 8,72 kg (89,6%) | Abaixo | 3,1 kg (180,3%) | Acima |
| Perna direita | 8,50 kg (87,3%) | Abaixo | 3,1 kg (180,0%) | Acima |

**Dado bruto de impedância** — o laudo ainda traz a matriz Z(Ω) por segmento (BD, BE, TR, PD, PE) em 20 kHz e 100 kHz. É a matéria-prima física de onde todo o resto é derivado; serve de controle de qualidade, mas não é obrigatória para o acompanhamento.

> **Hipótese:** como InBody120 tem layout padronizado, os 3 arquivos do Drive devem ter exatamente esses mesmos campos — o que torna a extração automática (OCR por região fixa) viável. Confirmo ao abrir os arquivos.

## Parte 2 — Como os arquivos se relacionam

Os 3 arquivos não são documentos independentes: são **3 fotografias do mesmo corpo em datas diferentes**. O que os costura é a chave de ligação.

- **Chave de identidade + tempo.** Cada laudo tem `ID` (a pessoa) e `Data/Hora` (o instante). O par **ID + Data/Hora identifica unicamente cada medição**. Empilhar os 3 por essa chave produz uma **série temporal** — a base de todo o acompanhamento.
- **Relação de composição (parte/todo), dentro de um mesmo laudo.** Os blocos se somam: Água + Proteína + Minerais + Gordura ≈ Peso; e massa magra dos 5 segmentos ≈ massa magra total. Isso vira uma **regra de validação automática**: se o OCR ler errado um campo, a soma não fecha e o app detecta.
- **Faixas de referência são derivadas do perfil.** Altura, idade e sexo definem as faixas que o laudo imprime. Se o perfil mudar entre exames (ex.: aniversário muda a idade), as faixas mudam — então compare sempre o **valor absoluto**, e trate a faixa como contexto daquele exame.
- **O próprio aparelho já pensa em série.** O laudo tem um bloco **“Histórico da Composição Corporal”** (Peso, Massa Muscular, % Gordura) — na amostra com 1 ponto só. Isso confirma que a leitura natural do InBody é **evolução no tempo**, exatamente o que seu app quer mostrar.
- **Ligação com o contexto clínico (hipótese).** No PC, a bioimpedância está na pasta da **Nutricionista**, ao lado de pastas de Endocrinologista, Cardiologista e Oncologista. Há potencial de cruzar a composição corporal com exames desses especialistas — fora do escopo agora, mas vale registrar.

**Modelo de dados sugerido (minha proposta):** duas tabelas — `pessoa` (ID, nome, sexo, altura) e `medicao` (ID, data\_hora, peso, gordura, SMM…, + segmentares), ligadas por `ID`. Cada PDF vira **uma linha** em `medicao`.

## Parte 3 — Quais análises já parecem possíveis

Pense no corpo como uma empresa acompanhada por um **painel de KPIs**: há o valor atual, a meta e a tendência. Separo o que dá para fazer **com 1 exame** do que exige a **série (3+ exames)**.

**Já possível com 1 exame (foto do momento)**

- **Semáforo contra referência.** Marcar cada métrica como dentro/fora da faixa. Na amostra, acendem *vermelho*: Massa de Gordura (22,8 vs 8,1–16,2), Gordura Visceral (10 vs ≤9), WHR (0,92 vs ≤0,90), IMC (26,4 = sobrepeso) e TMB abaixo do esperado.
- **Distância até a meta (gap analysis).** O laudo já entrega a meta: −12,6 kg de gordura. É o equivalente ao *gap* entre realizado e orçado — ponto de partida de um “burn-down”.
- **Mapa de assimetria e déficit.** As duas pernas estão “Abaixo” (89,6% e 87,3% do ideal) — um gargalo localizado, como uma filial abaixo da meta enquanto as outras batem.

**Possível com a série (3+ exames) — o coração do app**

- **Tendência por KPI.** Linha do tempo de Peso, % Gordura e Massa Muscular — subindo, estável ou caindo.
- **Velocidade da mudança.** kg/mês de gordura e de músculo: a *taxa*, não só o nível (como variação MoM de receita).
- **Qualidade da recomposição.** O cenário ideal é **gordura ↓ e músculo ↑ ao mesmo tempo**. Cruzar as duas séries diz se o progresso é saudável ou se está perdendo os dois (músculo junto).
- **Projeção até a meta.** Com a tendência, estimar *quando* a gordura chega na faixa — um “forecast” simples.
- **Aderência.** Intervalo entre exames (regularidade do acompanhamento), como cadence de reporte.

> **Importante (fato):** os 3 exames já estão carregados — a seção “Evolução” acima traz a primeira curva. Com o 4º laudo (22/10) ganhamos mais um ponto.

## Parte 4 — Dúvidas, riscos e limitações

**Leitura automática (OCR) — onde mais quebra**

- **Separador decimal BR.** Os números usam vírgula (22,8). Um OCR descuidado lê `228` ou `22.8` — erro de 10×. Precisa de regra de *parsing* pt-BR e da validação por soma (Parte 2).
- **Anotações à mão.** A amostra tem marcações manuscritas sobre o laudo. OCR não lê isso de forma confiável — candidato natural ao fluxo “campo faltante → digitar” que você props.
- **Qualidade da foto.** Entrada por câmera varia com luz, ângulo e foco; campos podem sair ilegíveis. O app precisa medir confiança por campo e **avisar exatamente qual falta**.
- **Campos truncados na origem.** O próprio PDF corta o nome (“MAURICIO DA SI…”) — nem todo campo ilegível é culpa do OCR.

**Dados e semântica**

- **Faixas não são fixas.** Mudam com idade/altura/sexo; não compare faixas entre exames — compare valores absolutos.
- **Escala de gordura visceral.** O InBody120 reporta *nível* (1–9 normal), não área em cm²; manter a definição consistente.

**Privacidade e governança (LGPD)**

- São **dados sensíveis de saúde**. Web + mobile sincronizados exigem decidir *onde* ficam (nuvem? criptografia? quem acessa?) — precisa estar resolvido antes de subir dados reais.
- **De quem é o acompanhamento?** A amostra é do Maurício; confirme o titular.

**Escopo e amostragem**

- **1 laudo lido.** Que o layout seja idêntico nos 3 do Drive é **hipótese** até abri-los.
- **4º arquivo reservado.** Para a ingestão posterior não duplicar, a chave `ID + Data/Hora` deve impedir registro repetido (idempotência).

## Minhas ideias de arquitetura

Minha proposta central: **um único registro validado na nuvem alimenta web e mobile**, e as 3 formas de entrada caem na mesma esteira de validação. O diferencial é o laço em destaque — quando um campo sai ilegível, o app diz **qual** campo é e deixa você digitar, **antes** de salvar. É a sua sugestão, virada parte central do desenho.

&#91;embedded content: Esteira de ingestão · 3 entradas, 1 validação, laço de campo faltante\]

As 3 entradas convergem para uma só validação; o que não passa vira aviso de campo faltante e volta; só o registro completo sincroniza para os dois apps.

**Decisões de arquitetura que proponho (e quero seu aval):**

- **Fonte única da verdade.** Um banco na nuvem; web e mobile são apenas *visões* dele. A sincronização se resolve no servidor — mais simples que sincronizar dois apps entre si.
- **Validação por confiança de campo.** Cada campo lido recebe um score; abaixo de um limite, ele entra no fluxo de digitação manual (em vez de salvar valor duvidoso).
- **Idempotência pela chave.** `ID + Data/Hora` impede que o 4º arquivo (e futuros) dupliquem uma medição já existente.
- **Offline-first no mobile.** Capturar ou digitar sem rede e sincronizar depois — útil no consultório/academia.
- **Privacidade por padrão.** Dado de saúde criptografado; escolher provedor e política de acesso antes de subir dados reais.

## Próximos passos

1. **Você me dá acesso aos 3 arquivos mais antigos** — connector do Drive, anexar aqui, ou baixar numa pasta do PC (detalhes na primeira seção). ✅ Feito: Drive conectado e os 3 laudos lidos.
2. **Confirmar o titular** do acompanhamento (a amostra é do Maurício).
3. **Eu extraio e valido os 3 laudos** — aplico o parse pt-BR, as regras de soma e monto o primeiro gráfico de evolução (Peso, % Gordura, Massa Muscular).
4. **Decidir privacidade/armazenamento** antes de subir dado real — condição para a parte web+mobile.
5. **Só então projetar/construir o app** (fora desta etapa inicial, como você pediu).

Me diga por qual via prefere mandar os arquivos e eu sigo do passo 3 em diante.
