# Prompts para gerar o diagrama

Dois prompts para o mesmo diagrama, ajustados ao comportamento de cada ferramenta.
Depois de escolher, exportar em PNG para `assets/diagrama-fluxo-multimodal.png`.

---

## A · Lucidchart AI

> Colar no gerador de diagramas por IA do Lucidchart.

Crie um fluxograma de raias (swimlanes) horizontais, em português do Brasil, representando um atendimento multimodal de cafeteria em que voz e tela carregam conteúdos diferentes.

**Raias, de cima para baixo:**
1. USUÁRIO — fala ou toque da pessoa. Fundo cinza claro, retângulo de cantos arredondados.
2. SISTEMA · VOZ — saída falada, transcrita entre aspas. Fundo azul claro, retângulo de cantos arredondados.
3. SISTEMA · TELA — conteúdo exibido no display do balcão, em tópicos curtos. Fundo verde claro, retângulo de cantos retos.

**Convenções:**
- Organize em colunas verticais por turno (T0 a T7): os nós de voz e de tela do mesmo turno ficam alinhados na mesma coluna.
- Cada nó do sistema termina com uma etiqueta entre colchetes: [A] Atribuição, [C] Complementaridade, [R] Redundância, [E] Equivalência.
- Redundância deliberada → borda tracejada. Complementaridade → borda grossa.
- Losango para a decisão. Nó com borda vermelha tracejada para conteúdo suprimido.
- Legenda no canto inferior direito: cor por canal, borda tracejada, borda grossa, siglas CARE.
- Título: "Cafeteria Inteli — fluxo multimodal | Agrupamento: tela auxiliar compartilhada".

**Nós (use exatamente estes, não invente etapas):**

T0 · Abertura
- USUÁRIO: [aproxima-se do balcão]
- VOZ: "[som de ativação] Boa tarde! Pode pedir." — [A]
- TELA: Cardápio completo com preços · indicador "Ouvindo…" — [C]

T1 · Escolher bebida
- USUÁRIO: "Um chocolate quente."
- VOZ: "Chocolate quente." — [R] borda tracejada
- TELA: Carrinho: 1 Chocolate quente — [A]

T2 · Tamanho e cobertura
- VOZ: "Qual tamanho — pequeno, médio ou grande?" — [C] borda grossa
- TELA: P 200ml R$7,00 | M 300ml R$9,00 | G 400ml R$11,00 — [C] borda grossa
- USUÁRIO: "Médio."
- VOZ: "Médio. Quer chantilly, canela, ou sem cobertura?" — [A]
- TELA: Carrinho R$ 9,00 · Chantilly +R$2,00 · Canela sem acréscimo — [C]
- USUÁRIO: "Canela."
- VOZ: "Fechado, com canela. Mais alguma coisa?" — [A]

T3 · Escolher comida
- USUÁRIO: "Vocês têm alguma coisa doce?"
- VOZ: "Cinco opções no display. Alguma te interessa?" — [A] condensação
- TELA: Bolo de cenoura R$5,50 | Cookie de castanha R$6,00 | Cookie de chocolate R$6,00 | Brownie R$7,50 | Muffin de banana R$5,00 — [A]
- USUÁRIO: "Um cookie."

T4 · Decisão (losango): o pedido identifica um único item do cardápio?
- Ramo NÃO:
  - VOZ: "[som breve de dúvida] Tem dois cookies. De castanha ou de chocolate?" — [C] borda grossa
  - TELA: os dois cookies ganham contorno; os outros três ficam esmaecidos — [C] borda grossa
  - USUÁRIO: "De castanha."
  - VOZ: "Cookie de castanha, anotado." — [R]
  - TELA: Carrinho + 1 Cookie de castanha R$ 6,00 — [A]
- Ramo SIM: segue direto para T5.

T5 · Avisar sobre alérgeno
- VOZ: "Atenção: esse cookie leva castanha-de-caju. Pode seguir?" — [C] borda grossa
- TELA: Contém castanha-de-caju, trigo, ovo, leite · Pode conter traços de amendoim e soja — [C] borda grossa
- TELA (conteúdo suprimido, borda vermelha tracejada): perfil de restrições alimentares da pessoa NÃO é exibido. Tela compartilhada. Em conflito, só a voz avisa, sem nomear a restrição.
- USUÁRIO: "Pode."

