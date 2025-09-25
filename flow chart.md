Open below code in https://mermaid.live/
==============

flowchart TD
 subgraph Enrichment_Subgraph["Email → Company Summary Pipeline"]
        G["Extract Domain\n(e.g., name@kalpataru.com → kalpataru.com)"]
        F["For Each Email"]
        H["Build Search Query\n(Gemini)"]
        I["Serper API Search"]
        J["Select Best URL\n(Gemini + Confidence)"]
        K["BrightData Scraping\n(With Polling)"]
        L["Summarize Website\n(Gemini: One-line)"]
        M["Merge Summary\ninto LinkedIn Profile"]
  end
    A(["Start"]) --> B["Trigger LinkedIn Discovery\n(BrightData Name API)"]
    B -- Success --> C["Wait for Profiles\n(Early Termination Enabled)"]
    B -- Error --> Z(["End: Error"])
    C --> D["Filter Profiles\n• Company Regex\n• Quality Score ≥4"]
    D --> E{"Any Emails\nin Profiles?"}
    E -- No --> Z
    E -- Yes --> F
    F --> G
    G --> H
    H --> I
    I --> J
    J --> K
    K --> L
    L --> M
    M --> N{"More Emails?"}
    N -- Yes --> F
    N -- No --> Z
    Z --> O(["End: Return Enriched Leads"])

    style A stroke:#FFD600

==============


In Mermaid flowcharts, different **shapes (boxes)** represent different types of steps or logic:

---

### 📦 Common Shapes & Their Meanings

| Shape          | Symbol / Type      | Meaning                                                                 |
|----------------|--------------------|-------------------------------------------------------------------------|
| **Rectangle**  | `A[Process Step]`  | A **process**, **action**, or **operation** (e.g., “Filter Profiles”, “Scrape Website”) |
| **Diamond**    | `B{Decision}`      | A **decision point** — typically has 2+ outgoing paths (Yes/No, True/False) |
| **Rounded Box**| `C([Start/End])`   | **Start or End** of the workflow (terminal nodes)                       |
| **Circle**     | `D((Node))`        | Connector or off-page reference (less common in basic flows)            |
| **Subgraph**   | `subgraph X [...]` | Group of related nodes (visually boxes them together)                   |

---

### ✅ In Your Diagram:
- `Filter Profiles...` → **Rectangle** = Processing step
- `Any Emails...?` → **Diamond** = Decision (Yes/No branch)
- `End: Error` → **Rounded Box** = Terminal state (end of flow)

---

### 💡 Pro Tip:
You can customize shapes for clarity:
```mermaid
A[Normal Process]
B{Decision}
C([Start])
D[[Database]]
E>Output]
```

This helps visually distinguish between **actions**, **decisions**, **start/end**, and **data stores**.
