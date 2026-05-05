# Source Sidechain Skill

This is a Markdown export of the original local Claude `/sidechain` skill used as source material for one-shot sidechain planning and execution governance.

```yaml
name: sidechain
version: "1.0.0"
description: Decompose complex tasks into JSON prompt chains with complexity-driven instruction depth (1-3 layers) and TDD-first subagent execution. Use when planning multi-component features, refactors, or any task requiring orchestrated implementation.
user-invocable: true
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Task
  - TodoWrite
```

# Sidechain - Task Decomposition & Orchestration

Decompose complex tasks into structured JSON prompt chains with complexity-driven instruction depth and TDD-first subagent execution.

## Usage

```text
/sidechain <task description>
```

## Process Overview

```text
/sidechain <task>
       |
       v
+------------------+
| Phase 1: Analyze | -> List components, hooks, queries, DB, UI
+--------+---------+
         |
         v
+------------------+
| Phase 2: Rate    | -> Assign complexity 1-3 to each item
+--------+---------+
         |
         v
+------------------+
| Phase 3: Chain   | -> Generate JSON prompt chain
+--------+---------+
         |
         v
+------------------+
| Phase 4: Execute | -> Dispatch subagents per subtask
+--------+---------+
         |
         v
+------------------+
| Phase 5: TDD     | -> Test-first for each subtask
+--------+---------+
```

---

## Phase 1: Task Analysis

Create analysis file at `opux/sidechain/[task-name]/analysis.md`:

```markdown
## Task Analysis: [Task Name]

### Components Needed
| Component | Type | New/Modify | Complexity |
|-----------|------|------------|------------|
| ComponentName | React Component | New | 2 |

### Hooks Needed
| Hook | Purpose | New/Modify | Complexity |
|------|---------|------------|------------|
| useHookName | Data fetching | New | 2 |

### Queries/Mutations
| Query/Mutation | Endpoint | Method | Complexity |
|----------------|----------|--------|------------|
| fetchData | /api/data | GET | 1 |

### Database Integrations
| Table | Operation | Migration? | Complexity |
|-------|-----------|------------|------------|
| tableName | SELECT/INSERT | Yes | 3 |

### UI Integrations
| Integration | Location | Type | Complexity |
|-------------|----------|------|------------|
| Dashboard widget | page.tsx | Add | 1 |

### Services/Business Logic
| Service | Purpose | New/Modify | Complexity |
|---------|---------|------------|------------|
| ServiceName | Business logic | New | 3 |
```

---

## Phase 2: Complexity Rating System

### Complexity 1 (Simple) - 1 Instruction Layer

- Single file change
- No external dependencies
- Straightforward logic
- Examples: Add a badge, create simple utility function, add field to form

**Instruction Structure:**

```json
{
  "instructions": {
    "layer1": "Goal + acceptance criteria"
  }
}
```

### Complexity 2 (Moderate) - 2 Instruction Layers

- 2-3 file changes
- Some coordination needed
- Moderate logic/state
- Examples: Add hook with query, create component with props, add API endpoint

**Instruction Structure:**

```json
{
  "instructions": {
    "layer1": "Goal + acceptance criteria",
    "layer2": "Implementation details + file locations + patterns to follow"
  }
}
```

### Complexity 3 (Complex) - 3 Instruction Layers

- 4+ file changes
- Multiple integrations
- Complex logic/state management
- Edge cases to handle
- Examples: New service with DB + API + UI, state machine, real-time feature

**Instruction Structure:**

```json
{
  "instructions": {
    "layer1": "Goal + acceptance criteria",
    "layer2": "Implementation approach + architecture decisions",
    "layer3": "Edge cases + error handling + performance considerations"
  }
}
```

---

## Phase 3: JSON Prompt Chain Generation

Create prompt chain at `opux/sidechain/[task-name]/prompt-chain.json`:

