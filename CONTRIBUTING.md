# Flujo de trabajo — Marbust Technology Company

GitHub Issues es el **backlog canónico** de todo el trabajo planificado, bugs, decisiones y follow-ups: es la **fuente de verdad**. Estas reglas aplican a **todos los repos**.

## El flujo, en orden (sin saltarse pasos)

1. **Issue en GitHub** — lo abre la cuenta **`MarbustTechnologyCompany`**, usando la plantilla (Bug o Work item). Un Issue = un solo resultado independientemente revisable.
2. **PR** — lo envía **`MarAntBQ`** desde una rama nueva (NUNCA a `main` directo). Vincula el Issue (`Closes #N` / `Refs #N`, en inglés).
3. **Revisión + Aprobación** — el revisor aprueba el PR como **`MarbustTechnologyCompany`** (el autor no se auto-aprueba: separación autor↔revisor).
4. **Producción** — recién DESPUÉS del PR aprobado/mergeado se despliega, y **cada deploy requiere aprobación explícita del responsable**.

## Cómo se escribe un Issue

Un buen Issue permite decidir e implementar sin acceso a una conversación privada:

- **Un Issue = un resultado independientemente revisable** (un outcome, un bug o una decisión).
- Debe traer: el **problema/outcome**, el **alcance** y las **exclusiones**, **criterios de aceptación** concretos, la **verificación** para cerrarlo, y **enlaces** a código/docs/contratos/incidentes.
- Para trabajo sensible (dinero, impuestos, identidad, proveedores) lista los **gates externos por separado**: un PR mergeado NO prueba un deploy, una migración, un smoke autenticado, un UAT de proveedor ni la activación en producción.
- **Nunca** pongas credenciales, tokens, cadenas de conexión, datos de clientes ni PII en un Issue.
- Se cierra cuando **se desplegó, se descartó o quedó superado**. Si el PR no lo cerró solo, deja un comentario con el motivo. (GitHub solo reconoce `Closes/Fixes/Resolves` en **inglés**.)

## Cómo se abre un PR

- Rama nueva por tarea; **el trabajo nunca va directo a `main`**.
- Descripción con la plantilla: **Resumen · Issue vinculado · Verificación (real, con output) · Evidencia de release (solo gates probados) · Seguridad y operaciones**.
- Marca **solo** la evidencia que de verdad pasó; `N/A` con motivo para lo que no aplique.
- **Merge = squash** (1 commit por PR) + borrar la rama.
