# EXP-2026-05-14 Pattern Implementation

## Project

Millionaire Quiz

## Selected Feature

50/50 Lifeline

## Selected Design Pattern

Strategy Pattern

## Goal of Experiment

The goal of this experiment was to check whether an AI assistant can implement the selected feature using a classical design pattern.

The selected feature was the 50/50 lifeline from the Millionaire Quiz project.

The selected pattern was the Strategy Pattern, because the quiz can have multiple lifeline types in the future.

## Prompt Provided to AI

I am working on a Python Tkinter + SQLite project called Millionaire Quiz.

The selected feature is the 50/50 lifeline.

Previously, this feature was described using BDD requirements and a Mermaid diagram.

Now I need to implement this feature as a clean module using the Strategy Pattern.

Requirements:

- Create a dedicated lifelines module.
- Use the Strategy Pattern.
- Create a base strategy class for lifelines.
- Create a FiftyFiftyStrategy class.
- Create a LifelineContext class.
- The 50/50 lifeline should keep the correct answer and one wrong answer.
- Two wrong answers should be removed.
- The correct answer must never be removed.
- The function should not directly update GUI or database.
- The result should be returned as data.
- The code should be clean, modular, and easy to extend.

Use Python.

## AI Output Summary

The AI generated a module with the following structure:

```text
lifelines
├── __init__.py
├── strategies.py
└── README.md
```

The main code was placed in `strategies.py`.

The module included:

- `LifelineStrategy`
- `FiftyFiftyStrategy`
- `LifelineContext`

## Example Code Result

```python
from abc import ABC, abstractmethod


class LifelineStrategy(ABC):
    @abstractmethod
    def apply(self, options, correct_answer, lifeline_available):
        pass


class FiftyFiftyStrategy(LifelineStrategy):
    def apply(self, options, correct_answer, lifeline_available):
        if not lifeline_available:
            return {
                "visible_options": options,
                "lifeline_available": False,
                "message": "50/50 lifeline has already been used."
            }

        if correct_answer not in options or len(options) != 4:
            return {
                "visible_options": options,
                "lifeline_available": lifeline_available,
                "message": "Invalid question data."
            }

        wrong_answers = [option for option in options if option != correct_answer]

        if len(wrong_answers) < 3:
            return {
                "visible_options": options,
                "lifeline_available": lifeline_available,
                "message": "Invalid answer options."
            }

        visible_options = [correct_answer, wrong_answers[0]]

        return {
            "visible_options": visible_options,
            "lifeline_available": False,
            "message": "50/50 lifeline used successfully."
        }


class LifelineContext:
    def __init__(self, strategy):
        self.strategy = strategy

    def use_lifeline(self, options, correct_answer, lifeline_available):
        return self.strategy.apply(options, correct_answer, lifeline_available)
```

## Evaluation

The AI applied the Strategy Pattern correctly.

The generated code has a base strategy class, a concrete strategy class, and a context class.

This makes the module easier to extend because new lifelines can be added as new strategy classes without changing the main quiz logic.

## Did the Pattern Help?

Yes, the Strategy Pattern helped clarify the code structure.

Instead of placing all lifeline logic inside the main quiz file, the logic was separated into its own module.

This makes the business logic easier to test, maintain, and reuse.

## Was There Any Overengineering?

For only one lifeline, the Strategy Pattern may look slightly more complex than a simple function.

However, for the Millionaire Quiz project, this is acceptable because more lifelines are planned in the roadmap.

For example:

- Second Chance
- Ask the Audience
- Phone a Friend

Because of this, the Strategy Pattern is a good architectural decision.

## Conclusion

This experiment showed that a design pattern can help guide AI code generation.

The Strategy Pattern gave the AI a clear structure and reduced the risk of creating messy code.

The result is a modular lifelines system that can be connected to the Tkinter interface later and extended with more lifeline types.
