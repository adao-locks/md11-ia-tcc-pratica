# Avaliação Individual — Módulo 11 — Tecnologias Emergentes e IA

**Data de entrega:** DD/MM/AAAA
**Formato:** individual, de consulta aberta — use slides, anotações e a própria IA à vontade para pesquisar e testar suas respostas.

## Como participar

1. Faça um **fork** deste repositório.
2. Clone o seu fork localmente.
3. Responda as questões teóricas **direto neste README**, abaixo de cada uma.
4. Complete a parte prática (veja abaixo) editando `CLAUDE.md`, `.claude/skills/minha-skill/SKILL.md` e `EVIDENCIAS.md`.
5. Abra um **Pull Request** do seu fork de volta para este repositório.

> O PR não será mergeado — ele existe só para eu avaliar o seu diff. Pode deixar aberto depois de enviar.

O objetivo não é decorar definições, e sim demonstrar que você entende os conceitos e sabe aplicá-los para ganhar eficiência ao usar IA no seu projeto de TCC. Responda com suas próprias palavras — copiar e colar resposta pronta de IA sem entender não demonstra o aprendizado esperado.

---

## Questões dissertativas

### Questão 1 — O que é um "agent"?
O que é um "agent" (agente de IA)? Explique com suas próprias palavras e dê um exemplo de situação em que faz mais sentido usar um agente do que um chat comum.

**Sua resposta:**

Pelo que eu entendi, um agente é uma IA que não fica só conversando, ela consegue fazer as coisas sozinha. Ela pode ler e editar arquivos, rodar comandos no terminal e ver se deu certo, e vai repetindo isso até terminar a tarefa. No chat normal eu tenho que ficar copiando e colando o código e o erro toda hora.

Um exemplo é quando quero adicionar uma função no projeto e ver se compila. Com um agente (tipo o Claude Code) ele mesmo abre o `Program.cs`, faz a alteração, roda o `dotnet build` e se der erro ele arruma. Pra uma dúvida rápida tipo "o que é uma tupla em C#" o chat normal já resolve.

### Questão 2 — O que são guidelines?
O que são "guidelines" (diretrizes) ao usar uma IA generativa? Qual é o papel delas na qualidade das respostas geradas pelo modelo?

**Sua resposta:**

Guidelines são as regras que eu passo pra IA seguir, tipo "escreve os nomes em português", "não cria arquivo novo", "não instala pacote". Elas podem ir no próprio prompt ou num arquivo como o `CLAUDE.md`, que a IA lê sempre.

Elas ajudam porque sem regra a IA faz do jeito que ela acha melhor, e às vezes não tem nada a ver com o meu projeto (por exemplo criar uma classe em inglês quando o projeto usa tupla em português). Com as guidelines as respostas ficam mais parecidas com o que eu quero e eu preciso corrigir menos coisa.

### Questão 4 — Escolha de modelo e nível de esforço
Qual modelo de IA utilizar para cada tipo de tarefa? Dê um exemplo de tarefa simples e outra mais complexa, explicando como você escolheria o modelo em cada caso. O que é o "nível de esforço" (effort level) e quando faz sentido aumentá-lo ou diminuí-lo?

**Sua resposta:**

Eu escolheria pelo tamanho da tarefa. Pra coisa simples uso um modelo mais rápido e barato, e pra coisa difícil uso um modelo mais forte.

- **Simples:** corrigir um texto, explicar um erro de compilação, criar dados de teste. Aqui um modelo menor (tipo o Haiku) já resolve e é mais rápido.
- **Complexa:** pensar a estrutura do sistema do TCC ou achar um bug que envolve vários arquivos. Aqui vale usar um modelo mais forte (tipo Sonnet ou Opus), porque ele entende melhor o contexto todo.

O nível de esforço é o quanto a IA "pensa" antes de responder. Eu aumentaria quando o problema é difícil ou quando errar dá muito trabalho depois, e diminuiria quando é uma tarefa simples, porque aí pensar mais só demora e gasta mais.

