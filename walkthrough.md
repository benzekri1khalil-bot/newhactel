# HACTEL Internal Tools Platform — Walkthrough

## Build Status: ✅ Production Build Successful

The platform has been fully built and verified with Next.js 16.2.9 (Turbopack).

## All Routes

| Route | Description |
|-------|-------------|
| `/login` | Glassmorphic login page with ambient particle animation |
| `/` | Main dashboard with tool grid, service info, AI chat |
| `/admin` | Admin control panel (stats, users, messages, settings) |
| `/tools/datasheet-generator` | AI-powered branded PowerPoint datasheet generator |
| `/tools/pdf-to-pptx` | PDF to PowerPoint converter with theme options |
| `/tools/translator` | Document translator with DOCX extraction support |

## Architecture

### Tech Stack
- **Framework**: Next.js 16 (App Router, TypeScript, Turbopack)
- **Styling**: Tailwind CSS with custom HACTEL design tokens (gold/dark theme)
- **3D Effects**: Three.js via `@react-three/fiber` + `@react-three/drei`
- **Document Generation**: `pptxgenjs` for branded PowerPoint export
- **Document Parsing**: `mammoth` for Word document extraction
- **Icons**: `lucide-react`
- **Persistence**: `localStorage` (no database required)

### Key Files

| File | Purpose |
|------|---------|
| [AppContext.tsx](file:///C:/Users/pc/.gemini/antigravity-ide/scratch/hactel-internal-tools/src/context/AppContext.tsx) | Central state management (users, credits, history, sessions) |
| [ProtectedLayout.tsx](file:///C:/Users/pc/.gemini/antigravity-ide/scratch/hactel-internal-tools/src/components/ProtectedLayout.tsx) | Auth-guarded layout with sidebar nav, command palette |
| [ThreeBackground.tsx](file:///C:/Users/pc/.gemini/antigravity-ide/scratch/hactel-internal-tools/src/components/ThreeBackground.tsx) | 3D wireframe boxes + particles + mouse parallax |
| [pptxGenerator.ts](file:///C:/Users/pc/.gemini/antigravity-ide/scratch/hactel-internal-tools/src/utils/pptxGenerator.ts) | HACTEL-branded A4 portrait PPTX template generator |
| [productDb.ts](file:///C:/Users/pc/.gemini/antigravity-ide/scratch/hactel-internal-tools/src/utils/productDb.ts) | Hardware specification database (Cisco, etc.) |

## TypeScript Fixes Applied

Three categories of pptxgenjs type errors were resolved:

1. **Missing `bold` property**: TypeScript inferred table row types from header cells (which had `bold: true`), requiring all data cells to also include `bold`. Added `bold: false` to 4 data cells.

2. **`width` → `pt`**: pptxgenjs `BorderProps` uses `pt` instead of `width` for border thickness. Fixed across 5 occurrences (3 table borders + 2 shape lines).

3. **`write("blob")` → `write({ outputType: "blob" })`**: pptxgenjs v4+ changed the `write()` API to accept a `WriteProps` object.

## How to Run

```powershell
cd C:\Users\pc\.gemini\antigravity-ide\scratch\hactel-internal-tools
$env:Path = "C:\Users\pc\AppData\Local\Microsoft\WinGet\Packages\OpenJS.NodeJS.LTS_Microsoft.Winget.Source_8wekyb3d8bbwe\node-v24.16.0-win-x64;" + $env:Path
npm run dev
```

Then open **http://localhost:3000/login** in your browser.

### Default Accounts

| Username | Password | Role |
|----------|----------|------|
| `admin` | `admin123` | Admin (unlimited credits) |
| `manager1` | `manager123` | Manager |
| `worker1` | `worker123` | Worker |

## Verification

- ✅ `npm run build` — Production build passes cleanly (0 errors)
- ✅ All 7 routes compiled and statically generated
- ✅ TypeScript strict mode satisfied
- ✅ Dev server launched on `localhost:3000`
