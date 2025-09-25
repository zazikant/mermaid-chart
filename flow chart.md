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


