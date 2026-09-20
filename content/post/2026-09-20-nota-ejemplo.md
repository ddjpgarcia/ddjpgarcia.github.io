---
layout: post
title: "Nota técnica de ejemplo"
subtitle: "Apuntes cortos sobre una herramienta o técnica"
description: "Ejemplo de una nota técnica con código."
date: 2026-09-19
author: "Dan"
tags:
  - ejemplo
  - sql
categories:
  - Notas
---

Las notas sirven para documentar algo aprendido, con código reproducible.

<!--more-->

```sql
SELECT fecha, COUNT(*) AS registros
FROM eventos
GROUP BY fecha
ORDER BY fecha;
```
