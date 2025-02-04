---
id: how-to-set-activityoptions-in-go
title: How to set ActivityOptions in Go
sidebar_label: ActivityOptions
description: Create an instance of `ActivityOptions` from the `go.temporal.io/sdk/workflow` package and use `WithActivityOptions()` to apply it to the instance of `workflow.Context`.
tags:
  - developer-guide
  - go
---

import {RelatedReadContainer, RelatedReadItem} from '../components/RelatedReadList.js'

<!-- prettier-ignore -->
import * as WhatIsAnActivityId from '../content/what-is-an-activity-id.md'
import * as WhatIsATaskQueue from '../content/what-is-a-task-queue.md'
import * as WhatIsAScheduleToCloseTimeout from '../content/what-is-a-schedule-to-close-timeout.md'
import * as WhatIsAScheduleToStartTimeout from '../content/what-is-a-schedule-to-start-timeout.md'
import * as WhatIsAStartToCloseTimeout from '../content/what-is-a-start-to-close-timeout.md'
import * as WhatIsAHeartbeatTimeout from '../content/what-is-a-heartbeat-timeout.md'
import * as WhatIsARetryPolicy from '../content/what-is-a-retry-policy.md'

Create an instance of [`ActivityOptions`](https://pkg.go.dev/go.temporal.io/sdk/workflow#ActivityOptions) from the `go.temporal.io/sdk/workflow` package and use [`WithActivityOptions()`](https://pkg.go.dev/go.temporal.io/sdk/workflow#WithActivityOptions) to apply it to the instance of `workflow.Context`.

The instance of `workflow.Context` is then passed to the `ExecuteActivity()` call.

| Field                                               | Required                          | Type                                                                        |
| --------------------------------------------------- | --------------------------------- | --------------------------------------------------------------------------- |
| [`ActivityID`](#activityid)                         | No                                | `string`                                                                    |
| [`TaskQueueName`](#taskqueuename)                   | No                                | `string`                                                                    |
| [`ScheduleToCloseTimeout`](#scheduletoclosetimeout) | Yes (or `StartToCloseTimeout`)    | `time.Duration`                                                             |
| [`ScheduleToStartTimeout`](#scheduletostarttimeout) | No                                | `time.Duration`                                                             |
| [`StartToCloseTimeout`](#scheduletoclosetimeout)    | Yes (or `ScheduleToCloseTimeout`) | `time.Duration`                                                             |
| [`HeartbeatTimeout`](#heartbeattimeout)             | No                                | `time.Duration`                                                             |
| [`WaitForCancellation`](#waitforcancellation)       | No                                | `bool`                                                                      |
| [`OriginalTaskQueueName`](#originaltaskqueuename)   | No                                | `string`                                                                    |
| [`RetryPolicy`](#retrypolicy)                       | No                                | [`RetryPolicy`](https://pkg.go.dev/go.temporal.io/sdk/temporal#RetryPolicy) |

### `ActivityID`

- Type: `string`
- Default: None

```go
activityoptions := workflow.ActivityOptions{
  ActivityID: "your-activity-id",
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsAnActivityId} />
</RelatedReadContainer>

### `TaskQueueName`

- Type: `string`
- Default: Inherits the TaskQueue name from the Workflow.

```go
activityoptions := workflow.ActivityOptions{
  TaskQueueName: "your-task-queue-name",
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsATaskQueue} />
</RelatedReadContainer>

### `ScheduleToCloseTimeout`

This or `ScheduleToStart` must be set.

- Type: `time.Duration`
- Default: ∞ (infinity - no limit)

```go
activityoptions := workflow.ActivityOptions{
  ScheduleToCloseTimeout: 10 * time.Second,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsAScheduleToCloseTimeout} />
</RelatedReadContainer>

### `ScheduleToStartTimeout`

This or `ScheduleToClose` must be set.

- Type: `time.Duration`
- Default: ∞ (infinity - no limit)

```go
activityoptions := workflow.ActivityOptions{
  ScheduleToStartTimeout: 10 * time.Second,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsAScheduleToStartTimeout} />
</RelatedReadContainer>

### `StartToCloseTimeout`

- Type: `time.Duration`
- Default: Same as the `ScheduleToCloseTimeout`

```go
activityoptions := workflow.ActivityOptions{
  StartToCloseTimeout: 10 * time.Second,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsAStartToCloseTimeout} />
</RelatedReadContainer>

### `HeartbeatTimeout`

```go
activityoptions := workflow.ActivityOptions{
  HeartbeatTimeout: 10 * time.Second,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsAHeartbeatTimeout} />
</RelatedReadContainer>

### `WaitForCancellation`

If `true` the Activity Execution will finish executing should there be a Cancellation request.

- Type: `bool`
- Default: `false`

```go
activityoptions := workflow.ActivityOptions{
  WaitForCancellation: false,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

### `OriginalTaskQueueName`

```go
activityoptions := workflow.ActivityOptions{
  OriginalTaskQueueName: "your-original-task-queue-name",
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

### `RetryPolicy`

- Type: [`RetryPolicy`](https://pkg.go.dev/go.temporal.io/sdk/temporal#RetryPolicy)
- Default:

```go
retrypolicy := &temporal.RetryPolicy{
  InitialInterval:    time.Second,
  BackoffCoefficient: 2.0,
  MaximumInterval:    time.Second * 100, // 100 * InitialInterval
  MaximumAttempts: 0, // Unlimited
  NonRetryableErrorTypes: []string, // empty
}
```

Providing a Retry Policy here is a customization, and overwrites individual Field defaults.

```go
retrypolicy := &temporal.RetryPolicy{
  InitialInterval:    time.Second,
  BackoffCoefficient: 2.0,
  MaximumInterval:    time.Second * 100,
}

activityoptions := workflow.ActivityOptions{
  RetryPolicy: retrypolicy,
}
ctx = workflow.WithActivityOptions(ctx, activityoptions)
var yourActivityResult YourActivityResult
err = workflow.ExecuteActivity(ctx, YourActivityDefinition, yourActivityParam).Get(ctx, &yourActivityResult)
if err != nil {
  // ...
}
```

<RelatedReadContainer>
  <RelatedReadItem page={WhatIsARetryPolicy} />
</RelatedReadContainer>
