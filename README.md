# LaunchDarkly AI Configs - Skills & Cookbooks

Skills and cookbook notebooks for working with LaunchDarkly AI Configs.

## Prerequisites

- A LaunchDarkly account with AI Configs enabled
- An API access token with appropriate permissions (`ai-configs:write`, `segments:write`, `/*:ai-tool/*`)
- Python 3.9+ installed
- Environment variable `LAUNCHDARKLY_API_TOKEN` set

## Skills Overview

### Foundation

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-projects](./aiconfig-projects/SKILL.md) | [cookbook](./aiconfig-projects/cookbook_aiconfig_projects.ipynb) | Create project and get SDK key |

### Create & Manage Configs

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-tools](./aiconfig-tools/SKILL.md) | [cookbook](./aiconfig-tools/cookbook_aiconfig_tools.ipynb) | Create tools for function calling |
| [aiconfig-create](./aiconfig-create/SKILL.md) | [cookbook](./aiconfig-create/cookbook_aiconfig_create.ipynb) | Create AI Configs with variations |
| [aiconfig-variations](./aiconfig-variations/SKILL.md) | [cookbook](./aiconfig-variations/cookbook_aiconfig_variations.ipynb) | Manage config variations |
| [aiconfig-update](./aiconfig-update/SKILL.md) | [cookbook](./aiconfig-update/cookbook_aiconfig_update.ipynb) | Update, archive, delete configs |

### SDK Usage

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-context-basic](./aiconfig-context-basic/SKILL.md) | [cookbook](./aiconfig-context-basic/cookbook_aiconfig_context_basic.ipynb) | Basic context patterns |
| [aiconfig-context-advanced](./aiconfig-context-advanced/SKILL.md) | [cookbook](./aiconfig-context-advanced/cookbook_aiconfig_context_advanced.ipynb) | Advanced multi-context patterns |
| [aiconfig-sdk](./aiconfig-sdk/SKILL.md) | [cookbook](./aiconfig-sdk/cookbook_aiconfig_sdk.ipynb) | Consume configs with SDK |

### Targeting

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-segments](./aiconfig-segments/SKILL.md) | [cookbook](./aiconfig-segments/cookbook_aiconfig_segments.ipynb) | Create segments for targeting |
| [aiconfig-targeting](./aiconfig-targeting/SKILL.md) | [cookbook](./aiconfig-targeting/cookbook_aiconfig_targeting.ipynb) | Configure targeting rules |

### Metrics & Monitoring

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-ai-metrics](./aiconfig-ai-metrics/SKILL.md) | [cookbook](./aiconfig-ai-metrics/cookbook_aiconfig_ai_metrics.ipynb) | Built-in AI metrics tracking |
| [aiconfig-online-evals](./aiconfig-online-evals/SKILL.md) | [cookbook](./aiconfig-online-evals/cookbook_aiconfig_online_evals.ipynb) | LLM-as-a-judge evaluations |
| [aiconfig-custom-metrics](./aiconfig-custom-metrics/SKILL.md) | [cookbook](./aiconfig-custom-metrics/cookbook_aiconfig_custom_metrics.ipynb) | Custom business metrics |

### API Reference

| Skill | Cookbook | Purpose |
|-------|----------|---------|
| [aiconfig-api](./aiconfig-api/SKILL.md) | [cookbook](./aiconfig-api/cookbook_aiconfig_api.ipynb) | API access patterns and authentication |

## Environment Variables

| Variable | Source | Used By |
|----------|--------|---------|
| `LAUNCHDARKLY_API_TOKEN` | LaunchDarkly UI (Authorization settings) | All API-based skills |
| `LAUNCHDARKLY_SDK_KEY` | `aiconfig-projects` skill output | All SDK-based skills |
| `OPENAI_API_KEY` | OpenAI | AI Metrics, Online Evals |

## Notes

- **Agent Mode vs Completion Mode**: Online evaluations (judges) only work with completion-mode configs, not agent-mode configs.
- **Tools are Optional**: You don't need to create tools if your AI Config doesn't use function calling.
- **Enable Judges**: Before using `aiconfig-online-evals`, enable judges in the LaunchDarkly UI.
