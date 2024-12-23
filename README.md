```mermaid
flowchart TB
%% Main workflow sections with icons
subgraph SP["fa:fa-vial 1. Sample Preparation & QC"]
    direction TB
    fresh("fa:fa-flask Fresh Tissue")
    ffpe("fa:fa-box FFPE Tissue")
    dissoc("fa:fa-mortar-pestle Tissue Dissociation")
    batch("fa:fa-layer-group Batch Considerations")
    
    fresh --> dissoc
    ffpe --> dissoc
    dissoc --> batch
    note1["fa:fa-info-circle Bone Tumor Specific<br>Handling Considerations<br>Bruning et al, 2022"]
    dissoc -.- note1
end

subgraph DP["fa:fa-microchip 2. Data Processing"]
    direction TB
    raw("fa:fa-database Raw Data")
    artrem("fa:fa-filter Artifact Removal")
    norm("fa:fa-balance-scale Normalization")
    
    raw --> |"alevin-fry (He et al, 2022)<br>cellranger<br>STARsolo (Kaminow et al, 2021)"| artrem
    artrem --> |"SoupX (Young & Behjati, 2020)<br>cellbender (Fleming et al, 2023)"| norm
    note2["fa:fa-check-circle QC metrics & filtering<br>Cell cycle, Mitochondria, nFeature"]
    norm -.- note2
end

subgraph INT["fa:fa-object-group 3. Integration"]
    direction TB
    harm("fa:fa-project-diagram Harmony<br>Korsunsky et al, 2019")
    seurat("fa:fa-network-wired Seurat v4<br>Hao et al, 2021")
    signac("fa:fa-code-branch Signac<br>Stuart et al, 2021")
    liger("fa:fa-sitemap LIGER<br>Welch et al, 2019")
    scvi("fa:fa-brain scVI<br>Gayoso et al, 2022")
    fastmnn("fa:fa-compress-arrows-alt fastMNN<br>Zhang et al, 2019")
end

subgraph ANN["fa:fa-tags 4. Cell Type Annotation"]
    direction TB
    pre["fa:fa-robot Pre-Trained<br>sc-type (Ianevski et al, 2022)<br>SingleR (Aran et al, 2019)<br>scGate (Andreatta et al, 2022)"]
    cust["fa:fa-cogs Custom<br>SVM (Abdelaal et al, 2019)<br>scDeepSort (Shao et al, 2021)"]
    mark["fa:fa-bookmark Markers<br>Osteoblast (Amarasekara et al, 2021)<br>MSC (Patel et al, 2016)<br>Osteoblast (Hojo et al, 2022)"]
end

subgraph TUMOR["fa:fa-dna 5. Tumor Analysis"]
    direction TB
    cnv("fa:fa-chart-line CNV Analysis")
    note3["inferCNV<br>copyKat (Gao et al, 2021)<br>SCEVAN (De Falco et al, 2023)<br>numbat (Gao et al, 2022)"]
    cnv -.- note3
end

subgraph TRAJ["fa:fa-route 6. Trajectory"]
    direction TB
    mono("fa:fa-stream Monocle<br>Qiu et al, 2017")
    sling("fa:fa-bezier-curve Slingshot<br>Street et al, 2018")
    velo("fa:fa-tachometer-alt velocyto<br>Manno et al, 2018")
    state("fa:fa-map-signs State Prediction<br>Weistuch et al, 2024")
end

subgraph STAT["fa:fa-calculator 7. Statistics"]
    direction TB
    de("fa:fa-not-equal DE Models<br>MAST, ZINB-WaVE")
    pseudo("fa:fa-copy Pseudoreplication")
    mt("fa:fa-tasks Multiple Testing<br>FDR, Bonferroni")
end

subgraph FUNC["fa:fa-puzzle-piece 8. Functional"]
    direction TB
    gsea("fa:fa-chart-bar GSEA<br>Korotkevich et al, 2021")
    meta("fa:fa-atom Metabolic<br>Wagner et al, 2021")
    comm("fa:fa-comments Communication<br>CellChat v2 (Jin et al, 2024)<br>cellphoneDB (Garcia-Alonso)")
end

subgraph DATA["fa:fa-database 9. Datasets"]
    note6["GSE152048 (Zhou et al, 2020)<br>GSE162454 (Liu et al, 2021)<br>GSE87624 (Scott et al, 2018)<br>SCPCP000017/18/23<br>GSE147390 (Gong et al, 2020)<br>GSE200529 (Truong et al, 2024)"]
end

%% Main workflow connections
SP --> DP --> INT --> ANN
ANN --> TUMOR
ANN --> TRAJ
ANN --> STAT
STAT --> FUNC
FUNC --> DATA

%% Rustic color palette
style SP fill:#D47553,stroke:#333,stroke-width:2px,color:#fff
style DP fill:#8B9E81,stroke:#333,stroke-width:2px,color:#fff
style INT fill:#DDB892,stroke:#333,stroke-width:2px,color:#333
style ANN fill:#9E6B57,stroke:#333,stroke-width:2px,color:#fff
style TUMOR fill:#B6855F,stroke:#333,stroke-width:2px,color:#fff
style TRAJ fill:#A47551,stroke:#333,stroke-width:2px,color:#fff
style STAT fill:#C17F59,stroke:#333,stroke-width:2px,color:#fff
style FUNC fill:#B67F66,stroke:#333,stroke-width:2px,color:#fff
style DATA fill:#9E7B65,stroke:#333,stroke-width:2px,color:#fff

classDef note fill:#fff,stroke:#999,stroke-width:1px,color:#666,font-size:10px
class note1,note2,note3,note4,note5,note6 note
```
