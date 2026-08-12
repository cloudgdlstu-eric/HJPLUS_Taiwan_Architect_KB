---
type: Skill
name: sprinkler-foam-piping-review
description: "This skill should be used when reviewing fire sprinkler and foam piping designs in Taiwan, checking the pipe sizes (diameters) based on the number of sprinkler/foam heads, layout rules, and flow calculations."
license: CC-BY-SA-4.0
compatibility: claude-code,opencode,agent-skills
verified:
  - { by: human:ericlee, at: 2026-08-12T00:00:00Z }
sources:
  - id: fire-standards-56
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=56
    title: 各類場所消防安全設備設置標準 §56
    last_modified: 2024-03-14
  - id: fire-standards-79
    resource: https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=D0120029&flno=79
    title: 各類場所消防安全設備設置標準 §79
    last_modified: 2024-03-14
metadata:
  audience: architects
  region: taiwan
  class: C
  status: verified
  data-currency: "2026-08-12"
---

# Sprinkler and Foam Piping System Review (灑水與泡沫滅火系統配管檢討)

## Overview

This skill provides the regulatory criteria and verification workflow for reviewing fire sprinkler and foam piping designs in Taiwan. It covers the mapping of sprinkler head counts to nominal pipe diameters, limits on sprinkler heads per branch line, and layout and zoning rules for foam systems.

---

## Section 1: Verification Workflow

When reviewing a fire protection piping design, follow these steps:

### Step 1: Identify the System Type
Determine if the system is:
*   **Automatic Sprinkler System (自動撒水設備)**: Relies on thermal-sensitive closed heads or open heads.
*   **Foam Extinguishing System (泡沫滅火設備)**: Commonly used in parking garages, generator rooms, or machine rooms.

### Step 2: Validate Pipe Sizing based on Head Count (for Sprinkler Systems)
Confirm the nominal diameter (mm) of each pipe segment based on the number of downstream sprinkler heads. Use the following regulatory mapping[^fire-standards-56]:

| Nominal Diameter (mm) | Metric / Imperial (inches) | Maximum Allowed Downstream Heads |
| :--- | :--- | :---: |
| **25** | 1" | 2 |
| **32** | 1-1/4" | 3 |
| **40** | 1-1/2" | 5 |
| **50** | 2" | 10 |
| **65** | 2-1/2" | 30 |
| **80** | 3" | 60 |
| **90** | 3-1/2" | 100 |
| **100 or larger** | 4" or larger | > 100 |

### Step 3: Check Branch Line Limits
Verify that **no individual branch line** (a pipe segment directly feeding sprinkler heads) has more than **8 sprinkler heads** connected to it[^fire-standards-56].

### Step 4: Validate Foam System Layout (for Foam Systems)
For foam system review, check the following criteria:
1.  **Zoning (放射區域)**: Each zoning area must have a floor area between **50 m² and 100 m²**[^fire-standards-79].
2.  **Coverage Radius (水平距離)**: The horizontal distance from any point on the protected floor to the nearest foam head must be **2.1 meters or less**[^fire-standards-79].
3.  **Pipe Specification**: Validate that the foam solution piping is dedicated and uses galvanized steel pipes of Sch 40 (for low-pressure lines) or Sch 80 (for high-pressure lines)[^fire-standards-79].

---

## Section 2: Enforcement and Error Messages

During verification, if any of the criteria are violated, output the corresponding warnings or errors as follows:

*   **Excessive Sprinkler Heads on a Branch Line**:
    *   *Warning/Error*: `[Error] Branch line [Branch_ID] has [Count] heads connected. Max allowed is 8 heads. (各類場所消防安全設備設置標準 §56)`
*   **Undersized Pipe Sizing**:
    *   *Warning/Error*: `[Error] Pipe segment [Segment_ID] with diameter [Size]mm serves [Count] heads. Max allowed for [Size]mm is [Max] heads. (各類場所消防安全設備設置標準 §56)`
*   **Invalid Foam Zone Area**:
    *   *Warning/Error*: `[Error] Foam zone [Zone_ID] has an area of [Area] m². Allowed range is 50 to 100 m². (各類場所消防安全設備設置標準 §79)`
*   **Excessive Horizontal Distance for Foam Heads**:
    *   *Warning/Error*: `[Warning] Maximum horizontal distance to nearest foam head in zone [Zone_ID] is [Distance]m. Max allowed is 2.1m. (各類場所消防安全設備設置標準 §79)`

---

## Related Skills

*   [building-services](../../../專業複委託/機電系統/building-services/SKILL.md) — For overall building service integration and mechanical design.
*   [taiwan-plumbing-design-codes](../../../建築法規/建築物給水排水設備設計技術規範/plumbing-drainage-design-code/SKILL.md) — For standard plumbing design rules in Taiwan.
*   [tw-mep-spec-wiki](../../../專業複委託/機電系統/台灣機電物料百科/tw-mep-spec-wiki/SKILL.md) — For details on galvanized piping specifications (CNS 6445 / ASTM Sch40).