### Questão 5 — Como estruturar um bom prompt
Descreva os elementos que tornam um prompt mais eficaz (ex.: contexto, objetivo, formato esperado, exemplos, restrições).

**Sua resposta:**

Pra mim um bom prompt tem:

- **Contexto:** falar qual é o projeto e a tecnologia (ex.: "é um console app em C# .NET 8").
- **Objetivo:** dizer bem certinho o que eu quero (ex.: "cria uma função pra remover tarefa pelo id").
- **Restrições:** o que ela não pode fazer (ex.: "não cria arquivo novo, mantém os nomes em português").
- **Formato:** como eu quero a resposta (ex.: "me mostra só o código novo e explica rapidinho").
- **Exemplos:** quando dá, mostrar um exemplo de como deve ficar.

Quanto mais claro eu for, menos a IA precisa adivinhar.

### Questão 6 — Iteração de prompt
O que significa "iterar" um prompt? Por que a primeira resposta de uma IA geralmente não é a versão final, e como você usaria a resposta recebida para melhorar o próximo prompt?

**Sua resposta:**

Iterar é ir melhorando o prompt aos poucos. Eu mando, vejo a resposta, e se não ficou como eu queria eu ajusto e mando de novo.

A primeira resposta quase nunca fica perfeita porque no primeiro prompt eu esqueço de passar alguma informação, e aí a IA completa do jeito dela. Por exemplo, se eu peço "cria uma função de remover tarefa" e ela cria uma classe em inglês, no próximo prompt eu falo "usa a tupla que já existe e deixa os nomes em português". Se eu vejo que estou pedindo a mesma correção várias vezes, coloco isso no `CLAUDE.md` pra não precisar repetir.

### Questão 7 — Zero-shot vs. few-shot
Qual é a diferença entre um prompt "zero-shot" e um prompt "few-shot"? Dê um exemplo de situação em que vale a pena incluir exemplos dentro do próprio prompt.

**Sua resposta:**

Zero-shot é quando eu só peço a tarefa sem dar nenhum exemplo. Few-shot é quando eu coloco alguns exemplos no prompt pra IA seguir o mesmo padrão.

Vale a pena usar exemplos quando o formato é bem específico. Por exemplo, se eu quero que a IA escreva mensagens de commit no padrão do meu grupo do TCC, eu mostro 2 ou 3 commits que já fizemos (tipo `feat: adiciona login`) e ela passa a escrever igual. Na Skill que eu criei também coloquei um exemplo de função no final pra IA copiar o estilo.

### Questão 8 — Memória e contexto entre sessões
O que significa uma IA "ter memória" entre sessões diferentes de conversa? Por que, em um projeto longo como o TCC, é importante decidir o que precisa ser "lembrado" e como fornecer esse contexto para a IA a cada nova conversa?

**Sua resposta:**

A IA não lembra sozinha das conversas antigas, cada conversa nova começa do zero. "Ter memória" é quando a ferramenta guarda algumas informações (em arquivo ou em um recurso de memória) e passa de novo pra IA quando eu abro outra conversa.

No TCC isso é importante porque o projeto é longo e eu não quero explicar tudo de novo toda vez. Mas também não dá pra mandar tudo, então preciso escolher o que é importante: as tecnologias, os padrões de código, os comandos e o que já foi feito. Pra isso dá pra usar o `CLAUDE.md` (que a IA lê toda vez), as Skills e um resumo do que foi feito na última conversa.

### Questão 9 — Avaliar a resposta da IA
Antes de aplicar a sugestão de uma IA no seu projeto, como você verifica se ela está correta? Descreva pelo menos 2 formas práticas de checar a confiabilidade de uma resposta gerada por IA.

**Sua resposta:**

A IA às vezes inventa coisas e fala com certeza, então eu não confio de primeira. Algumas formas de checar:

