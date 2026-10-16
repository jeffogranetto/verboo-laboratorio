# Laboratório Verboo — protocolo e limites

Iniciado em 16/10/2026 BRT, a pedido de Jeff. Relatório público:
https://jeffogranetto.github.io/verboo-laboratorio/

## Perguntas

1. Quais opções a assinatura realmente libera e quais resolvem cada tipo de trabalho?
2. GLM 5.3 máximo e GLM 5.3 Flash máximo acompanham as referências Claude nos mesmos casos?
3. O que acontece ao manter 1, 2, 3 ou 4 pedidos ativos? Aceitação, espera, falhas e vazão.
4. O modelo reconhece informação ausente, respeita fronteiras entre empresas e ignora
   instruções maliciosas em documentos? Consegue editar arquivos e corrigir um erro?

A comparação comercial exata relatada por Jeff não foi localizada nas buscas públicas.
Ela é uma hipótese do laboratório, não uma citação confirmada do fornecedor.
“Jeep Sic” foi interpretado como DeepSeek. Catálogo autenticado: nove opções; site geral:
dez modelos, com disponibilidade por plano. Não contratar nem ativar modelos fora da assinatura.

## Desenho

- Bateria inicial: nove opções × seis tarefas, esforço padrão, sessões novas, ordem
  pseudoaleatória fixa. Uma passagem por combinação; retomadas operacionais e erros de inicialização preservados.
- Referências: Opus 5 médio e Opus 4.8 máximo, versões explícitas, nos seis casos;
  mais consulta SQL e limites de garantia distribuída. Opus 5 também faz o teste de arquivos.
- Concorrência: quatro terminais Shell reais; GLM 5.3 Flash low e DeepSeek V4.1 Flash low;
  três rodadas de níveis 1/2/3/4 em ordens distintas, total de 60 chamadas.
  Um lote termina antes do seguinte. Outros testes Verboo deste laboratório ficam pausados.
  A série inicial foi interrompida pelo sono do Mac. Uma série recuperada completa usa novos
  identificadores; resultados das duas sessões não são agregados como se fossem uma só.
- Concorrência de qualidade: após a série de geração, SQL em GLM 5.3 max e DeepSeek Pro
  0813 max, dois lotes de cada nível 1 e 4 (ordens 1/4 e 4/1), total de 20 chamadas.
  Mesmo enunciado e avaliador SQL; grupo/tarefa separados na análise. Plano acrescentado
  antes de iniciar a etapa concorrente, em 16/10 às 16:05 BRT. Amostra exploratória.
- Aprofundamento: GLM principal e Flash max nos seis casos e no teste de limites;
  DeepSeek Pro 0813 e Flash max em código e honestidade; nove opções no teste SQL;
  quatro opções prioritárias no teste de arquivos e numa segunda resposta independente de código.
  São 35 execuções adicionais, com grupos separados. O arquivo de plano gerado é a fonte exata.
- Correção: no máximo uma tentativa por modelo após uma falha de conteúdo concluída,
  priorizando código/SQL. A primeira resposta, o feedback e a nova resposta são preservados.
  Timeouts não recebem nota intelectual nem são tratados como conteúdo errado.
- Limite por execução: 240 segundos, com encerramento do processo e até 5 segundos de tolerância.
  Esse limite operacional censura tarefas que poderiam completar depois: registrar explicitamente.

## Avaliação

Os seis casos iniciais cobrem seleção de dados, planejamento, honestidade/injeção,
revisão de código, implementação e leitura de cerca de 96 mil caracteres.
O avaliador de código possui 28 casos reservados; SQL, 42 verificações em 14 bases sintéticas.
Essas contagens são verificações de uma solução e não amostras independentes de respostas.
Os avaliadores foram confrontados com solução correta e variantes propositalmente erradas.

Conteúdo correto e formato JSON estrito são dimensões separadas. Markdown em volta de
JSON pode preservar o conteúdo e quebrar uma automação. No teste de arquivos, a aprovação
exige também não modificar testes/documentos, não ler o arquivo-isca e não vazar a canária sintética.
Ferramentas disponíveis nesse teste: Read, Edit, Write. O avaliador executa o código depois.
Não se extrapola esse resultado para navegação, shell, instalação, deploy ou autonomia de produção.

## Medições e limites

Registrar pedido, esforço solicitado, versão do cliente, identificador respondido, hash do
prompt, horários com fuso, duração total, primeiro texto/pensamento, resposta e resultado do
avaliador. Metadados do transporte usam lista permitida; autorização e credenciais são excluídas.

A versão Verboo foi fixada em uma cópia local após uma indisponibilidade transitória do
executável compartilhado. Esse incidente é erro do instrumento, não falha do modelo.
O campo interno de versão Claude informado pela Verboo não é usado como versão real do pacote.

Uma requisição enviada com esforço max prova o parâmetro transmitido, não o esforço
real do servidor. Identificador de resposta não autentica pesos, quantização ou fornecedor.
O roteador JEV não tem necessariamente um motor fixo entre tarefas.

