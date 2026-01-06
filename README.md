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

# 1.3 Executor

An **Executor** defines **how and where tasks are executed** in Apache Airflow.

The executor works with the **Scheduler** to run tasks on workers.

---

## Role of Executor

* Receives tasks from Scheduler
* Sends tasks to workers
* Manages task execution

### High-Level Flow

```
DAG → Scheduler → Executor → Worker → Task
```

---

## Common Executor Types

### 🔹 Sequential Executor

* Runs one task at a time
* Used for testing only

### 🔹 Local Executor

* Runs tasks in parallel on a single machine
* Used for small to medium workloads

### 🔹 Celery Executor

* Distributed execution
* Uses message broker (Redis/RabbitMQ)
* Suitable for large-scale pipelines

### 🔹 Kubernetes Executor

* Runs each task in a Kubernetes pod
* Highly scalable and cloud-native

---

## When to Use Which Executor

| Executor   | Best For               |
| ---------- | ---------------------- |
| Sequential | Learning & testing     |
| Local      | Small teams            |
| Celery     | Enterprise workloads   |
| Kubernetes | Cloud-native pipelines |

---

# 1.4 Operators

Operators define **what action a task performs**.

Each task in a DAG is created from an operator.

---

## 1.4.1 BashOperator

Executes shell commands.

### Use Cases

* Run shell scripts
* Call Linux commands


---

## 1.4.2 PythonOperator

Executes a Python function.

### Use Cases

* Data processing
* API calls
* Custom logic

---

## 1.4.3 Sensor

Sensors **wait for a condition to be met**.

### Common Sensors

* FileSensor
* ExternalTaskSensor
* TimeSensor

### Use Cases

* Wait for file arrival
* Wait for upstream DAG completion

---

## 1.4.4 SubDagOperator

Used to create **nested DAGs** inside a parent DAG.

⚠️ *Not recommended for new designs* (performance issues).

### Use Cases

* Legacy workflows
* Grouping tasks (now replaced by Task Groups)

---

## 1.4.5 TriggerDagRunOperator

Triggers another DAG from the current DAG.

### Use Cases

* Modular pipelines
* Master-child DAG pattern


---

## Summary Table

| Component             | Purpose              |
| --------------------- | -------------------- |
| Executor              | Executes tasks       |
| BashOperator          | Run shell commands   |
| PythonOperator        | Run Python functions |
| Sensor                | Wait for conditions  |
| SubDagOperator        | Nested DAGs          |
| TriggerDagRunOperator | Trigger another DAG  |

---




