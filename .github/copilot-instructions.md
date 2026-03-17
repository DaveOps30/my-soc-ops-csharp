# Soc Ops — Workspace Instructions

## ⚠️ Mandatory Development Checklist

Run before every commit — no exceptions:

```bash
dotnet build SocOps/SocOps.csproj   # must pass with 0 errors, 0 warnings
dotnet test                          # must pass (when tests exist)
```

- [ ] Build passes clean
- [ ] Tests pass
- [ ] No unused variables or imports
- [ ] CSS uses utility classes from `wwwroot/css/app.css` — no inline styles

---

## Project

**Soc Ops** — Social Bingo game (Blazor WebAssembly, .NET 10). Players mark 5×5 squares by finding people who match the prompts. Game state: `Start → Playing → Bingo`.

```
SocOps/
├── Pages/Home.razor             # Single routable page; switches on GameState
├── Components/                  # StartScreen, GameScreen, BingoBoard, BingoSquare, BingoModal
├── Services/BingoGameService.cs # State + localStorage persistence (scoped singleton)
├── Services/BingoLogicService.cs# Stateless: board gen, toggle, bingo detection
├── Data/Questions.cs            # Edit here to change prompts; FREE_SPACE at index 12
└── wwwroot/css/app.css          # Custom Tailwind-like utility classes
```

Dev server: `dotnet run --project SocOps/SocOps.csproj` → http://localhost:5166

---

## Key Conventions

- **Styling** — Compose utility classes (`flex flex-col items-center gap-4`). Add new utilities to `app.css`; never use `<style>` blocks or `style=`. See `.github/instructions/css-utilities.instructions.md`. For redesigns, follow `.github/instructions/frontend-design.instructions.md`.
- **State** — `BingoGameService` is source of truth. Components subscribe to `OnStateChanged` → call `StateHasChanged()`; unsubscribe in `Dispose()`. Saves with fire-and-forget (`_ = SaveGameStateAsync()`).
- **Blazor** — `[Parameter]` on all component inputs; use `EventCallback<T>` over `Action<T>` for child→parent events.
- **C# naming** — PascalCase public, camelCase locals, `_camelCase` private fields.

---

## Custom Agents

| Agent | Use for |
|-------|---------|
| `quiz-master.agent.md` | Themed icebreaker questions |
| `tdd.agent.md` | Full Red → Green → Refactor cycle |
| `pixel-jam.agent.md` | Design-driven UI features |
| `ui-review.agent.md` | UX critique and improvements |
