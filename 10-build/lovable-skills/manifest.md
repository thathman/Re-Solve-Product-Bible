# Re:Solve Lovable Skill Manifest

This manifest is the canonical inventory for workspace skill installation and review.

| Skill | Canonical path | Primary trigger | FOUND-001 | Auto-use |
|---|---|---|---:|---:|
| resolve-feature | `resolve-feature/SKILL.md` | bounded feature implementation | Required | On |
| resolve-ui | `resolve-ui/SKILL.md` | UI/component/page refinement | Required | On |
| resolve-shell | `resolve-shell/SKILL.md` | app shell/global chrome | Required | On |
| resolve-navigation | `resolve-navigation/SKILL.md` | route/nav hierarchy changes | Required | On |
| resolve-responsive | `resolve-responsive/SKILL.md` | cross-device layout review | Required | On |
| resolve-accessibility | `resolve-accessibility/SKILL.md` | WCAG/accessibility review | Required | On |
| resolve-design-review | `resolve-design-review/SKILL.md` | final visual/design QA | Required | On |
| resolve-security-review | `resolve-security-review/SKILL.md` | auth/sensitive/high-risk review | Required | On |
| resolve-pwa | `resolve-pwa/SKILL.md` | PWA/offline/cache/push | Required | On |
| resolve-release | `resolve-release/SKILL.md` | end-of-slice go/no-go | Required | On |
| self-host-check | `self-host-check/SKILL.md` | portability review | Required | On |
| resolve-form | `resolve-form/SKILL.md` | forms/intake/settings | No | On |
| resolve-data-table | `resolve-data-table/SKILL.md` | operational lists/tables | No | On |
| resolve-record-workspace | `resolve-record-workspace/SKILL.md` | record 360/detail workspaces | No | On |
| resolve-dashboard | `resolve-dashboard/SKILL.md` | dashboards/summary analytics | No | On |
| resolve-portal | `resolve-portal/SKILL.md` | Client Portal/client-safe flows | No | On |
| resolve-notifications | `resolve-notifications/SKILL.md` | notifications/delivery/preferences | No | On |
| resolve-attention | `resolve-attention/SKILL.md` | unresolved Attention Items | No | On |
| resolve-action-registry | `resolve-action-registry/SKILL.md` | reusable business actions | No | On |
| resolve-settings | `resolve-settings/SKILL.md` | settings/configuration control plane | No | On |
| resolve-data-migration | `resolve-data-migration/SKILL.md` | import/export/migration/dedupe | No | On |
| resolve-plugin | `resolve-plugin/SKILL.md` | plugin lifecycle/extensions | No | On |
| resolve-connector | `resolve-connector/SKILL.md` | external provider integration | No | On |
| resolve-automation | `resolve-automation/SKILL.md` | automation/workflow runtime | No | On |
| resolve-api | `resolve-api/SKILL.md` | REST/API/webhooks | No | On |
| resolve-mcp | `resolve-mcp/SKILL.md` | MCP tools/clients | No | On |
| resolve-monitoring | `resolve-monitoring/SKILL.md` | native monitoring/posture/incidents | No | On |
| resolve-document | `resolve-document/SKILL.md` | Document Studio/commercial docs | No | On |
| resolve-ai | `resolve-ai/SKILL.md` | Àríyá/AI tools/provider | No | On |
| resolve-vault | `resolve-vault/SKILL.md` | protected confidential data | No | On |

## Deprecated names
Do not install or retain:
- `airix-feature`
- `airix-ui`
- `airix-form`
- `airix-data-table`
- `airix-security-review`
- `airix-pwa`
- `airix-release`

## Versioning
Until a dedicated skill-package version scheme is needed, Git commit history is the source of version truth. If a skill's behavior materially changes, note the update in the Product Bible PR and refresh the Lovable workspace copy.
