#  Infrastructure Technique Radio Vostok

//TODO blabla présentation

## Vision d'ensemble

```mermaid
graph TD
    subgraph locaux
    A[studio principal] --> B[régie principale]
    P[Scène village] --> B[régie principale]
    B[régie principale] --> C[CDM]
    D[studio 2] --> C[CDM]
    Z[booth dj] --> C[CDM]
    end
    G[bus / émissions extérieures] <--> C[CDM]
    subgraph diffusion
    C[CDM] --> E[diffusion DAB]
    C[CDM] --> F[diffusion web]
    end
    subgraph outils et publications web
    C[CDM] <--> H[Clouds]
    H[Clouds] <--> C[CDM]
    H[Clouds / VPM] --> I[radiovostok.ch]
    H[Clouds] --> J[radiobascule.ch]
    H[Clouds] --> K[blogostok]
    H[Clouds] --> L[réseaux sociaux]
    H[Clouds] --> M[plateformes podcast]
    H[Clouds] --> N[App]
    end
    G[bus / émissions extérieures] .-> O[CDM backup] 
    O[CDM backup] .-> E[diffusion DAB]
    O[CDM backup] .-> F[diffusion web]
    Q[Équipements reportage] .-> H[Clouds]
    Q[Équipements reportage] .-> C[CDM]
```
## Inventaire 

// TODO
(pistes outils inventaire à noter ici)

## État des services 

// TODO
(pistes outils monitoring à noter ici)

monitoring actuel :
- détecteur de silence
    - flux internet
    - la vostoke (// TODO à fiabiliser)
    - DAB (//TODO à remettre en service)
- ..