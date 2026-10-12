---
{"dg-publish":true,"permalink":"/paralleism-types/","created":"2026-10-01T15:11:53.069+01:00","updated":"2026-10-11T21:02:48.958+01:00","dg-note-properties":{}}
---

#hpc 

There are three main ways to break a problem up for parallel execution:

1. **Data Parallelism📦️:** The _same_ operation is applied to _different_ pieces of data simultaneously. (Example: Adding two large vectors element-by-element, or applying a filter to every pixel in an image).
    
2. **Task Parallelism⚙️:** _Different_ tasks are executed concurrently. These tasks are often independent or loosely coupled. (Example: One thread handles network I/O while another handles UI rendering; Producer-Consumer).
    
3. **Pipeline Parallelism:** A task is broken into sequential stages, and data flows through them like an assembly line. Each stage runs on a different processor. (Example: CPU instruction pipelines; a data processing pipeline where Stage 1 parses, Stage 2 filters, and Stage 3 saves).
    

- _Note: Hybrid Approaches combine these (e.g., MPI + OpenMP)._


***
Next :  [[Concurrent vs Parallel Execution\|Concurrent vs Parallel Execution]]