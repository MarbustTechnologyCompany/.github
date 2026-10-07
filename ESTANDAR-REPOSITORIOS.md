# Estándar de repositorios — Marbust Technology Company

Este documento es la **fuente única** de cómo se organiza **todo** repositorio de Marbust Technology Company, sin excepción. Cada repo lo **adapta** a lo suyo; no lo reinventa.

**El objetivo de fondo:** si mañana se contrata a un programador, tiene que poder continuar cualquier proyecto leyendo **solo su repo**, sin que nadie se lo explique en persona.

La implementación de referencia es **`MediMarbustSaaS`** (producto SaaS) y **`MarAntBQ/CallingSupportApp`** (open source). Cuando este documento y un repo de referencia difieran en un detalle, manda lo que esté **implementado y probado** en la referencia; este documento se corrige.

---

## 1. Qué lleva todo repo

Adaptado al tipo de repo (producto SaaS, sitio/app de cliente, app móvil, API, herramienta interna):

| Archivo | Qué lleva |
|---|---|
| `README.md` | Qué es y qué **no** es, documentación, cómo colaborar. **Sin estado escrito a mano** ("ya está", "lo siguiente", "hoy hace"): el avance se ve en issues, milestones y novedades automáticas |
| `docs/ONBOARDING.md` | Primer día: qué leer y en qué orden, accesos que pedir (y cuáles **no**), herramientas, cómo levantar el proyecto, primer issue, cuentas de GitHub, cómo pedir ayuda, lo que nunca se hace |
| `CONTRIBUTING.md` | El recorrido completo tarjeta → issue → PR → QA → merge: ramas, commits, instalación local, uso de IA |
| `AGENTS.md` + `CLAUDE.md` (`@AGENTS.md`) | **Clase** del repo (§2), stack decidido, estructura, idiomas y glosario, reglas duras, seguridad, interfaz, skills. Para todas las personas y agentes de IA |
| `SECURITY.md` | Cómo se reporta una vulnerabilidad en privado y qué pasa ante una filtración |
| `.github/marbust.json` | `{ "producto": "<nombre>", "clase": "producto\|cliente\|interno" }` (§2) |
| `.github/ISSUE_TEMPLATE/` | `bug.yml`, `work-item.yml`, `modulo.yml` (cuando aplique) y `config.yml` con `blank_issues_enabled: false` |
| `.github/pull_request_template.md` | Plantilla de la empresa + **Cómo probar** + sección **Novedad** (§4) |
| `.github/scripts/pr-checks.mjs` (+ `pr-checks.test.mjs`) | Checker de título y sección Novedad (§4) |
| `.github/workflows/pr-checks.yml` | Check **Checks del PR**: corre el checker **de la rama base** para que un PR no pueda saltárselo (§4) |
| `.claude/skills/` | `trabajar-un-issue`, `escribir-un-issue`, `revisar-codigo` y la skill de los **datos sensibles** del dominio (§5) |
| Ajustes del repo | Solo **squash merge**; **borrar la rama** al mergear (§6) |

**Reglas de redacción de los documentos:** en español, con **tuteo**; **autocontenidos** (nada que dependa de una conversación privada); **sin secretos**; **sin datos reales** de clientes ni de personas.

---

## 2. La clase del repo

Cada repo declara su **clase** en `.github/marbust.json` y la repite en `AGENTS.md`. La clase decide si puede tener **novedades públicas**.

| Clase | Ejemplos | Novedad pública | Novedad interna |
|---|---|---|---|
| **`producto`** — producto de la empresa | Marbust System, MarbustStore, MediMarbust, el CMS de Marbust Websites, MBHostCloud, MBRelax | **Sí**, revisada en el PR | Sí |
| **`cliente`** — sitio o app de un cliente | La web de un cliente, su CMS instalado, su API | **Nunca** | Sí, para el equipo |
| **`interno`** — herramienta interna | Bots, scripts del VPS, configuraciones, colecciones, plugins | **Nunca** | Sí |

`marbust.json`:

```json
{
  "producto": "Marbust System",
  "clase": "producto"
}
```

