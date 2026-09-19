# condia-grok-avatars

Fotos de los agentes de **GrokBot** en Condia (gestión de proyecto y auditoría).

Público a propósito: Slack necesita que `icon_url` sea accesible sin login para pintar la foto
en cada mensaje.

## Cómo se usan

La app de Slack **Condia Ops** (`A0C35GFFY0H`) postea con el scope `chat:write.customize`, que
permite pasar `username` e `icon_url` por mensaje. Una app, ocho personas.

```json
{
  "channel":  "C0BSP4YJRCK",
  "text":     "DEV-42 pasa a Listo para QA.",
  "username": "Laura Méndez · PM",
  "icon_url": "https://raw.githubusercontent.com/CedenoH07/condia-grok-avatars/main/pm.jpg"
}
```

## Las ocho

| Archivo | Persona | Rol |
|---|---|---|
| `pm.jpg` | Laura Méndez | PM / BO Monday + handoff |
| `cos.jpg` | Alex Mendoza | Chief of Staff |
| `web-own.jpg` | Tomás Herrera | Dueño web Next.js |
| `fb-own.jpg` | Marco Salcedo | Dueño Firebase / rules |
| `qa.jpg` | Valentina Ruiz | QA vs ticket Monday |
| `rel.jpg` | Diego Navarro | Release (≠ merge) |
| `legal.jpg` | Patricia Gómez | Legal |
| `sme.jpg` | Margaret Walsh | SME HOA |

URL base: `https://raw.githubusercontent.com/CedenoH07/condia-grok-avatars/main/<archivo>`

## Reemplazar una foto

GitHub exige el `sha` del archivo actual al sobrescribir:

```bash
gh api -X PUT repos/CedenoH07/condia-grok-avatars/contents/pm.jpg \
  -f message="nueva foto de Laura" \
  -f sha="$(gh api repos/CedenoH07/condia-grok-avatars/contents/pm.jpg --jq .sha)" \
  -f content="$(base64 -i nueva.jpg | tr -d '\n')"
```

Slack cachea los avatares un rato: el cambio puede tardar en verse.

## Las otras dos AI

| AI | App de Slack | Avatares |
|---|---|---|
| Claude (código) | `@Claude` | `CedenoH07/office-avatars` → `condia/` |
| ChatGPT (diseño) | Condia Design `A0C2YLLDR1B` | `CedenoH07/office-avatars` → `condia/` |
| GrokBot (PM/auditoría) | Condia Ops `A0C35GFFY0H` | este repo |

Definición completa del reparto: `office/agents/identities.json` en `Hecmapp/condia`.
