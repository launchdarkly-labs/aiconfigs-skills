# LaunchDarkly AI Configs - Skills & Cookbooks

This document outlines the recommended order for using the AI Config skills and their cookbook notebooks.

## Prerequisites

Before testing any skills, ensure you have:
- A LaunchDarkly account with AI Configs enabled
- An API access token with appropriate permissions (`ai-configs:write`, `segments:write`)
- Python 3.9+ installed
- Environment variable `LAUNCHDARKLY_API_TOKEN` set

## Testing Order

### Phase 1: Foundation (Project Setup)

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 1 | [aiconfig-projects](./aiconfig-projects/SKILL.md) | [cookbook_aiconfig_projects.ipynb](./aiconfig-projects/verification/cookbook_aiconfig_projects.ipynb) | Create project and get SDK key | None |

**Why first?** Creates the project and extracts SDK keys needed for all other skills.

### Phase 2: Create Configs (API-Based)

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 2 | [aiconfig-tools](./aiconfig-tools/SKILL.md) | [cookbook_aiconfig_tools.ipynb](./aiconfig-tools/verification/cookbook_aiconfig_tools.ipynb) | Create tools for function calling | Projects |
| 3 | [aiconfig-create](./aiconfig-create/SKILL.md) | [cookbook_aiconfig_create.ipynb](./aiconfig-create/verification/cookbook_aiconfig_create.ipynb) | Create AI Configs with variations | Projects, Tools |
| 4 | [aiconfig-variations](./aiconfig-variations/SKILL.md) | [cookbook_aiconfig_variations.ipynb](./aiconfig-variations/verification/cookbook_aiconfig_variations.ipynb) | Manage config variations | Configs |

**Why this order?** Tools must be created before configs that reference them. Configs must exist before you can manage variations.

### Phase 3: SDK Usage (Requires Configs)

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 5 | [aiconfig-context-basic](./aiconfig-context-basic/SKILL.md) | [cookbook_aiconfig_context_basic.ipynb](./aiconfig-context-basic/verification/cookbook_aiconfig_context_basic.ipynb) | Basic context patterns | None (pure SDK) |
| 6 | [aiconfig-sdk](./aiconfig-sdk/SKILL.md) | [cookbook_aiconfig_sdk.ipynb](./aiconfig-sdk/verification/cookbook_aiconfig_sdk.ipynb) | Consume configs with SDK | Projects, Configs, Context Basic |

**Why this order?** Context patterns are foundational - you need to understand contexts before using them with the SDK to fetch configs.

### Phase 4: Targeting & Updates

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 7 | [aiconfig-segments](./aiconfig-segments/SKILL.md) | [cookbook_aiconfig_segments.ipynb](./aiconfig-segments/verification/cookbook_aiconfig_segments.ipynb) | Create segments for targeting | Projects |
| 8 | [aiconfig-targeting](./aiconfig-targeting/SKILL.md) | [cookbook_aiconfig_targeting.ipynb](./aiconfig-targeting/verification/cookbook_aiconfig_targeting.ipynb) | Configure targeting rules | Configs, Variations, Segments |
| 9 | [aiconfig-update](./aiconfig-update/SKILL.md) | [cookbook_aiconfig_update.ipynb](./aiconfig-update/verification/cookbook_aiconfig_update.ipynb) | Update, archive, delete configs | Configs |

**Why this order?** Segments should be created before targeting rules that use them. Targeting requires variations to exist. Updates demonstrate config lifecycle.

### Phase 5: Metrics & Monitoring

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 10 | [aiconfig-ai-metrics](./aiconfig-ai-metrics/SKILL.md) | [cookbook_aiconfig_ai_metrics.ipynb](./aiconfig-ai-metrics/verification/cookbook_aiconfig_ai_metrics.ipynb) | Built-in AI metrics tracking | SDK, Configs |
| 11 | [aiconfig-online-evals](./aiconfig-online-evals/SKILL.md) | [cookbook_aiconfig_online_evals.ipynb](./aiconfig-online-evals/verification/cookbook_aiconfig_online_evals.ipynb) | LLM-as-a-judge evaluations | Configs, SDK |
| 12 | [aiconfig-custom-metrics](./aiconfig-custom-metrics/SKILL.md) | [cookbook_aiconfig_custom_metrics.ipynb](./aiconfig-custom-metrics/verification/cookbook_aiconfig_custom_metrics.ipynb) | Custom business metrics | SDK, AI Metrics |

