# Segmentation-and-Template-Matching



Question 3 : 

          ┌──────────────────────────────┐
          │  Start: Input Test Image     │
          └────────────┬─────────────────┘
                       ↓
          ┌──────────────────────────────┐
          │  Preprocess the Image        │
          │  (Grayscale, Resize, Blur,   │
          │  Threshold)                   │
          └────────────┬─────────────────┘
                       ↓
          ┌──────────────────────────────┐
          │ Load Template Digits (0-9)   │
          │ from Sample Directory        │
          └────────────┬─────────────────┘
                       ↓
          ┌──────────────────────────────┐
          │ Template Matching (ZNCC)     │
          │ - Compare with all templates │
          │ - Find highest similarity    │
          └────────────┬─────────────────┘
                       ↓
          ┌──────────────────────────────┐
          │ KNN Classification (k=3)     │
          │ - Compute Euclidean distance │
          │ - Select nearest templates   │
          │ - Majority voting            │
          └────────────┬─────────────────┘
                       ↓
      ┌────────────────────────────────────┐
      │  Display Predictions:               │
      │  - Template Matching Result (ZNCC)  │
      │  - KNN Classification Result        │
      └────────────────────────────────────┘
                       ↓
          ┌──────────────────────────────┐
          │            End               │
          └──────────────────────────────┘
