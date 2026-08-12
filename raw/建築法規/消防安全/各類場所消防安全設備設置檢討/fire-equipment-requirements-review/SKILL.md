---
type: Skill
name: fire-equipment-requirements-review
description: "This skill should be used when analyzing or generating the required fire safety equipment checklist for a building in Taiwan, evaluating parameters like occupancy usage, height, floors, total area, basement floors, and windowless floors against the statutory thresholds of the Fire Safety Standards."
license: CC-BY-SA-4.0
compatibility: claude-code,opencode,agent-skills
verified:
  - { by: human:ericlee, at: 2026-08-12T00:00:00Z }
sources:
  - id: fire-standards-12
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=12
    title: 各類場所消防安全設備設置標準 §12 (場所分類)
    last_modified: 2024-03-14
  - id: fire-standards-extinguisher
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=14
    title: 各類場所消防安全設備設置標準 §14 (滅火器)
    last_modified: 2024-03-14
  - id: fire-standards-hydrant
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=15
    title: 各類場所消防安全設備設置標準 §15 (室內消防栓)
    last_modified: 2024-03-14
  - id: fire-standards-sprinkler
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=17
    title: 各類場所消防安全設備設置標準 §17 (自動撒水設備)
    last_modified: 2024-03-14
  - id: fire-standards-alarm
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=19
    title: 各類場所消防安全設備設置標準 §19 (火警自動警報設備)
    last_modified: 2024-03-14
  - id: fire-standards-smoke
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=188
    title: 各類場所消防安全設備設置標準 §188 (排煙設備)
    last_modified: 2024-03-14
metadata:
  audience: architects
  region: taiwan
  class: C
  status: verified
  data-currency: "2026-08-12"
---

# Fire Equipment Requirements Review (各類場所消防安全設備設置檢討)

## Overview

This skill guides the AI agent through the step-by-step checklist generation for fire protection systems in a building project in Taiwan. By taking building input properties (classification, height, levels, floor area, basements, windowless floors), the agent identifies the applicable statutory rules and outputs a compliant checklist.

---

## Section 1: Review Parameter Requirements

When evaluating a project, the agent must collect the following input parameters:
1.  **Usage Classification (場所用途分類)**: Class A, B, C, D, or E per Article 12[^fire-standards-12].
2.  **Number of Floors (地上層數/地下層數)**.
3.  **Building Height (建築物高度 in meters)**.
4.  **Total Floor Area (總樓地板面積 in m²)**.
5.  **Floor Area of Specific Floors (單層樓地板面積, 地下層面積, 無窗戶層面積 in m²)**.
6.  **Windowless Status (是否含無窗戶層)**.

---

## Section 2: Core Equipment Rules & Thresholds

The agent must check the inputs against the following statutory thresholds:

### 1. Extinguisher (滅火器) [^fire-standards-extinguisher]
*   **Mandatory**: If building has any Class A occupancy, or Class B/C/D/E with total area $\ge 150\text{ m}^2$, or any basement/windowless floor $\ge 50\text{ m}^2$.

### 2. Indoor Fire Hydrant (室內消防栓) [^fire-standards-hydrant]
*   **Trigger A (Class A Occupancy)**: Total area $\ge 150\text{ m}^2$ (or $\ge 75\text{ m}^2$ for basements/windowless floors).
*   **Trigger B (Class B Occupancy)**: Total area $\ge 500\text{ m}^2$ (or $\ge 150\text{ m}^2$ for basements/windowless floors).
*   **Trigger C (Class C - Factory/Warehouse)**: Total area $\ge 700\text{ m}^2$ (or $\ge 150\text{ m}^2$ for basements/windowless floors).
*   **Trigger D (Class D - Parking)**: Total area $\ge 200\text{ m}^2$ (or $\ge 150\text{ m}^2$ for basements/windowless floors).
*   **Trigger E (Floor Count)**: Any building of 6 stories or more, or floors 1-5 with floor area $\ge 150\text{ m}^2$ per floor.

### 3. Automatic Sprinkler System (自動撒水設備) [^fire-standards-sprinkler]
*   **Trigger A (Height/Stories)**: Any building 11 stories or more, or height $> 31\text{ meters}$ (sprinkler required on floors 11 and above, or all floors depending on occupancy and zoning).
*   **Trigger B (Basements)**: Basement floor area $\ge 1000\text{ m}^2$.
*   **Trigger C (Class A)**: Stories 1 to 10 with area $\ge 1000\text{ m}^2$, or basements/windowless floors $\ge 1000\text{ m}^2$.
*   **Trigger D (Class B)**: Stories 1 to 10 with area $\ge 1500\text{ m}^2$.
*   **Trigger E (Class C)**: Factory or warehouse area $\ge 1500\text{ m}^2$ (non-fireproof) or $\ge 3000\text{ m}^2$ (fireproof).

### 4. Automatic Fire Alarm System (火警自動警報設備) [^fire-standards-alarm]
*   **Trigger A (Class A)**: Total area $\ge 150\text{ m}^2$ (or $\ge 75\text{ m}^2$ for basements/windowless floors).
*   **Trigger B (Class B/C/D)**: Total area $\ge 500\text{ m}^2$ (or $\ge 150\text{ m}^2$ for basements/windowless floors).
*   **Trigger C (Floor Count)**: Any building of 5 stories or more with total area $\ge 500\text{ m}^2$.

### 5. Smoke Exhaust System (排煙設備) [^fire-standards-smoke]
*   **Trigger A (Class A)**: Floor area of Class A space $\ge 300\text{ m}^2$.
*   **Trigger B (Windowless)**: Any windowless floor with area $\ge 50\text{ m}^2$.
*   **Trigger C (Basements)**: Basement floor area $\ge 1000\text{ m}^2$.
*   **Trigger D (Class B/C/D/E)**: Floor area of spaces without natural ventilation opening $\ge 300\text{ m}^2$.

---

## Section 3: Interactive Verification Flow

When answering user queries:
1.  Ask for the 6 input parameters if they are not provided.
2.  Perform logical evaluation for each of the core equipment categories.
3.  Output the results in the standard format:
    *   **Required Equipment Checklist**: Highlight which items are triggered and the specific clauses.
    *   **Evaluation Path**: Clear rationale of why an item is triggered or exempted.