```json
{
  "$schema": "sidechain-prompt-chain-v1",
  "taskId": "TASK-001",
  "name": "Task Name",
  "description": "High-level task description",
  "complexity": 3,
  "tdd": true,
  "analysis": {
    "components": ["ComponentA", "ComponentB"],
    "hooks": ["useFeature"],
    "queries": ["GET /api/feature"],
    "database": ["feature_table"],
    "ui": ["Dashboard integration"]
  },
  "subtasks": [
    {
      "id": "A1",
      "name": "Create database schema",
      "complexity": 1,
      "agentType": "general-purpose",
      "instructions": {
        "layer1": "Add feature_table to schema with columns: id, name, created_at. Generate migration."
      },
      "tdd": {
        "testFirst": "Write test that verifies table exists and has correct columns",
        "testFile": "packages/database/src/__tests__/schema.test.ts",
        "testCommand": "cd timemachine-existing/packages/database && bun test",
        "implementation": "Add table to schema/index.ts, run db:generate"
      },
      "files": {
        "create": [],
        "modify": ["packages/database/src/schema/index.ts"]
      },
      "dependencies": [],
      "outputs": ["drizzle/XXXX_migration.sql"]
    },
    {
      "id": "A2",
      "name": "Create API endpoint",
      "complexity": 2,
      "agentType": "general-purpose",
      "instructions": {
        "layer1": "Create GET /api/feature endpoint that returns feature data",
        "layer2": "Use Hono router pattern from existing routes. Add Zod validation. Return { success: true, data: Feature[] }"
      },
      "tdd": {
        "testFirst": "Write API integration test that calls endpoint and verifies response shape",
        "testFile": "apps/api/src/routes/__tests__/feature.test.ts",
        "testCommand": "cd timemachine-existing/apps/api && bun test",
        "implementation": "Create route file, add to router index"
      },
      "files": {
        "create": ["apps/api/src/routes/feature.ts"],
        "modify": ["apps/api/src/routes/index.ts"]
      },
      "dependencies": ["A1"],
      "outputs": ["apps/api/src/routes/feature.ts"]
    },
    {
      "id": "A3",
      "name": "Create React hook and component",
      "complexity": 3,
      "agentType": "general-purpose",
      "instructions": {
        "layer1": "Create useFeature hook and FeatureCard component for dashboard",
        "layer2": "Hook uses React Query with queryKey ['feature']. Component displays feature data in card format matching existing dashboard style.",
        "layer3": "Handle loading state with Skeleton. Handle error state with error message. Handle empty state. Support real-time updates via WebSocket invalidation."
      },
      "tdd": {
        "testFirst": "Write component tests for all states: loading, error, empty, data. Write hook test for query behavior.",
        "testFile": "apps/web/src/components/__tests__/FeatureCard.test.tsx",
        "testCommand": "cd timemachine-existing/apps/web && bun run test",
        "implementation": "Create hook in hooks/, component in components/dashboard/"
      },
      "files": {
        "create": [
          "apps/web/src/hooks/useFeature.ts",
          "apps/web/src/components/dashboard/FeatureCard.tsx"
        ],
        "modify": ["apps/web/src/app/page.tsx"]
      },
      "dependencies": ["A2"],
      "outputs": ["FeatureCard.tsx", "useFeature.ts"]
    }
  ],
  "execution": {
    "order": ["A1", "A2", "A3"],
    "parallelizable": [],
    "checkpoints": [
      {
        "after": "A1",
        "verify": "Migration generated, types updated"
      },
      {
        "after": "A2",
        "verify": "API responds correctly, types match"
      },
      {
        "after": "A3",
        "verify": "Component renders, all states handled"
      }
    ]
  },
  "verification": {
    "finalTests": "cd timemachine-existing && bun run test",
    "typeCheck": "cd timemachine-existing && bun run lint",
    "acceptanceCriteria": [
      "Feature data displays on dashboard",
      "All tests pass",
      "No TypeScript errors"
    ]
  }
}
```

---

## Phase 4: Subagent Dispatch

### Agent Type Selection by Complexity

| Complexity | Primary Agent | Strategy |
|------------|---------------|----------|
| 1 | `general-purpose` | Single focused agent, minimal context |
| 2 | `general-purpose` | Test-first instruction, then implementation |
| 3 | `Plan` then `general-purpose` | Plan agent designs approach, implementation agent executes |

### Agent Type by Task Nature

