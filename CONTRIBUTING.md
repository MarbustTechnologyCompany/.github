# Flujo de trabajo — Marbust Technology Company

GitHub Issues es el **backlog canónico** de todo el trabajo planificado, bugs, decisiones y follow-ups. Trello da el tablero visual; los Issues son la **fuente de verdad**. Estas reglas aplican a **todos los repos** de la empresa (y personales).

## El flujo, en orden (sin saltarse pasos)

1. **Tarjeta en Trello** — en el tablero correcto (Marbust System / Sitios Webs Clientes / Marbust Technology Company), con marca + severidad + ejecutor + "cómo probar".
2. **Issue en GitHub** — lo abre la cuenta **`MarbustTechnologyCompany`** (el "PO/empresa"), usando la plantilla (Bug o Work item). Enlaza la tarjeta de Trello.
3. **PR** — lo envía **`MarAntBQ`** (el dev) desde una rama nueva (NUNCA a `main` directo). Vincula el Issue (`Closes #N` / `Refs #N`).
4. **QA + Aprobación** — quien hace el **QA** (Codex o Claude) **aprueba el PR como `MarbustTechnologyCompany`** (el autor no se auto-aprueba: separación autor↔revisor).
5. **Producción** — recién DESPUÉS del PR aprobado/mergeado se despliega, y **cada deploy requiere el OK explícito de Marco**.

## Cómo se escribe un Issue

Un buen Issue permite decidir e implementar sin acceso a una conversación privada:

- **Un Issue = un resultado independientemente revisable** (un outcome, un bug o una decisión).
- Debe traer: el **problema/outcome**, el **alcance** y las **exclusiones**, **criterios de aceptación** concretos, la **verificación** para cerrarlo, y **enlaces** a código/docs/contratos/incidentes/tarjeta.
- Para trabajo sensible (dinero, SRI, identidad, proveedores) lista los **gates externos por separado**: un PR mergeado NO prueba un deploy, una migración, un smoke autenticado, un UAT de proveedor ni la activación en producción.
- **Nunca** pongas credenciales, tokens, cadenas de conexión, datos de clientes ni PII en un Issue.
- Se cierra cuando **se desplegó, se descartó o quedó superado**. Si el PR no lo cerró solo, deja un comentario con el motivo. (Ojo: GitHub solo reconoce `Closes/Fixes/Resolves` en **inglés**, no "Cierra".)

## Cómo se abre un PR

- Rama nueva por tarea; **el fix nunca va directo a `main`**.
- Descripción con la plantilla: **Resumen · Issue vinculado · Verificación (real, con output) · Evidencia de release (solo gates probados) · Seguridad y operaciones**.
- Marca **solo** la evidencia que de verdad pasó; `N/A` con motivo para lo que no aplique.
- **Merge = squash** (1 commit por PR) + borrar la rama.
- **Sin co-autoría de Claude** en commits ni en la descripción del PR.

## Identidades (2 cuentas)

- **`MarbustTechnologyCompany`** (dueña de los repos) → **crea Issues y aprueba PRs**.
- **`MarAntBQ`** (dev) → **hace ramas y PRs**.

## Nota

El bloqueo server-side de "no `main` sin PR" (branch protection) requiere **GitHub Pro** en repos privados; sin él, este flujo se sostiene por convención + la revisión/aprobación del PR.
