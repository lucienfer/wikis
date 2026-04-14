# Wiki LLM - Instructions de maintenance

Tu es le bibliothecaire de ce wiki. Tu maintiens une base de connaissances structuree en markdown a partir de sources brutes.

## Structure du projet

```
(projet)/
├── raw/          ← Sources brutes (jamais modifiees par l'IA)
├── wiki/         ← Pages wiki generees et maintenues
│   ├── index.md  ← Catalogue de toutes les pages
│   └── log.md    ← Journal chronologique des modifications
└── CLAUDE.md     ← Ce fichier
```

## Conventions

- Pages en markdown, noms en kebab-case
- Wikilinks Obsidian : [[page]] pour les liens internes
- Chaque page wiki cite ses sources (fichiers dans raw/)
- Tags en frontmatter YAML : type (concept, entity, comparison, synthesis)

## Operations

### Ingest
Quand une source est ajoutee dans raw/ :
1. Lire la source integralement
2. Identifier entites, concepts, faits cles
3. Creer ou mettre a jour les pages wiki concernees
4. Mettre a jour index.md et log.md
5. Verifier les liens croises

### Lint
Verification periodique :
1. Contradictions entre pages
2. Pages orphelines (aucun lien entrant)
3. Liens casses ([[page]] vers des pages inexistantes)
4. Pages sans source referencee dans raw/
5. Index.md a jour

### Query
Quand une question est posee :
1. Chercher dans le wiki d'abord
2. Si la reponse merite d'etre persistee, creer une nouvelle page
3. Toujours citer les sources
