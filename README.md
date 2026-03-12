# Dine or Dash: ¿Dónde comemos?

> Sistema de recomendación de restaurantes basado en reseñas de Yelp — Philadelphia.

**Sistemas de Recomendación — Especialización en Ciencia de Datos e IA (UTEC – MIT)**  
Martina Ibarra · Elena Salomón · Florencia Nebot · 2026

---

## Descripción

Sistema de recomendación personalizado de restaurantes construido sobre reseñas de Yelp para Philadelphia. Cinco modelos progresivos — desde ranking simple hasta filtrado colaborativo enriquecido con análisis de sentimiento y red social de amigos.

El proyecto parte de la paradoja de la elección: demasiadas opciones paralizan al usuario. La solución incorpora no solo patrones de comportamiento individual sino también la influencia de la red social, replicando el comportamiento natural de las recomendaciones entre conocidos.

---

## Dataset

- **Fuente:** [Yelp Open Dataset](https://www.yelp.com/dataset)
- **Subconjunto:** Restaurantes de Philadelphia
- **Reseñas:** 111.831 ratings reales
- **Usuarios únicos:** 8.714
- **Restaurantes únicos:** 3.372
- **Densidad de la matriz:** < 0.4% (alta dispersión — oportunidad para el sistema de recomendación)
- **Variables:** 40 columnas (usuario, restaurante, reseña, atributos)

---

## Modelos

| # | Modelo | RMSE | Precisión | Recall | F1 |
|---|--------|------|-----------|--------|----|
| 1 | Rank Based (baseline) | — | — | — | — |
| 2 | CF User-User (KNN) | 1.1203 | 0.736 | 0.823 | 0.777 |
| 3 | CF Item-Item (KNN) | 1.1356 | 0.729 | 0.827 | 0.775 |
| 4 | SVD Matrix Factorization | 1.0292 | 0.721 | 0.785 | 0.752 |
| 5 | SVD + Friends (Social Graph) | 1.1103 | 0.728 | 0.839 | 0.780 |
| **6** | **SVD + Sentiment Analysis** ✓ | **1.1103** | **0.728** | **0.846** | **0.783** |

**Métrica prioritaria: Recall** — la proporción de restaurantes relevantes que el sistema logra capturar.

---

## Red Social

El grafo construido con NetworkX conectó:
- **8.714 nodos** (usuarios)
- **32.917 aristas** (vínculos entre amigos)

La centralidad de cada usuario fue calculada con `degree_centrality` para identificar usuarios influyentes dentro de la red.

---

## Arquitectura Híbrida Recomendada

| Sección en la app | Modelo |
|---|---|
| Usuarios nuevos (cold start) | Rank Based |
| "Basado en tus reseñas" | SVD + Sentiment Analysis |
| "Lo que recomiendan tus amigos" | SVD + Friends |
| "Similares a tu historial" | CF Item-Item |

---

## Stack Técnico

```
Python · scikit-surprise · VADER (NLTK) · NetworkX · spaCy · pandas · seaborn
```

---

## Estructura del Repositorio

```
DineOrDash/
├── restaurant_recommendation.ipynb
├── Restaurants_recommendation_system.pptx
└── README.md
```

> **Dataset:** El dataset de Yelp no está incluido por su tamaño. Puede descargarse desde [Yelp Open Dataset](https://www.yelp.com/dataset).
