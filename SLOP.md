# Parallel API Operations

Parallel API

Version: 0.1.2

## Overview

This API contains 11 operations grouped into 3 categories.

## Search API

[View Search API operations](tags/Search API.yaml)

### web_search_alpha_search_post

**POST /alpha/search**

Execute web search with AI-native results

Searches the web using natural language objectives and returns ranked URLs with extended webpage excerpts. Built on Parallel's custom web crawler and index, this API takes flexible inputs (search objective and/or search queries) and returns LLM-ready ranked URLs with extended webpage excerpts. The Search API is optimized for AI agents and RAG systems requiring high-quality, relevant web content.

[View operation details](operations/web_search_alpha_search_post.yaml)

---

## Task API v1

[View Task API v1 operations](tags/Task API v1.yaml)

### tasks_runs_post_v1_tasks_runs_post

**POST /v1/tasks/runs**

Create a new task run for structured web research

Initiates a task run that transforms natural language queries into precise, schema-compliant web outputs. The task run is created immediately in 'queued' status and begins processing asynchronously. You can specify input data (string or JSON), select a processor (lite, base, core, pro, ultra), and define structured output schemas. Beta features like Source Policy, MCP servers, and webhooks can be enabled by setting the 'parallel-beta' header with appropriate values.

[View operation details](operations/tasks_runs_post_v1_tasks_runs_post.yaml)

---

### tasks_runs_get_v1_tasks_runs__run_id__get

**GET /v1/tasks/runs/{run_id}**

Retrieve current status of a task run

Retrieves the current status and metadata for a specific task run by its run_id. This endpoint returns the task run object with current status (queued, running, completed, failed, etc.), processor information, timestamps, and any warnings or errors. The actual task results are available through the separate `/result` endpoint once the task is completed.

[View operation details](operations/tasks_runs_get_v1_tasks_runs__run_id__get.yaml)

---

### tasks_runs_input_get_v1_tasks_runs__run_id__input_get

**GET /v1/tasks/runs/{run_id}/input**

Retrieve the original input data for a task run

Retrieves the complete input data that was submitted when creating the specified task run. This includes the task specification (input/output schemas), the actual input data (text or JSON), processor selection, and any metadata that was provided. This endpoint is useful for debugging, auditing, or reconstructing the context of a completed task run.

[View operation details](operations/tasks_runs_input_get_v1_tasks_runs__run_id__input_get.yaml)

---

### tasks_runs_result_get_v1_tasks_runs__run_id__result_get

**GET /v1/tasks/runs/{run_id}/result**

Retrieve task run results with citations and reasoning

Retrieves the complete results of a task run, blocking until the task is completed if it's still in progress. The response includes both the structured output that conforms to your specified schema and the comprehensive "basis" - citations, reasoning, excerpts, and confidence levels that support each output field. This endpoint automatically handles polling and will wait up to the specified timeout (default 600 seconds) for task completion.

[View operation details](operations/tasks_runs_result_get_v1_tasks_runs__run_id__result_get.yaml)

---

## Task API (Beta)

[View Task API (Beta) operations](tags/Task API (Beta).yaml)

### tasks_taskgroups_post_v1beta_tasks_groups_post

**POST /v1beta/tasks/groups**

Create a task group for batch processing

Creates a new TaskGroup container to organize and track multiple task runs collectively. Task Groups enable efficient batch processing of hundreds or thousands of tasks with unified monitoring, intelligent failure handling, and real-time results streaming. This is ideal for large-scale operations like bulk CRM enrichment, due diligence workflows, or competitive intelligence gathering where you need to process many similar tasks and monitor their progress as a group.

[View operation details](operations/tasks_taskgroups_post_v1beta_tasks_groups_post.yaml)

---

### tasks_taskgroups_get_v1beta_tasks_groups__taskgroup_id__get

**GET /v1beta/tasks/groups/{taskgroup_id}**

Get aggregated status across all runs in a task group

Retrieves the current aggregated status and progress information for all task runs within the specified TaskGroup. This includes the total number of task runs, counts of runs by status (queued, running, completed, failed, etc.), whether the group is still active, and a human-readable status message. This endpoint provides a high-level overview of your batch processing progress without needing to check individual task runs.

[View operation details](operations/tasks_taskgroups_get_v1beta_tasks_groups__taskgroup_id__get.yaml)

---

### tasks_taskgroups_runs_get_v1beta_tasks_groups__taskgroup_id__runs_get

**GET /v1beta/tasks/groups/{taskgroup_id}/runs**

Stream task runs and their results from a task group

Streams task runs from a TaskGroup in real-time, optionally including their inputs and outputs as they become available. Task runs are returned in the order they were added to the group, with completed tasks including their full results and incomplete tasks showing current status. This server-sent events endpoint enables real-time monitoring and result collection for batch processing workflows. You can filter by status and control whether to include input data and output results.

[View operation details](operations/tasks_taskgroups_runs_get_v1beta_tasks_groups__taskgroup_id__runs_get.yaml)

---

### tasks_taskgroups_runs_post_v1beta_tasks_groups__taskgroup_id__runs_post

**POST /v1beta/tasks/groups/{taskgroup_id}/runs**

Add multiple task runs to an existing task group

Adds multiple new task runs to an existing TaskGroup for batch processing. You can specify a default task specification that applies to all runs, then provide individual inputs and processor selections for each task. This allows you to efficiently queue hundreds or thousands of similar tasks while maintaining the ability to customize inputs and processors per task. The runs are added immediately and begin processing asynchronously.

[View operation details](operations/tasks_taskgroups_runs_post_v1beta_tasks_groups__taskgroup_id__runs_post.yaml)

---

### tasks_sessions_events_get_v1beta_tasks_groups__taskgroup_id__events_get

**GET /v1beta/tasks/groups/{taskgroup_id}/events**

Stream real-time events from a task group

Streams real-time events from a TaskGroup including status updates and run completions via server-sent events. This endpoint provides live updates about group-level status changes and individual task run completions, enabling real-time monitoring of batch processing operations. The connection remains open for up to 10 minutes as long as at least one run in the TaskGroup is active, and supports resumable streaming using event IDs for reliable event delivery.

[View operation details](operations/tasks_sessions_events_get_v1beta_tasks_groups__taskgroup_id__events_get.yaml)

---

### tasks_taskgroups_runs_id_get_v1beta_tasks_groups__taskgroup_id__runs__run_id__get

**GET /v1beta/tasks/groups/{taskgroup_id}/runs/{run_id}**

Retrieve status of a specific run within a task group

Retrieves the current status and metadata for a specific task run within a TaskGroup by its run_id. This endpoint provides the same information as the standard task run status endpoint but is scoped within the context of a task group. The actual task results are available through the separate result endpoints once the task is completed. This is useful for checking the status of individual tasks within a batch processing operation.

[View operation details](operations/tasks_taskgroups_runs_id_get_v1beta_tasks_groups__taskgroup_id__runs__run_id__get.yaml)

---

