# Smaug 
# 🔥🐉🪙

## O que é a aplicação?  
Smaug é um robô de análise quantitativa exaustiva que varre o mercado da B3 em busca do melhor universo possível para encontrar a operação de trading de maior lucro e de menor risco.

## Problema que resolve  
Estratégias de trading exigem ajustes específicos para cada ativo, pois cada ativo possui um padrão diferente. Encontrar os melhores parâmetros demanda a execução de múltiplos backtests com diferentes combinações, o que se torna inviável manualmente quando aplicado a um grande número de ativos.
O robô resolve esse problema com análise exaustiva (verifica todas as possibilidades possíveis), por meio de análise combinatória de variáveis, executando backtests em escala e identificando as melhores oportunidades com base na relação risco/retorno e custo de oportunidade. Isso torna o processo mais eficiente, escalável e orientado por dados.

## Público-alvo  
Devido ao equilíbrio de Nash, um sistema eficiente tende a perder eficácia se amplamente divulgado. A vantagem competitiva está na exclusividade, portanto o Smaug é restrito ao uso dos seus desenvolvedores e traders contribuidores.

## Funcionalidades mínimas da primeira versão  
- Análise diária dos dados OHLC (Open, High, Low, Close) dos ativos.  
- Conversão dos dados para banco SQLite via script Typescript.  
- Aplicação de filtros como: lucro mínimo, taxa de acerto mínimo, ratio de ganho/max drawdown e entre outros.  
- Implementação de uma estratégia inicial, atualmente há 2 já implementadas para tempo do diário [25/08/2025].
- Geração de tabela classificando ativos do mais ao menos lucrativo.  
- Interface simples para visualização, ainda a definir entre web ou desktop.

## Funcionalidades futuras
- Criar um mapeamento de coordenadas temporais combinando dia da semana com hora do dia (ex.: terça às 13:00, segunda às 14:00) ou dia do mês com hora do dia, com o objetivo de identificar possíveis ineficiências no mercado causadas por movimentos de grandes instituições financeiras.

## Banco de Dados com foco em integridade
- Coleta de dados exclusivamente por meios oficiais, como MetaTrader (no caso de Forex) e arquivos de transações da B3.
- Mitigação de risco de omissão de dados presente em APIs públicas gratuitas devido a conflito de interesse.
- Armazenamento estruturado no banco SQLite, garantindo consistência e integridade.
- Possibilidade de integração futura com bancos mais robustos (PostgreSQL, MySQL) caso o volume de dados exija.

## Interface gráfica  
A interface gráfica ainda não está definida. A prioridade inicial é o backend e automação, com a interface visando simplicidade e facilidade de uso.

## Plataforma final  
Desktop.

## Linguagem base  
Desenvolvido inicialmente em TypeScript para prototipagem rápida, com plano de reimplementação em Java visando maior desempenho e robustez.

## Meta de performance e volume de dados  
Inicialmente, o Smaug processará entre 500 e 600 ativos da B3. Futuramente, o sistema será expandido para mercados como Forex, criptomoedas, ações americanas ou qualquer ativo com liquidez mínima.

O projeto passará por mais duas etapas:  
- A próxima etapa será a análise intraday dos ativos, utilizando dados OHLC de 1 hora.  
- Após a validação dessa funcionalidade, a etapa final será a análise com dados OHLC de 5 minutos.

## Natureza do projeto  
Produto real, restrito ao uso dos desenvolvedores e traders colaboradores. Os desenvolvedores podem mencioná-lo em seus currículos, desde que não revelem informações que possibilitem engenharia reversa.

# Smaug Utilizará  a Estratégia de Alavancagem Temporal com Diversificação de Eventos Raros
Utilizada no robô *Ouroboros*
© 2025 Giovanne Bohms

##  Conceito

Esta estratégia busca explorar **eventos raros com alto potencial de lucro**, utilizando uma forma alternativa de alavancagem: **alavancagem no tempo**, e não no valor da operação.

A ideia é simples: **se um evento é raro e ocorre em média a cada X dias em um ativo**, então apostar simultaneamente em vários ativos **aumenta a chance de capturar esse evento mais rapidamente**. Isso permite adiantar o lucro sem aumentar o risco por operação.

---

##  Objetivo

- Acelerar o tempo até que um evento raro ocorra.
- Utilizar alavancagem via simultaneidade (não via empréstimo de capital).
- Automação de inserção de ordens por meio do metaTrader quando o valor do ativo estiver próximo da ordem de compra ou venda. Por meio da automação torna o custo de oportunidade eficiente

---

##  Lógica da Estratégia de Alavancagem Temporal

1. Identificar um **evento com baixa probabilidade**, mas com **alto retorno potencial** (ex hipotético: 5% de chance de ocorrer no dia, 2% de retorno).
2. Assumir que esse evento ocorre **em média uma vez a cada X dias** por ativo.
3. Em vez de esperar passivamente o evento ocorrer em um único ativo, **apostar em vários ativos que possuem as mesmas probabilidades ao mesmo tempo**.
4. Quando **um dos ativos executar com sucesso a estratégia**, **cancelar as demais apostas**.
5. Isso cria uma **alavancagem no tempo**, sem aumentar o risco individual de cada posição.

---

##  Exemplo Prático

- **Evento esperado**: ocorre em média 1 vez a cada 10 dias em cada ativo.
- **Capital disponível**: R$ 1.000
- **Estratégia**:
  - Apostar R$ 1.000 distribuídos em **10 ativos diferentes** com a mesma estrutura de risco/retorno.
  - Observar o comportamento ao longo de **1 dia**.
  - Se **um único ativo** realizar o evento desejado:
    - **Encerrar imediatamente** todas as outras operações.
  - Isso equivale a ter esperado 10 dias em um único ativo — **mas em 1 dia real**.

---

##  Vantagens

- Redução do tempo necessário para realizar um lucro estatístico.
- Aumento da frequência de oportunidade sem necessidade de mais capital.

---

##  Risco

- O evento pode **não ocorrer em nenhum dos ativos**, gerando perda total naquele ciclo.
- O evento **pode ocorrer em mais de um ativo gerando alavancagem de capital**
- Requer **cancelamento ágil** das ordens restantes após o sucesso em um ativo (mitigável com metaTrader).

---


##  Conclusão

Essa estratégia explora uma lacuna muitas vezes ignorada no mercado: **a possibilidade de alavancar no tempo, e não no capital**. Ao distribuir apostas com mesma estrutura estatística em múltiplos ativos simultaneamente, o trader **antecipa o sucesso esperado**, aumentando a eficiência da estratégia com risco controlado.

---

### Por que criei este paper?

Embora eu tenha conhecimento e experiência em trading e desenvolvimento, este projeto é muito complexo, o mais desafiador em que já trabalhei. O objetivo deste paper é reunir pessoas que compartilhem a mesma paixão, sejam traders ou programadores, dispostas a colaborar, unindo habilidades em programação e experiência em mercado financeiro. A ideia é formar um grupo pequeno, de no **máximo** 3 a 4 pessoas, já que o lucro é limitado, mas com foco em encontrar, por meio de busca detalhada, os padrões mais lucrativos e de menor risco.
