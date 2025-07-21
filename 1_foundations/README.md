# Agents

## What is an agent?
AI Agents are programs where LLM outputs control the workflow - HuggingFace.

One output from LLM is able to decide what tasks are carried out in what sequence.

In general, AI solution or agentic AI involves any or all of these 5 hallmarks:
1. Multiple LLM calls.
2. LLM with the ability to use tools.
3. An environment where LLMs interact (send messages, coordination orchestration).
4. A planner to coordinate activities.
5. Autonomy (giving some ability to an LLM to control what order things happen; giving LLM the opportunity to decide how to carry out future actions).

## Agentic systems (two sub-fields of agentic AI)
*Anthropic* distinguishes two types of agentic systems:
1. *Workflows* are systems where LLMs and tools orchestrated through predefined code paths.
2. *Agents* are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks. 

## Five design patterns when budiling Agentic systems for workflow (Anthropic)
1. *Prompt chaining*: decompose into fixed sub-tasks. It has LLM carrying out some task and then potentially based on some code, then pass that to a second LLM and that output could move on to the third and so on. This is chaining a series of LLM calls, decomposing into a fixed set of subtask. This is good because we can take care to frame each LLM call very precisely to get the best, and the most effective LLM response based on that prompt while keeping the whole process and workflow on guardrails by taking it step by step through a sequence of well defined tasks. (Yellow boxes are calls to LLM and blue boxes is where some code/software is written).
![prompt_chaining](images/prompt_chaining.png)
2. *Routing*: direct an input into a specialized sub-task, ensuring separation of concerns. Inputs come in and an LLM has the task of deciding which of multiple possible models are selected to carry out this function. The idea is to have specialist models here (LLM1, LLM2, LLM3) and they are good at carrying out specific task, the LLM router's job is to classify the task, understand which of the specialists will be best equipped to tackle the task. This allows for separation of concerns for being able to have different LLMs that have different levels of expertise and have a LLM to route to these experts.
![routing](images/routing.png)
3 *Parallelization*: breaking down tasks and running multiple subtasks concurrently. The idea is to have some code that takes a task and break it down into multiple pieces that should all run in _parallel_, where the tasks are sent to three LLMs to carry out three different activities concurrently. The aggregator (code) then takes the answers and stitches them together. (The tasks dont have to be different, it could be the same task but carried out three times.)
![parallelization](images/parallelization.png)
4. *Orchestrator-worker*: complex tasks are broken down dynamically and combined. It is no longer code that is doing the orchestration, rather, it is an LLM. The idea is that we are using a model to break down a complex task into smaller steps and then using a LLM to combine the result, hence making it much more dynamic because the orchestrator (LLM) can choose how to divide up the task. This design pattern might be hard to be considered as a (fixed) workflow because the orchestrator (LLM) has autonomy to how to divide the tasks and choose how many different LLMs get assigned the activities.
![orchestrator_worker](images/orchestrator_worker.png)
5. *Evaluation-optimizer*: LLM output is validated by another. The first LLM Generator doing its job to generate a solution, and a second LLM Evaluator evaluates the work of the first LLM. The LLM Evaluator does not generate content, but instead, it checks the work of a prior LLM and then accept or reject (with reason).
![evaluation_optimizer](images/evaluation_optimizer.png)

_A key concern to building any production agentic systems with LLM is about accuracy, predictability, robustness of the response and having validation agents to increase accuracy and build more guarantees._

## Understand agents