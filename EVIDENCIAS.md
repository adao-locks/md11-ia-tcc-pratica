# Evidência de uso real da IA (Questão 11)

## Ferramenta

- **Claude Code** (aba *Code* do app desktop do Claude, no Windows 11), conectado à pasta local do repositório.
- **Modelo:** Claude Opus 5.5.
- **Data:** 29/09/2026.
- A IA tinha acesso ao código local: lia arquivos, editava e executava `dotnet build` / `dotnet run` no terminal.

## Prompt exato

> Quero que voce Analise todo o projeto de maneira extremamente minunsiosa, inclusive o Readme.MD e resolva o tudo que foi passado

## O que a IA fez

1. **Análise do projeto:** listou os arquivos versionados, leu `README.md`, `CLAUDE.md`, `EVIDENCIAS.md`, a skill modelo, o template de PR, `.gitignore`, `.sln`, `.csproj` e `Program.cs`. Conferiu os runtimes instalados (.NET 8 e 10) e rodou `dotnet build` + `dotnet run` **antes** de mudar qualquer coisa, para ter uma linha de base.
2. **`CLAUDE.md`:** escreveu o guia do projeto (contexto, stack, estrutura do `Program.cs`, comandos, convenções e o que a IA não deve fazer).
3. **Skill:** renomeou `minha-skill/` para `nova-funcionalidade-tarefas/` (com `git mv`) e escreveu a receita passo a passo para adicionar uma operação ao gerenciador.
4. **Uso da Skill numa tarefa real:** invocou a skill com o argumento *"adicione uma função para listar somente as tarefas pendentes"* (sugestão do próprio comentário no fim do `Program.cs`) e seguiu os passos:
   - criou a função local `ListarPendentes()` logo após `Listar()`, em português, estilo Allman, reaproveitando o formato `[ ] #Id — Titulo`;
   - adicionou o bloco `=== Somente as tarefas pendentes ===` **antes** do `Console.ReadLine()`;
   - não tocou em `.csproj`, `.sln` nem nas funções existentes;
   - validou com build e execução:

```text
Build succeeded.
    0 Warning(s)
    0 Error(s)
...
=== Depois de concluir a tarefa #1 ===
[X] #1 — Estudar para a avaliação do Módulo 11
[ ] #2 — Configurar o CLAUDE.md do projeto
[ ] #3 — Criar uma Skill reutilizável

=== Somente as tarefas pendentes ===
[ ] #2 — Configurar o CLAUDE.md do projeto
[ ] #3 — Criar uma Skill reutilizável
```

5. **README:** escreveu um **rascunho** das respostas dissertativas, para eu revisar e reescrever com as minhas palavras.

## A IA seguiu o CLAUDE.md / Skill?

**Sim, em quase tudo:** manteve a tupla nomeada, os nomes em português, o travessão `—` na saída, o `Console.ReadLine()` como última instrução, alterou só o `Program.cs` e compilou sem warnings antes de dar a tarefa por concluída. Também não fez commit/push, como o `CLAUDE.md` pede.

**O que precisou de ajuste / o que aprendi:**

- **Skill em cache:** quando a skill foi invocada, o Claude Code carregou a versão **antiga** do `SKILL.md` (o modelo com `TODO`), porque a lista de skills é lida no início da sessão e a skill tinha acabado de ser renomeada/editada. A IA percebeu, conferiu o arquivo no disco e seguiu a versão nova. Lição: depois de criar ou editar uma skill, **abrir uma nova sessão** para ela ser carregada corretamente.
- **Travamento no `Console.ReadLine()`:** rodar `dotnet run` direto deixaria o terminal da IA esperando Enter. Por isso o `CLAUDE.md` e a skill documentam o comando `echo | dotnet run --project GerenciadorDeTarefas`.
- **Iteração do prompt:** a primeira versão das respostas do README ficou formal e longa demais. Mandei um segundo prompt — *"A parte de escrita do readme quero que vc faca mais simples como se fosse um dev junior respondendo"* — e a IA reescreveu as 9 respostas com linguagem mais simples e direta.
- **Revisão humana:** a IA deixou claro que as respostas dissertativas são rascunho — cabe a mim conferir e reescrever antes de entregar.