En un repo de cliente, una mejora **no** sale en lo público. Pero si esa mejora se hizo en **el producto** (por ejemplo, el CMS), el PR del repo del producto **sí** la anuncia.

**Repos personales de Marco Antonio (cuenta `MarAntBQ`):** aplican el mismo estándar, con dos diferencias: el flujo es **self-managed** (la empresa no abre sus issues ni aprueba sus PRs; él abre issue + PR y mergea tras el QA de Codex) y **no alimentan el log público** de `developers.marbust.com` (eso es solo de productos de la empresa). Su sección Novedad queda **solo interna**. Los repos de cliente que vivan en su cuenta personal llevan la misma excepción de §6.

---

## 3. El flujo de trabajo

El detalle vive en el `CONTRIBUTING.md` de la empresa (y el de cada repo lo referencia). En orden, sin saltarse pasos:

1. **Tarjeta** en Trello (tablero del proyecto) con marca, severidad, rol y ejecutor.
2. **Issue** en GitHub — lo abre **`MarbustTechnologyCompany`**, con la plantilla. Un issue = **un resultado** independientemente revisable, autocontenido.
3. **Rama** nueva — el trabajo **nunca** va directo a `main`.
4. **PR** — lo envía **`MarAntBQ`** (o quien implemente, con su cuenta). Se abre en **borrador** con la plantilla llena, vincula el issue (`Closes #N` / `Refs #N`, en inglés).
5. **QA** — **Codex participa siempre**: si Codex implementó, el QA lo hace Claude, y al revés. Antes del PR se corre la skill `revisar-codigo` sobre el propio diff.
6. **Aprobación** — aprueba **`MarbustTechnologyCompany`** (el autor **no** se auto-aprueba: separación autor↔revisor).
7. **Squash** — un issue, un PR, un commit. Se borra la rama.
8. **Producción** — recién después del merge. Los repos con auto-deploy despliegan al mergear; los demás, con el OK explícito del responsable.

