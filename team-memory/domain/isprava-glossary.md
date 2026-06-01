---
name: isprava-glossary
description: Isprava-specific terminology, business rules, and domain concepts Claude should always apply when working on any Isprava-related task
metadata:
  type: domain
  updated: 2026-05-25
---

# Isprava Domain Knowledge & Glossary

Company-specific terms, business rules, and domain concepts. Claude should apply these definitions whenever they appear in a task, PRD, or analysis — do not use generic industry definitions that conflict with these.

---

## Core terminology

| Term | Definition | Notes |
|------|-----------|-------|
| **Guest** | A person who books and stays at an Isprava property | May or may not be the same person as the contact who made the booking |
| **Property Manager** | The person or team responsible for a specific villa or property | Can be internal Isprava staff or an external partner |
| **Booking** | A confirmed reservation for a guest at a property for specific dates | Distinct from an enquiry or a hold |
| **Ops team** | Isprava's internal operations team | Manages the platform, resolves issues, handles escalations |
| *(Add more terms)* | | |

---

## Business rules

| Rule | Description | Where it applies |
|------|-------------|-----------------|
| *(e.g. "Minimum booking window")* | *(e.g. Bookings must be made at least X days in advance)* | *(e.g. Booking flow)* |

---

## Domain concepts

| Concept | Explanation |
|---------|------------|
| *(Add Isprava-specific concepts that need clarification)* | |

---

## How to update this file

Add terms in alphabetical order within their section. If a term has a nuance that differs from the generic industry definition, include a "Notes" entry explaining the difference. Commit with: `docs(team-memory): add [term] to glossary`