1. **Rodar e testar:** compilar com `dotnet build`, rodar o programa e testar alguns casos, tipo lista vazia ou um id que não existe.
2. **Olhar a documentação:** ver na documentação oficial (Microsoft Learn, por exemplo) se aquele método ou biblioteca existe mesmo.
3. **Ler o código:** ver com calma o que mudou (`git diff`) e se tiver algo que eu não entendi, pedir pra IA explicar antes de aceitar.

Também é bom fazer commit antes, porque se der problema dá pra voltar.

### Questão 10 — Dividir tarefas complexas em etapas
Por que, em tarefas mais complexas, pode ser melhor dividir o trabalho em um fluxo de etapas (ex.: primeiro classificar/organizar, depois processar, depois revisar) em vez de pedir tudo em um único prompt? Dê um exemplo aplicado a uma tarefa do seu TCC.

**Sua resposta:**

Porque quando eu peço tudo de uma vez a IA acaba esquecendo alguma coisa ou fazendo tudo meio mal feito, e fica difícil achar onde deu errado. Dividindo em partes eu consigo conferir cada uma antes de ir pra próxima.

Exemplo no TCC, fazer o login do sistema:

1. Primeiro peço pra IA olhar o projeto e listar o que precisa mudar.
2. Depois peço um plano com os passos.
3. Aí peço pra fazer um passo por vez, testando cada um.
4. No final peço pra ela revisar o código procurando erros (por exemplo se a senha está sendo salva com hash).

> **Questão 3** (como escrever um bom CLAUDE.md) e a **Questão 11** (prática, evidência de uso real da IA) são respondidas nos próprios arquivos `CLAUDE.md` e `EVIDENCIAS.md` — veja a parte prática abaixo.

---

## Parte prática

1. **Complete o `CLAUDE.md`** na raiz deste repositório — é onde você responde a Questão 3, documentando o projeto para orientar um assistente de IA.
2. **Complete a Skill** em `.claude/skills/minha-skill/SKILL.md`, com instruções reutilizáveis para uma tarefa recorrente do projeto. Renomeie a pasta `minha-skill/` para o nome real da sua skill.
3. **Conecte um assistente de IA ao código local** (Claude Code, GitHub Copilot, Cursor, ou outro de sua escolha) e use-o pelo menos uma vez de verdade, aplicando o `CLAUDE.md` e/ou a Skill que você criou em uma tarefa real do projeto `GerenciadorDeTarefas`.
4. **Complete o `EVIDENCIAS.md`** — é onde você responde a Questão 11, documentando essa experiência (ferramenta usada, prompt exato, o que a IA fez, se seguiu suas instruções).

### O que NÃO fazer

- ❌ Copiar as respostas, o CLAUDE.md ou a Skill de um colega
- ❌ Inventar uma evidência que não aconteceu de verdade
- ❌ Alterar arquivos fora do escopo pedido

## Sobre o projeto de exemplo

Dentro de `GerenciadorDeTarefas/` tem um console app simples em C# — um gerenciador de tarefas fictício — que serve de base para você praticar. Não é necessário adicionar funcionalidades novas ao app; o foco é a configuração e o uso da IA em cima desse código.

Abra `GerenciadorDeTarefas.sln` no Visual Studio, ou rode pelo terminal:

```bash
cd GerenciadorDeTarefas
dotnet run
```

---

## Critérios de avaliação (10 pontos)

| Critério | Pontos |
|---|---|
| Questões dissertativas (conjunto) | 4 |
| `CLAUDE.md` bem estruturado e específico ao projeto (Questão 3) | 2 |
| Skill funcional e realmente reutilizável | 2 |
| `EVIDENCIAS.md` — uso real da IA, seguindo (ou não) o CLAUDE.md/Skill (Questão 11) | 1 |
| Qualidade do Pull Request (descrição clara, organizado, dentro do escopo) | 1 |

## Entrega

Envie o **link do seu Pull Request** pelo Akademos até a data acima.
