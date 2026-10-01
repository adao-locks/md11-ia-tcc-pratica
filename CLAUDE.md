# CLAUDE.md — GerenciadorDeTarefas

Guia para assistentes de IA que trabalham neste repositório. Leia inteiro antes de alterar qualquer arquivo.

## Contexto do projeto

- Repositório da **avaliação do Módulo 11 (Tecnologias Emergentes e IA)** do Entra21.
- O código é um **console app didático em C#** (`GerenciadorDeTarefas/`) que gerencia uma lista de tarefas **somente em memória**. Ele é simples de propósito: serve de base para praticar o uso de IA, não para virar um produto.
- Não há banco de dados, arquivos, API, interface gráfica nem pacotes NuGet. Não adicione nada disso.

## Stack e estrutura

| Item | Valor |
|---|---|
| Linguagem | C# (top-level statements, sem `class Program`/`Main`) |
| Framework | .NET 8 (`net8.0`), `ImplicitUsings` e `Nullable` habilitados |
| Solução | `GerenciadorDeTarefas.sln` → `GerenciadorDeTarefas/GerenciadorDeTarefas.csproj` |
| Código | Tudo em `GerenciadorDeTarefas/Program.cs` |
| Testes | Não existem (não há projeto de testes) |

Organização do `Program.cs`, nesta ordem:

1. **Estado** — `tarefas` (`List<(int Id, string Titulo, bool Concluida)>`) e `proximoId`.
2. **Funções locais** — `Adicionar`, `Concluir`, `Listar`, ... (uma responsabilidade cada).
3. **Demonstração** — chamadas às funções com `Console.WriteLine` de cabeçalho `=== ... ===`.
4. `Console.ReadLine();` — mantém a janela aberta no Visual Studio. **Deve continuar sendo a última instrução executável.**

## Comandos úteis

```bash
dotnet build GerenciadorDeTarefas.sln          # compilar (deve terminar com 0 warnings, 0 errors)
dotnet run --project GerenciadorDeTarefas      # executar (pressione Enter para sair)
echo | dotnet run --project GerenciadorDeTarefas   # executar sem travar no ReadLine (útil para a IA/CI)
```

## Convenções de código

- **Idioma:** identificadores, textos de console e comentários em **português** (`Adicionar`, `Concluida`, `titulo`). Nomes de funções são verbos no infinitivo em PascalCase; variáveis em camelCase.
- **Modelo de dados:** manter a **tupla nomeada** `(int Id, string Titulo, bool Concluida)`. Não criar `class`/`record Tarefa` nem novos arquivos sem pedido explícito.
- **Funções locais** no topo do arquivo, antes da demonstração, com `void` quando não retornam nada.
- **Tuplas são imutáveis:** para alterar um item, substitua o elemento inteiro (`tarefas[i] = (tarefas[i].Id, tarefas[i].Titulo, true);`), como em `Concluir`.
- **Estilo:** chaves em linha própria (Allman), 4 espaços, `var` sempre que o tipo for óbvio, interpolação `$"..."`, laços `for`/`foreach` simples — o estilo é propositalmente didático; evite LINQ rebuscado quando um laço simples resolve.
- **Saída no console:** formato `"{status} #{Id} — {Titulo}"` com status `[X]` / `[ ]` e travessão `—` (não hífen). Novos blocos de demonstração seguem `Console.WriteLine();` + `Console.WriteLine("=== Descrição ===");`.
- **Ids:** vêm sempre de `proximoId++`; nunca são reaproveitados depois de uma remoção.

## Como trabalhar aqui

- Antes de editar, leia o `Program.cs` inteiro e reproduza o estilo existente.
- Para **adicionar uma funcionalidade**, use a skill `.claude/skills/nova-funcionalidade-tarefas/SKILL.md`.
- Depois de qualquer alteração em código: rode `dotnet build` e `echo | dotnet run --project GerenciadorDeTarefas` e confira a saída.
- Mudanças pequenas e focadas: uma funcionalidade por vez; mostre o diff e explique o que mudou.

## O que a IA NÃO deve fazer

- ❌ Não alterar `README.md` a não ser para responder as questões dissertativas; não mexer nos enunciados, critérios ou datas.
- ❌ Não alterar `.github/`, `.gitattributes`, `.gitignore`, `.sln` ou `.csproj` (inclusive `TargetFramework`) sem pedido explícito.
- ❌ Não adicionar pacotes NuGet, persistência, frameworks de UI, injeção de dependência ou novas camadas/arquivos.
- ❌ Não remover o `Console.ReadLine()` final nem o comentário de orientação no fim do `Program.cs`.
- ❌ Não traduzir o código para inglês nem renomear funções/variáveis existentes.
- ❌ Não inventar conteúdo para `EVIDENCIAS.md`: só registrar o que realmente aconteceu na sessão.
- ❌ Não fazer commit, push ou abrir PR sem o aluno pedir.
