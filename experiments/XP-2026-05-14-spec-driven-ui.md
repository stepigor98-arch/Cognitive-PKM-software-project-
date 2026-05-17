# EXP-2026-05-14 Spec Driven UI

## Project

Millionaire Quiz

## Feature

50/50 Lifeline

## Goal

The goal was to create a small UI for the 50/50 lifeline and connect it with the backend module from previous task.

## Design Contract

I created `docs/DESIGN.md`.

It includes:

- framework choice
- colors
- typography rules
- spacing rules
- component rules
- backend connection rule

## Framework

I used Streamlit because the project is in Python and it is simple to connect with Python backend code.

## Prompt Used

I asked AI to generate a Streamlit UI using my DESIGN.md file.

The UI needed to:

- show one quiz question
- show four answer options
- have a 50/50 button
- call the existing backend module
- show the result message
- not duplicate backend logic

## Result

AI generated a simple Streamlit file:

```text
MillionaireQuiz_Folder/ui/lifeline_demo.py
