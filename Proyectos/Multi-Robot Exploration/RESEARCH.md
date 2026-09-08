# Research

## Working Project Statement
I am developing a multi-robot autonomous exploration system in which ground robots collaboratively explore unknown environments, share partial information, and make autonomous decisions about where to explore next. The project investigates whether learning-based coordination can improve exploration efficiency and robustness under realistic constraints such as limited communication, battery resources, partial observability, and robot failures.*

## Core Question
How can a group of autonomous robots collaboratively explore an unknown environment and decide what to do next using incomplete information?

⚠️ This question is not yet fully specified. The exact contribution must be found through literature review.

## Candidate Directions

### Direction A: Autonomous decision-making
Can individual robots learn what to do without explicit programming?
- explore, stop, change zone, investigate anomaly, return, help another robot

### Direction B: Coordination under constraints
Can robots learn how to work together under realistic limits?
- distribute zones, avoid redundancy, adapt when one fails
- battery constraints, communication limits

### Direction C: Perception + collective decision-making
Can robots use perception to build collective understanding and decide as a system?

**Current hypothesis:** Direction B or C, or something in between is where the most meaningful contribution lies.

## Research Philosophy
- Problem
- Research Question
- Hypothesis
- System
- Experiment
- Results
- Iteration

NOT: Technology → find a reason to use it.

## Key Concepts

**Active exploration**
Robots ask: "Where would obtaining more information be most valuable?"
Prioritize areas where uncertainty is high or information gain is high.

**Robot failure as research variable**
Failure is a feature, not a bug. The system should detect and adapt.
Questions: Can robots redistribute? How much performance is lost? Does decentralized coordination improve resilience?

**Communication constraints**
Not assuming perfect communication.
Question: How much communication does the system actually need?

## Evaluation Metrics (tentative)
- % environment explored
- Exploration time
- Coverage rate
- Distance traveled / energy consumed
- Redundant exploration
- Map accuracy
- Task allocation efficiency
- Performance after robot failures
- Performance under communication loss
- Generalization to unseen environments

## Baselines to Compare Against
- Random exploration
- Greedy exploration
- Frontier-based exploration
- Classical task allocation
- Auction-based coordination
- Centralized planning
- Decentralized heuristics