T6 · Confirmar pedido
- VOZ: "Quinze reais, no cartão do seu cadastro. Confirma?" — [R] borda tracejada
- TELA: Chocolate quente médio R$9,00 | Cookie de castanha R$6,00 | TOTAL R$15,00 | Cartão •••• 0942 | [CONFIRMAR] [CANCELAR] — [R] borda tracejada
- USUÁRIO: "Pode fechar." OU toca em CONFIRMAR — [E]

T7 · Encerramento
- VOZ: "[som de sucesso] Fechado. Sua senha é 23, chamo no balcão." — [R] borda tracejada
- TELA: Senha 23 em corpo grande · status "em preparo" · ~5 min — [R] borda tracejada
- USUÁRIO: [retira-se do balcão]

**Conexões:** sequência T0 → T1 → T2 → T3 → T4 → T5 → T6 → T7. Dentro de cada turno, ligue o nó de VOZ ao nó de TELA com linha tracejada fina, sem seta, rotulada "simultâneo".

---

## B · Figma (FigJam AI / Figma Make)

> O gerador do FigJam não desenha raias nem aplica estilo por nó. Por isso este prompt embute o canal no texto de cada bloco e deixa a formatação para o passo manual descrito no fim.

Gere um fluxograma vertical em português do Brasil sobre um atendimento de cafeteria com dois canais de saída: voz e tela. Cada bloco começa com o canal entre colchetes. Não resuma nem reescreva os textos.

[VOZ] "[som de ativação] Boa tarde! Pode pedir." (A)
[TELA] Cardápio completo com preços + indicador "Ouvindo…" (C)
[USUÁRIO] "Um chocolate quente."
[VOZ] "Chocolate quente." (R)
[TELA] Carrinho: 1 Chocolate quente (A)
[VOZ] "Qual tamanho — pequeno, médio ou grande?" (C)
[TELA] P 200ml R$7 · M 300ml R$9 · G 400ml R$11 (C)
[USUÁRIO] "Médio."
[VOZ] "Médio. Quer chantilly, canela, ou sem cobertura?" (A)
[TELA] Carrinho R$9,00 · Chantilly +R$2 · Canela sem acréscimo (C)
[USUÁRIO] "Canela."
[USUÁRIO] "Vocês têm alguma coisa doce?"
[VOZ] "Cinco opções no display. Alguma te interessa?" (A)
[TELA] Bolo de cenoura · Cookie de castanha · Cookie de chocolate · Brownie · Muffin de banana, com preços (A)
[USUÁRIO] "Um cookie."
[DECISÃO] O pedido identifica um único item?
[VOZ] "Tem dois cookies. De castanha ou de chocolate?" (C)
[TELA] Os dois cookies destacados, os outros esmaecidos (C)
[USUÁRIO] "De castanha."
[VOZ] "Cookie de castanha, anotado." (R)
[VOZ] "Atenção: esse cookie leva castanha-de-caju. Pode seguir?" (C)
[TELA] Contém castanha-de-caju, trigo, ovo, leite · traços de amendoim e soja (C)
[SUPRIMIDO] Perfil de restrições da pessoa não vai à tela — tela compartilhada
[USUÁRIO] "Pode."
[VOZ] "Quinze reais, no cartão do seu cadastro. Confirma?" (R)
[TELA] Itens · TOTAL R$15,00 · Cartão •••• 0942 · [CONFIRMAR] [CANCELAR] (R)
[USUÁRIO] "Pode fechar." ou toca em CONFIRMAR (E)
[VOZ] "[som de sucesso] Fechado. Sua senha é 23, chamo no balcão." (R)
[TELA] Senha 23 em corpo grande · em preparo · ~5 min (R)

### Passo manual depois de gerar (5–10 min)

1. Desenhe três **Sections** horizontais e nomeie: USUÁRIO, SISTEMA · VOZ, SISTEMA · TELA.
2. Arraste cada bloco para a section do seu prefixo e alinhe verticalmente os blocos do mesmo turno.
3. Pinte por canal: cinza (usuário), azul claro (voz), verde claro (tela).
4. Bordas: tracejada nos blocos (R); grossa nos blocos (C) de T2, T4 e T5; vermelha tracejada no bloco [SUPRIMIDO].
5. Apague os prefixos entre colchetes — a section já identifica o canal.
6. Adicione a legenda e o título "Cafeteria Inteli — fluxo multimodal | Agrupamento: tela auxiliar compartilhada".

> Alternativa: no **Figma Make**, colar o prompt acima acrescentando "desenhe como diagrama de raias horizontais, uma raia por canal, turnos alinhados em colunas" — ele monta a estrutura já estilizada, mas o texto sai menos fiel e precisa de conferência.