**Important:** For `aiconfig-online-evals`, you must **enable judges in the LaunchDarkly UI first** before running the notebook.

### Phase 6: Advanced Topics

| Order | Skill | Notebook | Purpose | Dependencies |
|-------|-------|----------|---------|--------------|
| 13 | [aiconfig-context-advanced](./aiconfig-context-advanced/SKILL.md) | [cookbook_aiconfig_context_advanced.ipynb](./aiconfig-context-advanced/verification/cookbook_aiconfig_context_advanced.ipynb) | Advanced multi-context patterns | Context Basic |
| 14 | [aiconfig-api](./aiconfig-api/SKILL.md) | [cookbook_aiconfig_api.ipynb](./aiconfig-api/verification/cookbook_aiconfig_api.ipynb) | API access patterns and authentication | Configs (to list) |

**Why last?** These build on all previous concepts.

## Quick Start Checklist

1. [ ] Set `LAUNCHDARKLY_API_TOKEN` environment variable
2. [ ] Run `aiconfig-projects` notebook to create project and get SDK key
3. [ ] The notebook will save `LAUNCHDARKLY_SDK_KEY` to your main .env file
4. [ ] Run `aiconfig-tools` to create any tools you need
5. [ ] Run `aiconfig-create` to create your first AI Config
6. [ ] Run `aiconfig-variations` to manage variations
7. [ ] Run `aiconfig-context-basic` to learn context patterns
8. [ ] Run `aiconfig-sdk` to test SDK consumption of your configs
9. [ ] Continue with other skills as needed

## Environment Variables Summary

| Variable | Source | Used By |
|----------|--------|---------|
| `LAUNCHDARKLY_API_TOKEN` | LaunchDarkly UI (Authorization settings) | All API-based skills |
| `LAUNCHDARKLY_SDK_KEY` | `aiconfig-projects` skill output | All SDK-based skills |
| `OPENAI_API_KEY` | OpenAI | AI Metrics, Online Evals |

## Skill Categories

### API-Based Skills (require `LAUNCHDARKLY_API_TOKEN`)
- aiconfig-projects
- aiconfig-api
- aiconfig-tools
- aiconfig-create
- aiconfig-variations
- aiconfig-update
- aiconfig-segments
- aiconfig-targeting
- aiconfig-ai-metrics
- aiconfig-custom-metrics

### SDK-Based Skills (require `LAUNCHDARKLY_SDK_KEY`)
- aiconfig-sdk
- aiconfig-context-basic
- aiconfig-context-advanced
- aiconfig-ai-metrics
- aiconfig-custom-metrics
- aiconfig-online-evals

## Notes

- **Agent Mode vs Completion Mode**: Online evaluations (judges) only work with completion-mode configs, not agent-mode configs.
- **Tools are Optional**: You don't need to create tools if your AI Config doesn't use function calling.
- **SDK Key Field**: The SDK key is extracted from the environment's `apiKey` field in the API response.
- **Enable Judges**: Before testing `aiconfig-online-evals`, enable judges in the LaunchDarkly UI.

## Future Skills

The following skills need to be created or completed:

| Skill | Status | Description |
|-------|--------|-------------|
| `aiconfig-frameworks` | DRAFT | LangGraph, CrewAI, Swarm, AutoGen integrations |
| `aiconfig-chat` | TODO | Interactive chat sessions (`create_chat()`, `chat.invoke()`) |
| `aiconfig-judges` | TODO | LLM judges for evaluation (`judge_config()`, `create_judge()`) |
| `aiconfig-feedback` | TODO | User feedback tracking (`track_feedback()`, `FeedbackKind`) |
| `aiconfig-bulk` | TODO | Bulk agent config fetch (`agent_configs()`) |

### Methods to Add to `aiconfig-ai-metrics`

| Method | Purpose |
|--------|---------|
| `track_metrics_of(fn, extractor)` | Generic async metrics tracking for any provider |
| `track_eval_scores(scores)` | Track evaluation scores |
| `track_judge_response(response)` | Track judge response with config key |
| `get_summary()` | Get current metrics summary |
