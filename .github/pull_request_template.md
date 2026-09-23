## Resumen

<!-- ¿Qué cambió y por qué? -->

## Issue vinculado

<!-- `Closes #123` si al mergear este PR se completa el issue, o `Refs #123` si es solo parte. -->

## Verificación

<!-- Los comandos, tests y chequeos manuales seguros que REALMENTE pasaron. Pega el output. -->

- [ ] Tests enfocados
- [ ] `tsc` sin errores (`npx tsc --noEmit` backend · `tsc -p tsconfig.app.json --noEmit` frontend)
- [ ] QA de Codex o Claude (revisión del diff + verificación)

## Evidencia de release

<!-- Marca SOLO los gates probados. Escribe N/A con motivo para lo que no aplique. Un PR mergeado NO prueba deploy/migración/UAT. -->

- [ ] Revisión de código + CI
- [ ] Migración / ALTER aplicado y verificado (si tocó entidades; prod `synchronize:false`)
- [ ] Listo para desplegar
- [ ] Smoke autenticado en navegador
- [ ] **Aprobado por MarbustTechnologyCompany** (el autor —MarAntBQ— no se auto-aprueba)
- [ ] **Activación en producción aprobada explícitamente por Marco**

N/A o gates pendientes:

## Seguridad y operaciones

<!-- Migración de datos, PII, movimiento de dinero, SRI, efectos en proveedores, feature flags, rollback o condiciones de stop. Escribe N/A si no aplica. -->
