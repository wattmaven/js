# Conventions

## TypeScript Testing

This project uses the [vitest](https://vitest.dev/guide/) testing framework.

```typescript
// sum.test.ts
import {describe, expect, test} from 'vitest'
import {sum} from './sum'

describe('sum', () => {
    test('adds 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3)
    })
})
```

Furthermore, we usually also split tests into different groups based on the type of test.

Some common groups are:

- Unit tests (`**/*.unit.test.ts`)
- Integration tests (`**/*.integration.test.ts`)
- End-to-end tests (`**/*.e2e.test.ts`)

```typescript
// vitest.workspace.ts

import {defineWorkspace} from "vitest/config";

export default defineWorkspace([
    {
        test: {
            name: "unit",
            include: ["**/*.unit.test.ts"],
            environment: "node",
        },
    },
    {
        test: {
            name: "integration",
            include: ["**/*.integration.test.ts"],
            environment: "node",
        },
    },
    {
        test: {
            name: "e2e",
            include: ["**/*.e2e.test.ts"],
            environment: "node",
        },
    },
]);
```

### Concurrent Testing

When defining tests, you should _probably_ use the `concurrent` function to run tests concurrently.

```typescript
// sum.test.ts
import {describe, expect, test} from 'vitest'
import {sum} from './sum'

describe.concurrent('sum', () => {
    test('adds 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3)
    })
})
```

Don't do this if you're testing something that requires a shared resource, like a database.
