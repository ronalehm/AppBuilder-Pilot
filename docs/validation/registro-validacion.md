# Registro de validación — AppBuilder-Pilot

- **Fecha:** 2026-11-24
- **Modalidad:** guiada (A1–A10 y T1–T3) y conformidad directa del propietario (A12 y A14).
- **Commit de origen del template:** `05aee0090304b718b2ab5f3215de9f24cdca3af9`
- **Commit base de la aplicación:** `f9b84f5a1d5794b54c95328a56eb5c311661e602` (igual al template, sin historia en común).
- **Dictamen A14:** ACEPTADA_POR_USUARIO (no CERRADA). Bajo responsabilidad del propietario.

## Etapas técnicas

| Etapa | Estado | Evidencia |
|---|---|---|
| A1 Entorno | PASS | EJECUTADA: git 2.49.0, node v26.12.1, npm 11.20.0, claude 2.1.331, gh autenticado |
| A2 Clonación | PASS | EJECUTADA: `npm ci --ignore-scripts`, exit 0 |
| A3 Remotos | PASS | EJECUTADA: `origin` = repo de la aplicación, `upstream` = template, `main` rastrea `origin/main` |
| A4 Principio | PASS | DECLARADA y EJECUTADA: repo, Clerk y Neon propios; Vercel diferido |
| A5 Clerk | PASS | REPORTADA: llaves definidas. Métodos (email y contraseña) DECLARADA, validados en A10 |
| A6 Neon | PASS | REPORTADA: mismo proyecto, pooled y directa correctas, base `neondb`. Rama Developer confirmada por el propietario |
| A7 Variables | PASS | EJECUTADA: `.env.local` ignorado por Git. REPORTADA: destino correcto y sin variables heredadas |
| A8 Migraciones | PASS | EJECUTADA: 5 migraciones aplicadas, exit 0 |
| A9 Superadmin | PASS | EJECUTADA: rol `superadmin`, estado `active` |
| A10 Arranque | PASS | EJECUTADA: HTTP 200 en `/` y `/sign-in`. Visual DECLARADA |
| A11 Webhook | PASS | REPORTADA: HTTP 200 con `{"status":"ok"}` al evento `user.deleted`. EJECUTADA: la fila de la cuenta eliminada quedó con `clerk_deleted_user_id` igual a su `clerk_user_id` |
| T1 Lint | CUMPLIDO | EJECUTADA: `npm run lint`, exit 0 |
| T2 Tests | CUMPLIDO | EJECUTADA: `npx vitest run`, exit 0. 936 pasan, 7 omitidas (integridad, sin base desechable) |
| T3 Build | CUMPLIDO | EJECUTADA: `npm run build`, exit 0 |
| T4 Integridad | NO_EJECUTADO | Sin base desechable confirmada. Aceptado expresamente por el propietario para v1.0.0 |

## Conformidad funcional (A12)

El propietario confirmó F1 a F10 como conformes (DECLARADA). Evidencia técnica adicional:

- F1 y F2: `200` del documento y consola sin errores de la aplicación (REPORTADA).
- F3: listado de usuarios con `200` (REPORTADA) y operación de cambio de rol sobre la cuenta de prueba.
- F4: perfil con datos correctos (REPORTADA).
- F5: preferencia persistida en el almacenamiento local tras recargar (REPORTADA).
- F8: efecto del webhook verificado en Neon (EJECUTADA).

## Observaciones abiertas (no bloquean la conformidad registrada)

- Tras el cambio de rol de la cuenta de prueba, la interfaz mostró "Administrador", pero en Neon figura como `user`. Queda sin resolver.
- Las llaves de Clerk en uso son de desarrollo. Las de producción deben configurarse antes de desplegar.
- Next.js advierte sobre un `package-lock.json` en el directorio de usuario, fuera del repo. No afecta la aplicación.

## Limitaciones aceptadas por el propietario

- T4 queda NO_EJECUTADO para v1.0.0.
- Clerk de desarrollo en uso.