| Task Type | Agent | Notes |
|-----------|-------|-------|
| Find files, understand code | `Explore` | Research phase |
| Design approach | `Plan` | Complex subtasks |
| Run tests, builds | `Bash` | Verification |
| Write code | `general-purpose` | Implementation |

### Dispatch Pattern

```typescript
// For each subtask in order:
for (const subtask of promptChain.subtasks) {
  // 1. TDD: Write test first
  await dispatchAgent({
    type: subtask.agentType,
    prompt: `
      SUBTASK: ${subtask.id} - ${subtask.name}
      COMPLEXITY: ${subtask.complexity}

      ## TDD PHASE 1: Write Test First
      ${subtask.tdd.testFirst}

      Test file: ${subtask.tdd.testFile}

      Write the failing test now.
    `
  });

  // 2. Run test (expect fail)
  await runBash(subtask.tdd.testCommand);

  // 3. Implement
  await dispatchAgent({
    type: subtask.agentType,
    prompt: `
      SUBTASK: ${subtask.id} - ${subtask.name}

      ## Instructions
      ${Object.values(subtask.instructions).join('\n\n')}

      ## TDD PHASE 2: Make Test Pass
      ${subtask.tdd.implementation}

      Implement now.
    `
  });

  // 4. Run test (expect pass)
  await runBash(subtask.tdd.testCommand);

  // 5. Checkpoint verification
  if (checkpoint = getCheckpoint(subtask.id)) {
    await verify(checkpoint);
  }
}
```

---

## Phase 5: TDD Enforcement

**Every subtask MUST follow Red-Green-Refactor:**

### Step 1: RED - Write Failing Test

```typescript
// Write test that defines expected behavior
describe('FeatureName', () => {
  it('should [expected behavior]', () => {
    // Arrange
    const input = { ... };

    // Act
    const result = featureFunction(input);

    // Assert
    expect(result).toEqual(expectedOutput);
  });
});
```

### Step 2: Run Test (Expect FAIL)

```bash
bun test path/to/feature.test.ts
# Expected: FAIL (feature not implemented yet)
```

### Step 3: GREEN - Minimal Implementation

```typescript
// Write just enough code to make test pass
export function featureFunction(input) {
  // Minimal implementation
  return expectedOutput;
}
```

### Step 4: Run Test (Expect PASS)

```bash
bun test path/to/feature.test.ts
# Expected: PASS
```

### Step 5: REFACTOR (if needed)

- Clean up code while keeping tests green
- Extract helpers, improve naming
- Run tests after each refactor

---

## Output Files

The sidechain skill generates these files in your project:

```text
opux/sidechain/[task-name]/
  analysis.md        # Component breakdown
  prompt-chain.json  # Execution chain
  progress.md        # Execution tracking
```

---

## Example: Live Liquidation Monitor

```text
/sidechain implement live liquidation monitor for stop-loss enforcement
```

Would generate:

**Analysis:**

- Components: `LivePositionMonitor` (complexity 2)
- Hooks: `usePositionHealth` (complexity 2)
- Services: `LiveLiquidationMonitor` (complexity 3)
- Database: None (uses existing positions table)
- UI: Dashboard health indicator (complexity 1)

**Prompt Chain:**

```json
{
  "subtasks": [
    {
      "id": "A1",
      "name": "Create LiveLiquidationMonitor service",
      "complexity": 3,
      "instructions": {
        "layer1": "Create service that monitors live positions against stop-loss prices",
        "layer2": "Subscribe to price.update events. For each position with stopLossPrice, check if current price breaches threshold. Use PositionService for close operations.",
        "layer3": "Handle WebSocket reconnection. Debounce rapid price updates. Log all stop-loss triggers. Emit alerts on execution. Handle partial fills."
      }
    }
  ]
}
```

---

## Rules

1. **Never skip TDD** - Every subtask writes tests first
2. **Respect complexity depth** - Match instruction layers to complexity rating
3. **Parallelize when possible** - Run independent subtasks concurrently
4. **Atomic subtasks** - Each should be independently verifiable
5. **Clear dependencies** - Explicit ordering for dependent tasks
6. **Update progress** - Mark subtasks complete in progress.md as you go
