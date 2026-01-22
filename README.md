# Task 1 – AI NLP to SQL Backend (EdTech)

## Overview
This project implements an AI-powered backend that converts natural language questions into SQL queries and returns answers from an EdTech database.

## Tech Stack
- Python
- FastAPI
- SQLite
- Jupyter Notebook

## How to Run
1. Open the notebook `Task1_NLP_to_SQL_EdTech.ipynb`
2. Run all cells
3. Open http://127.0.0.1:8000/docs

## API Endpoints
POST /query
GET /stats

## NLP to SQL Approach
A rule-based NLP-to-SQL approach is used with schema awareness and SQL safety validation.

## Limitations
- Only SELECT queries supported
- Limited natural language patterns
