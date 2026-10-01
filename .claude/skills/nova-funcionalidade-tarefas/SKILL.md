---
name: nova-funcionalidade-tarefas
description: Adiciona uma nova operação (ex.: remover, editar, filtrar, contar tarefas) ao GerenciadorDeTarefas/Program.cs seguindo o estilo existente e validando com build + execução. Use quando o pedido for "adicione/crie uma função/funcionalidade" no gerenciador de tarefas.
---

# Nova funcionalidade no GerenciadorDeTarefas

Receita para incluir **uma** operação nova no `GerenciadorDeTarefas/Program.cs` sem quebrar o estilo nem o escopo do projeto. As regras gerais estão no `CLAUDE.md` da raiz; esta skill é o passo a passo.

## Entrada esperada

O pedido do usuário descrevendo a operação (ex.: "remover tarefa por id", "listar só as pendentes"). Se o comportamento em um caso de borda não estiver claro (id inexistente, lista vazia), escolha o comportamento mais simples e **diga qual escolheu** no resumo final.

## Passo a passo

1. **Ler** o `GerenciadorDeTarefas/Program.cs` inteiro e identificar as 4 seções: estado → funções locais → demonstração → `Console.ReadLine()`.
2. **Verificar se já existe** algo equivalente. Se existir, reutilize/ajuste em vez de duplicar.
3. **Escrever a função local** logo após a última função existente (antes de qualquer chamada de demonstração):
   - Nome: verbo no infinitivo em PascalCase, em português (`Remover`, `ListarPendentes`, `Editar`).
   - Parâmetros em camelCase e em português (`int id`, `string novoTitulo`).
   - Trabalhar sobre a lista `tarefas` com tupla `(int Id, string Titulo, bool Concluida)`; para alterar um item, **substituir a tupla inteira**.
   - Para remover durante iteração, percorrer com `for` **de trás para frente** ou usar `tarefas.RemoveAll(t => t.Id == id)`.
   - Para listagens, reaproveitar o formato `"{status} #{t.Id} — {t.Titulo}"` com `[X]`/`[ ]` e travessão `—`.
   - Id inexistente: não lançar exceção; seguir o comportamento de `Concluir` (ignorar silenciosamente) salvo pedido contrário.
4. **Demonstrar** a função na seção de demonstração, **antes** do `Console.ReadLine()`:
   ```csharp
   NovaFuncao(argumentos);

   Console.WriteLine();
   Console.WriteLine("=== Depois de <descrição da ação> ===");
   Listar(); // ou a própria função, se for uma listagem
   ```
5. **Não mexer** em: `.csproj`, `.sln`, funções existentes (exceto se o pedido exigir), o `Console.ReadLine()` final e o comentário de orientação no fim do arquivo.
6. **Validar:**
   ```bash
   dotnet build GerenciadorDeTarefas.sln
   echo | dotnet run --project GerenciadorDeTarefas
   ```
   O build deve ter **0 warnings e 0 errors** (o projeto usa `Nullable`). Confira na saída se o bloco novo aparece e se o resultado faz sentido. Se falhar, corrija e rode de novo — não entregue sem compilar.

## Checklist de saída

- [ ] Função nova em português, no topo junto das outras, estilo Allman.
- [ ] Nenhum arquivo além do `Program.cs` alterado.
- [ ] Bloco `=== ... ===` de demonstração adicionado antes do `Console.ReadLine()`.
- [ ] `dotnet build` sem warnings e saída de `dotnet run` conferida.
- [ ] Resumo ao usuário: o que foi adicionado, decisões de caso de borda e a saída do programa.

## Exemplo (few-shot)

Pedido: "adicione uma função para remover tarefa pelo id".

```csharp
void Remover(int id)
{
    for (var i = tarefas.Count - 1; i >= 0; i--)
    {
        if (tarefas[i].Id == id)
        {
            tarefas.RemoveAt(i);
        }
    }
}
```

Demonstração:

```csharp
Remover(2);

Console.WriteLine();
Console.WriteLine("=== Depois de remover a tarefa #2 ===");
Listar();
```