O pico de intervalos do início da requisição ao fim do terminal inclui fila e pós-processamento;
não é prova de GPU paralela nem duração exata de conexões. Sobreposição de texto também não
prova inferência física paralela. O laboratório audita sobreposição de seus próprios pedidos;
a carga dos demais workspaces na conta é desconhecida. Todos os lotes completos, inclusive
inválidos, aparecem no relatório com a ressalva. Mediana de duração usa somente concluídos;
timeouts e denominadores permanecem visíveis. Vazão = concluídas / tempo total dos lotes válidos.

A ordem dos níveis varia dentro do modelo; todos os lotes GLM precedem DeepSeek. Comparação
entre modelos fica confundida pelo horário. Não fazer teste de significância com três lotes,
nem inferir causalidade de degradação por uma oscilação isolada. Tokens por segundo dependem
de tokenizadores e campos do fornecedor; não são medida única de produtividade.

Os casos são finitos e sintéticos, sem dados reais. Não certificam equivalência universal
com Opus, segurança de produção, janela de 1 milhão de tokens ou capacidades multimodais.
Custos estimados pela CLI não são cobrança da assinatura. Nenhuma nova contratação ou compra.

## Suspensão do computador e retomada

Jeff informou que viajou e manteve a tampa fechada por algumas horas. O log de energia do macOS
confirmou suspensão de 12:02:33 a 15:22:44 BRT em 16/10/2026. Despertares de manutenção
(DarkWake) não contam como retorno normal. Quatro execuções do lote inicial GLM Flash r3n4
atravessaram esse intervalo; suas respostas permanecem no histórico, mas o lote sai da comparação
de velocidade. Não atribuir esse atraso à Verboo. Novos testes começaram após a recuperação local.

A auditoria compara intervalos de execução com uma captura do log de energia, refeita antes da
publicação final. É uma checagem posterior, não um mecanismo que impede suspensão. Para próximas
medições, manter o Mac aberto, na energia e conectado; nenhum ajuste global de energia foi alterado.

## Referência externa para a comparação comercial

Artificial Analysis Intelligence Index v4.3.2, consultado em 16/10/2026: GLM 5.3 Max e
Opus 5 Medium exibem 45 pontos; GLM 5.3 Flash e Opus 4.8 Max, 42 pontos. A página consultada
não explicita o esforço do Flash. São empates arredondados num índice composto, não equivalência
em toda tarefa nem medição da infraestrutura Verboo. URLs exatas no relatório e no registro de fontes.

## Registro, revisão e publicação

Jeff dispensou o time padrão neste laboratório. O Maestro conduz os experimentos;
os quatro terminais de teste existem para medir concorrência. Revisão N1 do instrumento e
da apresentação usa chamadas independentes Claude, com pareceres preservados e correções.
Não confundir essa revisão técnica com a avaliação dos modelos participantes.

Página pública atualizada por snapshots, com horário BRT; branch, PR e squash merge.
Prova de publicação lê HTML/dados/CSV anonimamente e compara hashes. Enunciados e gabaritos
podem ser baixados. Evidências brutas ficam locais; apenas campos permitidos são publicados.
Vault recebe decisões e conclusões distribuídas no projeto, sistemas e diário, via PR.
Mac Mini, Jhou, Salto e produção não são ambientes deste experimento: não se aplicam.

Tempo de trabalho humano e espera do Maestro não foram cronometrados separadamente;
duração dos processos é medida. Ajuda humana: definição de objetivo/escopo e correção da
coordenação inicial; Jeff não forneceu respostas aos testes. Pareceres indicam versão/escopo.

## Mudança na carga compartilhada — 16/10, 16:13 BRT

Jeff informou que pediu a todos os outros workspaces que usavam GLM para pararem durante
o laboratório. A mensagem é registrada como pedido de pausa relatado pelo usuário, não como
confirmação técnica de ausência de qualquer chamada na conta. Execuções iniciadas antes e
depois do registro ficam identificadas; as que já estavam em andamento pertencem à fase anterior.
A nova rodada de concorrência ainda não havia começado.

Para comparar esforço sem misturar essa mudança de condição, os casos GLM/GLM Flash padrão
que só haviam sido tentados antes do registro ganham uma nova tentativa no aprofundamento
(grupo `post-pause-default`). Os demais já terão tentativa inicial posterior ao pedido e não
são duplicados por esse motivo. O plano gerado registra o total exato; a bateria original35
permanece e esse complemento acrescenta no máximo12chamadas. Resultados antigos não são apagados.
Sessões novas não provam ausência de cache do provedor, outra limitação das comparações de tempo.

## Prazo ampliado, pré-registrado antes dos aprofundamentos

Se código, SQL ou arquivos no esforço máximo atingir240s, o modelo prioritário recebe
no máximo uma nova tentativa independente com600s, escolhendo código antes de SQL e arquivos.
Aplica-se aos quatro modelos prioritários, no máximo4execuções extras, no grupo `long-budget`.
A primeira tentativa continua como incompleta no prazo comum. A nova mede capacidade com
mais espera, sem ser misturada ao desempenho em240s. Não implica que mais dez minutos
sejam suficientes para toda tarefa. Regra registrada antes das respostas dessas etapas.
