# Copilot Workspace Instructions

## Development Checklist

Before committing any changes, ensure:

- [ ] `dotnet build` passes with no errors
- [ ] `dotnet test` passes (when tests exist)
- [ ] Code follows C# conventions (PascalCase for public members)
- [ ] No unused variables or imports

## Project Overview

**Soc Ops** is a Social Bingo game for in-person mixers, built with **Blazor WebAssembly (.NET 10)**. Players find people who match icebreaker questions to mark squares and get 5 in a row.

This repo also serves as a **GitHub Copilot Agent Lab** — a workshop demonstrating agentic AI workflows (custom agents, instructions, prompts, multi-agent orchestration).

## Key Commands

```bash
# Run dev server (http://localhost:5166)
cd SocOps && dotnet run

# Build
dotnet build SocOps/SocOps.csproj

# Run tests (when they exist)
dotnet test
```

## Architecture

```
SocOps/
├── Pages/
│   └── Home.razor             # Main page ("/"), top-level game state controller
├── Components/                # Reusable Blazor components
│   ├── BingoBoard.razor       # 5×5 grid renderer
│   ├── BingoSquare.razor      # Individual cell (button with state)
│   ├── GameScreen.razor       # Game board wrapper with header/instructions
│   ├── StartScreen.razor      # Splash/start UI
│   └── BingoModal.razor       # Bingo win overlay
├── Models/
│   ├── GameState.cs           # Enum: Start | Playing | Bingo
│   ├── BingoSquareData.cs     # Data: Id, Text, IsMarked, IsFreeSpace
│   └── BingoLine.cs           # Data: Type, Index, Squares[]
├── Services/
│   ├── BingoGameService.cs    # State manager — single source of truth
│   └── BingoLogicService.cs   # Pure static logic (board generation, bingo detection)
├── Data/
│   └── Questions.cs           # 24 static icebreaker questions + FREE_SPACE
└── wwwroot/
    ├── index.html             # Entry point HTML
    └── css/app.css            # All custom CSS (Tailwind-inspired utility system)
```

> **Note:** `.solutions/` contains frozen step-by-step workshop checkpoints — treat them as read-only reference material.

## State Management

- `BingoGameService` is the **single source of truth** for UI state — all components subscribe to its `OnStateChanged` event and call its methods.
- `BingoLogicService` is **purely static** — no DI, no side effects; safe to call anywhere.
- State is persisted to `localStorage` via `IJSRuntime` (JSON, versioned with a `StoredGameData` nested class).
- Fire-and-forget async pattern used for saves: `_ = SaveGameStateAsync();`

## Styling

Custom CSS utility classes (Tailwind-inspired) live entirely in `wwwroot/css/app.css` — **no npm, no CDN**.

| Category | Examples |
|----------|---------|
| Layout | `.flex`, `.flex-col`, `.grid`, `.grid-cols-5`, `.items-center` |
| Spacing | `.p-4`, `.px-6`, `.mb-2`, `.mx-auto`, `.gap-1` |
| Sizing | `.h-full`, `.w-full`, `.max-w-md`, `.aspect-square` |
| Colors | `.bg-cream`, `.bg-paper`, `.bg-caramel`, `.text-espresso` (see Design Guide) |
| Typography | `.text-xs`–`.text-5xl`, `.font-bold`, `.font-display` (Playfair Display) |
| Borders | `.border`, `.rounded-lg`, `.shadow-xl` |
| Animation | `.transition-all`, `.duration-150`, `.animate-[bounce_0.5s_ease-out]` |

When adding new utilities, follow the existing patterns in `app.css`. See `.github/instructions/css-utilities.instructions.md` for full reference.

## Design Guide

**Theme:** Cozy Coffee Shop — warm, relaxed, like a community board at a local café.

### Color Palette (CSS variables in `:root`)

| Variable | Value | Use |
|----------|-------|-----|
| `--espresso` | `#2c1a0e` | Headings, primary text |
| `--coffee` | `#5c3317` | Secondary text, borders |
| `--latte` | `#c49a6c` | Subtle accents, card borders |
| `--caramel` | `#d4823a` | CTA buttons, marked squares |
| `--cream` | `#faf3e8` | Page background |
| `--paper` | `#f0e6d3` | Card / square backgrounds |
| `--foam` | `#fdf8f0` | Header, modal background |
| `--cinnamon` | `#a0522d` | Active borders, winning highlight |
| `--gold** | `#e8a628` | Winning bingo line squares |

### Typography

- **Headings/brand:** `font-display` — Playfair Display (loaded from Google Fonts)
- **Body/UI:** Nunito (loaded from Google Fonts) — set on `body`
- Loaded via `<link>` in `wwwroot/index.html`

### Component Patterns

| Component utility | Description |
|-------------------|-------------|
| `.card-cozy` | Parchment card: `bg-paper`, `border-latte`, warm shadow |
| `.header-cozy` | Foam header: `bg-foam`, `border-b border-latte` |
| `.btn-primary` | Caramel CTA button with cinnamon active state |
| `.steam-container` / `.steam-line` | Animated steam lines above the coffee cup |

### Bingo Square States

| State | Classes |
|-------|---------|
| Unmarked | `bg-paper border-latte text-espresso` |
| Marked | `bg-caramel border-cinnamon text-foam font-semibold` |
| Winning line | `bg-gold border-cinnamon text-espresso font-bold` |
| Free space | `bg-coffee border-espresso text-foam font-display` |

## Available Copilot Agents

Agents live in `.github/agents/` and can be invoked from VS Code Copilot Chat:

| Agent | File | Purpose |
|-------|------|---------|
| **TDD Supervisor** | `tdd.agent.md` | Multi-agent TDD workflow (write tests → implement → verify) |
| **Quiz Master** | `quiz-master.agent.md` | Generate and update icebreaker questions in `Questions.cs` |
| **UI Review** | `ui-review.agent.md` | Playwright-powered visual UI review and feedback |
| **Pixel Jam** | `pixel-jam.agent.md` | Iterative creative UI design and redesign |

## Available Instructions

Persistent coding guidance in `.github/instructions/`:

- **`css-utilities.instructions.md`** — Full catalog of CSS utilities; when/how to add new ones
- **`frontend-design.instructions.md`** — Design philosophy: avoid "AI slop", commit to distinctive aesthetics

## Tooling

- **Playwright MCP** — browser automation via `@playwright/mcp@latest` (MS Edge); configured in `.vscode/mcp.json`
- **GitHub Actions** — auto-deploys to GitHub Pages on push to `main` (`deploy.yml`)
- **Dev Container** — `.devcontainer/devcontainer.json` uses `.NET 10` image, forwards port `5166`

## Conventions

- PascalCase for public members, component files, and namespaces (`SocOps.Models`, `SocOps.Services`)
- Components use `[Parameter]` + `EventCallback` for parent-child communication
- Component-scoped CSS uses co-located `.razor.css` files
- Scaffolded pages (`Counter.razor`, `Weather.razor`) are not game-relevant and can be ignored
