<!-- Ábrelo como borrador (Draft) apenas empieces, con `Refs #<número>`. Cuando esté listo, cámbialo a `Closes #<número>` y márcalo como listo para revisión. La plantilla se llena completa también en borrador. -->

## Resumen

<!-- Qué cambió y por qué. Si el PR hace algo más o distinto de lo que pidió el issue, dilo aquí. -->

## Novedad

<!-- La sección Novedad del PR es lo que alimenta las novedades del producto; su formato lo valida el check "Checks del PR". Una línea por público; "ninguna" si no aplica.
Esta plantilla es la de la organización (repos de clase `interno`): solo línea interna. Un repo de clase `producto` adapta su propia plantilla y agrega "pública" e "hito"; uno de `cliente` tampoco las lleva. Ver ESTANDAR-REPOSITORIOS.md. -->

- interna:

## Issue vinculado

<!-- `Closes #123` si al mergear este PR se completa el issue, o `Refs #123` si es solo parte. En inglés: GitHub no reconoce "Cierra". -->

## Cómo probar

<!-- Pasos para que el revisor lo compruebe por su cuenta: entorno (local/demo), rol, ruta, qué hacer y qué debería ver. -->

1.

## Verificación

<!-- Solo lo que SÍ se corrió, con el output pegado. Un checkbox marcado sin haberlo probado convierte el PR en un documento que miente. N/A con el motivo si no aplica. -->

- [ ] Tests / checks enfocados (pega el output)
- [ ] Revisión del propio diff con la skill `revisar-codigo`
- [ ] QA de Codex (o de Claude, si Codex implementó)

## Evidencia de release

<!-- Marca SOLO los gates probados. Un PR mergeado NO prueba deploy, migración ni activación. -->

- [ ] Revisión de código + CI
- [ ] Desplegado y verificado (si aplica)
- [ ] Revisado y aprobado por el revisor asignado (el autor no se auto-aprueba)

N/A o gates pendientes:

## Seguridad y operaciones

<!-- Credenciales, PII, datos de clientes, migraciones, infraestructura, rollback. N/A si no aplica. -->

- [ ] No se agregaron credenciales, `.env`, secretos ni datos reales de clientes/personas

---

> Este PR entra a `main` por **squash**. Un issue, un PR, un commit. Sin co-autoría de IA en commits ni en PRs.