**Commits:** con tipo (`feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `perf`), en español. **Prohibido** agregar líneas de co-autoría de herramientas de IA, en commits y en PRs.

---

## 4. Novedades automáticas desde los PRs

Ningún README ni ningún sitio documenta los cambios **a mano**. Las novedades **salen solas de los PRs mergeados**. La parte pública funciona como el **newsroom de lo que desarrolla la empresa**: solo mejoras y funcionalidades de **nuestros productos**.

La plantilla de PR de **todos** los repos trae esta sección:

```markdown
## Novedad

<!-- Una línea por público. Escribe "ninguna" si no aplica. La línea pública la puede leer
cualquiera: nada de vulnerabilidades, infraestructura, nombres de clientes ni datos internos. -->

- pública:
- interna:
- hito: no
```

- **pública:** qué cambia para el cliente o el usuario, en una frase. Ej.: «MediMarbust ya incluye facturación electrónica.»
- **interna:** qué cambió para el equipo (puede mencionar módulos, decisiones técnicas, issues).
- **hito:** `sí` cuando es un logro público destacado del producto; `no` el resto.
- Los PRs de dependencias (`dependabot`, `renovate`) y los marcados `ninguna` no generan novedad.
- **Arreglos de seguridad:** la línea pública **nunca** describe la falla. Como mucho: «Mejoras de seguridad.»
- El revisor del PR revisa **también** la línea pública: si pone en riesgo la seguridad o expone algo interno, es un `[bug]` que bloquea.

**En repos de clase `cliente` e `interno`, la plantilla de PR va sin las líneas `pública` ni `hito`** (solo `interna`), y el check las **rechaza** si aparecen.

**El checker** (`.github/scripts/pr-checks.mjs`, con sus pruebas `pr-checks.test.mjs`) valida dos cosas: el **título** del PR (empieza con un tipo: `feat`/`fix`/`docs`/…) y la sección **Novedad** según la clase del repo (`producto` exige las tres líneas; `cliente`/`interno` solo `interna` y rechazan `pública`/`hito`). El workflow **`pr-checks.yml`** (check **Checks del PR**) corre el checker **de la rama base**, no el del PR, para que un PR no pueda saltárselo editando su propio checker; y exige que el PR vaya contra `main`.

**Límite conocido (a decidir con Marco Antonio):** en repos privados de una **cuenta personal**, GitHub no permite *required status checks* ni protección de rama sin **GitHub Pro** (la API responde 403). Sin eso, un check en rojo no bloquea el merge y un PR podría editar su propio workflow. Hoy lo cubren la revisión (skill `revisar-codigo`) y la aprobación de la empresa. La decisión —pagar GitHub Pro vs. pasar los repos a la organización— la toma Marco Antonio.

El `README.md` de cada repo de producto enlaza a su página pública de novedades en **developers.marbust.com**, junto a los badges de avance por milestone.

---

## 5. Las skills: dos rutas

Cada repo lo explica en `AGENTS.md`, `CONTRIBUTING.md` y `docs/ONBOARDING.md`:

1. **Colaboradores nuevos o externos** trabajan con las skills que vienen **dentro del repo** (`.claude/skills/`). Es una copia pensada para quien no tiene acceso a nada más. Claude Code las carga al abrir el repo; con otros agentes, se les pasa el `SKILL.md`.
2. **Colaboradores oficiales de Marbust** trabajan con el **directorio oficial de la empresa**: el repo privado `MarbustTechnologyCompany/ClaudeSkills` (clonado en `~/.claude/skills`). **Es la fuente de verdad.**

Cómo se mantienen:

- Las skills del repo se actualizan **a mano desde el directorio oficial**, con su propio PR, cuando cambia la versión oficial.
- Si alguien mejora una skill dentro de un repo, la mejora se lleva **primero al directorio oficial** y desde ahí se vuelve a copiar. Nunca hay dos versiones distintas que se ignoren.
- Cada copia en un repo dice al inicio que es una copia del directorio oficial, con la fecha o el commit de la última sincronización.

Las cuatro skills base de todo repo: `trabajar-un-issue`, `escribir-un-issue`, `revisar-codigo` (**obligatoria** antes de abrir un PR y al revisar el de otro) y la skill de los **datos sensibles** del dominio (por ejemplo `datos-de-pacientes` en MediMarbust).

---

## 6. La excepción de los repos de cliente

Los repos de **clase `cliente`** no llevan **atribución a IA** ni **andamiaje interno visible para el cliente**. El estándar se aplica en la forma que corresponda sin romper esa regla:

- **Clase `cliente`** en `marbust.json`, **nunca** novedad pública.
- Los documentos internos (AGENTS, CONTRIBUTING, skills, plantillas) **no** se entregan al cliente ni describen infraestructura de Marbust en lo que el cliente pueda ver. Si el repo se comparte con el cliente, el andamiaje de colaboración se mantiene fuera de lo que él recibe.
- Sin menciones a herramientas de IA en commits, PRs, README ni en el código.
- Lo demás del estándar (flujo, issues/PRs con plantilla, `revisar-codigo`, squash) **sí** aplica, para el equipo.

Caso por caso, si un repo de cliente necesita apartarse de algo del estándar, se deja **escrito en su `AGENTS.md`** el motivo.

---

## 7. Ajustes del repo en GitHub

- **Solo squash merge** habilitado (merge commit y rebase deshabilitados).
- **Borrar la rama** automáticamente al mergear.
- Check **Checks del PR** como *required status check* **donde GitHub lo permita** (ver el límite de §4).
- Issues en blanco deshabilitados (`config.yml` con `blank_issues_enabled: false`).

---

## 8. Cómo se aplica

Por **partes**, con el flujo de §3: **un PR por repo**, con su tarjeta e issue, QA de Codex, aprobación de la empresa, squash y —para los submódulos del paraguas `ClaudeSessionsMBTech`— el **bump del paraguas** después del merge. Nada de cambios masivos sin revisión.

Prioridad: primero los **productos** activos de la empresa, después las **apps y herramientas**, al final los **repos de clientes** con su excepción. El paraguas se mantiene sincronizado en la PC y en el VPS devbox para no perder continuidad.
