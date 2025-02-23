# Roadmap
Roadmap for the club.

The club's main focus is **analytic prompt engineering** and **systematic semantics analysis of prompts and answers**. 


## Analytics

The roadmap and development pipeline of the analytics team is as follows:

### Labelists

```mermaid
graph TD;
    subgraph Frontend
        A1["User Inputs Prompt"] -->|HTML DOM| A2["Express.js (Node.js @5000)"]
    end

    subgraph Backend
        A2 -->|Sends Prompt| B1["Flask Server @4040"]
        B1 -->|Embed Prompt| B2["Embedding Model → vec1"]
        B1 -->|Forwards to LLM| C1["Ollama LLM @11434"]
        C1 -->|Processes Prompt & Generates Answer| C2["Node.js Receives Answer"]
        C2 -->|"Express.js (Back to Frontend)"| A3["HTML DOM Displays Answer"]
    end

    subgraph Labeling Process
        A3 -->|User Labels Answer| D1["Express.js (Sends Label to Flask@4040)"]
        D1 -->|Embed Answer| D2["Embedding Model → vec2"]
        D2 -->|Store Combined Data in SQLite| D3["Save: vec1, vec2, prompt, answer, prompt label, answer label"]
        D3 -->|User Continues Prompting| A1
    end

    subgraph Prompt Labelists Interface
        A1 -->|Labelists Assign Prompt Labels| F1["Prompt Labeling by Labelists"]
        F1 -->|Store Labels in SQLite| F2["Store Prompt Labels with Data"]
    end

    subgraph Labelists Group
        A1 -->|Labelists Assign Semantic Dimensions| E1["Semantic Labeling by Group"]
        E1 -->|Store in SQLite| E2["Store Semantic Dimensions with Data"]
    end

    subgraph Public Network
        A2 -->|Cloudflared @5000| Net["Public Internet"]
    end

```

### Data Scientists

```mermaid
graph TD;
    subgraph Analytical Process
        A1["Receives DB Updates"] -->|Preprocess Dataset| B1["Preprocess Dataset"]
        
        subgraph Training Process
            B1 -->|Fetch Weights from Weights DB| C1["Fetch Weights from SQLite DB"]
            
            C1 -->|Load vec1 Weights & Prompts| D1["Train MLP on vec1 (Prompt Analyzer)"]
            D1 -->|Store Updated Weights| E1["Store Weights for Prompts"]
            
            C1 -->|Load vec2 Weights & Answers| D2["Train MLP on vec2 (Answer Analyzer)"]
            D2 -->|Store Updated Weights| E2["Store Weights for Answers"]
        end
        
        B1 -->|SQLite API via Python| F1["SQLite API"]
        
        subgraph Analysis
            F1 -->|Fetch Model & Data| G1["Fetch Model and Prompt/Answer Set"]
            G1 -->|Run Prompt/Answer Science Computations| H1["Run Prompt Science Computations (3.1)"]
            G1 -->|Run Answer Science Computations| H2["Run Answer Science Computations (3.2)"]
        end
    end

```

## Semantic Analysis

!TODO
