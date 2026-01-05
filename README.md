# airflow

# Introduction to Apache Airflow

Apache Airflow is an **open-source workflow orchestration tool** used to **schedule, monitor, and manage data pipelines**.

Airflow is widely used in data engineering to orchestrate:

* ETL / ELT pipelines
* Data warehouse loads
* Machine learning workflows
* Batch data processing jobs

Airflow workflows are defined as **code (Python)**, which makes them version-controlled, testable, and reusable.

---

# 1.1 Core Concepts

---

## 1.1.1 DAG Definition

A **DAG (Directed Acyclic Graph)** represents a workflow in Airflow.

### Key Points

* Directed → Tasks have direction (order)
* Acyclic → No circular dependencies
* Graph → Tasks are connected by dependencies

A DAG:

* Defines **what tasks run**
* Defines **execution order**
* Does NOT execute tasks itself

---

## 1.1.2 Operators

Operators define **what kind of work** a task performs.

### Common Operator Types

* **BashOperator** – Runs shell commands
* **PythonOperator** – Executes Python functions
* **DummyOperator** – Placeholder task
* **EmailOperator** – Sends emails
* **BranchPythonOperator** – Conditional branching

---

## 1.1.3 Tasks

A **task** is a single unit of work in Airflow.

* A task is an **instance of an operator**
* Each task has a unique `task_id`
* Tasks are executed independently

### Task Lifecycle

```
Scheduled → Queued → Running → Success / Failed
```

---

## 1.1.4 DAG-to-DAG Trigger

Airflow allows one DAG to **trigger another DAG**.

### Why use DAG-to-DAG triggering?

* Modular pipelines
* Reusable workflows
* Master-child DAG design

---

# 1.2 Scheduler

The **Scheduler** is the heart of Apache Airflow.

### What the Scheduler Does

* Monitors DAGs
* Determines when tasks should run
* Submits tasks to the executor

### Scheduler Responsibilities

* Reads DAG definitions
* Creates DAG runs based on schedule
* Checks task dependencies
* Queues tasks for execution

### High-Level Flow

```
DAG → Scheduler → Executor → Worker → Task Execution
```

### Important Notes

* Scheduler does NOT execute tasks directly
* Execution is handled by Executors (Local, Celery, Kubernetes)

---

## Summary Table

| Concept     | Description            |
| ----------- | ---------------------- |
| DAG         | Workflow definition    |
| Operator    | Type of work           |
| Task        | Instance of operator   |
| DAG Trigger | Trigger another DAG    |
| Scheduler   | Orchestrates execution |

---

## Why Airflow Is Important

* Scalable workflow orchestration
* Python-based pipelines
* Strong scheduling & monitoring
* Industry standard for data engineering

---

