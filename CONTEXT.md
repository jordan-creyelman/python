# Contexte global — Projets Python

## Mission

Servir de référence commune pour concevoir, développer, maintenir et faire évoluer de futurs projets Python : scripts, automatisations, outils CLI, APIs, applications et expérimentations.

## Principes

- Privilégier la simplicité, la lisibilité, la maintenabilité et la fiabilité.
- Commencer par clarifier l'objectif, les entrées/sorties, les contraintes et les critères de réussite.
- Ne pas choisir une architecture ou une dépendance sans besoin concret.
- Faire évoluer le projet progressivement : petite version fonctionnelle, puis améliorations ciblées.
- Préserver la compatibilité et les fonctionnalités existantes lors des modifications.

## Règles de conception prioritaires

- **PEP 8** : formatage cohérent, nommage explicite, imports organisés, code Python idiomatique.
- **KISS (Keep It Simple, Stupid)** : choisir la solution la plus simple qui fonctionne ; refuser la complexité spéculative.
- **Fonctions modulaires** : petites fonctions cohérentes, une responsabilité, arguments et valeurs de retour clairs ; privilégier des fonctions pures quand c'est possible.
- **Clean Code** : code auto-explicatif, faible duplication, gestion explicite des erreurs, intention claire ; commentaires pour le « pourquoi », pas pour répéter le code.
- **SOLID** : appliquer les cinq principes quand ils aident réellement à faire évoluer une conception orientée objet ; ne pas ajouter de classes ou d'interfaces artificielles.
- **Clean Architecture** : séparer règles métier, orchestration et infrastructure lorsqu'il existe une complexité qui le justifie ; les détails techniques dépendent du métier, pas l'inverse.
- **YAGNI** : ne pas anticiper des fonctionnalités ou couches non demandées.
- **Tests** : concevoir les composants pour être testables isolément, sans multiplier les mocks inutilement.

## Architecture proportionnée à la taille du projet

Choisir en fonction de la complexité métier, des dépendances, des intégrations et de la maintenance attendue — pas seulement du nombre de lignes.

### Petit projet — script ou utilitaire ponctuel

- Un ou quelques fichiers Python, fonctions réutilisables et point d'entrée `main()`.
- Aucun dossier `domain/`, `application/` ou interface abstraite par défaut.
- Extraire un module seulement si cela améliore réellement la compréhension ou la réutilisation.

### Projet moyen — application, CLI ou API avec plusieurs fonctionnalités

- Organiser en modules par responsabilité ou par fonctionnalité.
- Séparer la logique métier des entrées/sorties, du framework et de la persistance.
- Garder des dépendances explicites et des tests ciblés.
- Introduire des services ou des interfaces seulement lorsque plusieurs implémentations ou tests le justifient.

### Grand projet — domaine complexe et évolution durable

- Envisager **Clean Architecture** : `domain/` (règles métier), `application/` (cas d'usage), `infrastructure/` (BDD, API, fichiers), `interfaces/` (HTTP, CLI, UI).
- Les dépendances de code pointent vers l'intérieur : la logique métier ne dépend ni du framework, ni de la base de données.
- Définir des contrats aux frontières lorsque c'est utile ; privilégier la composition et l'injection explicite des dépendances.
- Appliquer SOLID pour limiter le couplage, sans complexité cérémonielle.

**Règle d'arbitrage : KISS et besoin concret priment sur l'application mécanique d'un pattern ou d'un principe SOLID.** Refactoriser vers plus de structure quand des besoins observables apparaissent.

## Philosophie et arbitrage

**Simple by default, modular by design, scalable when needed.**

En cas d'arbitrage, viser dans cet ordre : correction du comportement, simplicité, lisibilité, maintenabilité, testabilité, modularité, évolutivité, puis performance mesurée. La sécurité et les contraintes métier restent impératives, pas des optimisations facultatives.

## Conception et bonnes pratiques complémentaires

- **Type hints** : annoter les interfaces importantes, les paramètres et les retours ; éviter d'ajouter des types qui nuisent à la lisibilité.
- **Fail fast** : valider les préconditions et les entrées aux frontières ; produire des erreurs explicites et exploitables.
- **Separation of concerns** : isoler métier, orchestration, présentation et accès aux ressources lorsque cela simplifie l'évolution.
- **Dependency injection** : passer explicitement les dépendances nécessaires (paramètres, constructeurs) ; ne pas installer un conteneur DI sans besoin.
- **Tests centrés sur le comportement** : vérifier cas nominaux, limites et erreurs ; limiter les mocks aux frontières externes.
- **Explicit is better than implicit** : éviter les effets de bord cachés, l'état global mutable et les conventions magiques.
- **Composition over inheritance** : composer des comportements avant de construire des hiérarchies d'héritage.
- **Observabilité** : utiliser `logging`, des messages contextualisés et des diagnostics utiles ; journaliser sans divulguer de secrets.
- **Configuration** : distinguer configuration, secrets et logique ; valider les paramètres au démarrage ; fournir des exemples non sensibles.
- **Documentation as code** : maintenir README, exemples d'usage et décisions techniques avec les changements correspondants.

## Garde-fous anti-surarchitecture

- Une fonction plutôt qu'une classe quand elle suffit.
- Pas d'interface abstraite avec une seule implémentation sans besoin documenté.
- Pas de pattern ou de couche supplémentaire sans problème concret.
- Ne pas fractionner des fonctions triviales en une multitude de fichiers.
- Ne pas ajouter de bibliothèque, de framework ou de service avant d'en justifier l'utilité.
- Ne pas anticiper des fonctionnalités hypothétiques ; refactoriser progressivement quand le besoin apparaît.
- DDD, CQRS et architecture hexagonale complète ne sont jamais des obligations par défaut.

## Outillage et automatisation proportionnés

- **Ruff** pour lint et formatage, **pytest** pour les tests.
- **Mypy ou Pyright** pour vérifier les types si la taille ou le risque le justifie.
- **pre-commit** pour lancer les contrôles locaux lorsque l'équipe ou le projet en bénéficie.
- **GitHub Actions** pour vérifier lint, types et tests à chaque pull request sur les projets maintenus.
- Pour un script ponctuel, privilégier la simplicité : quelques tests utiles et une vérification locale peuvent suffire.
- Les commandes et configurations réellement choisies doivent figurer dans le README du projet.
- Ne pas déclarer des contrôles réussis sans les avoir exécutés.

## Environnement

- Utiliser une version de Python récente et maintenue, adaptée aux dépendances et à la cible d'exécution ; consigner la version choisie dans chaque projet.
- Isoler les dépendances avec un environnement virtuel (`python -m venv .venv`).
- Déclarer explicitement les dépendances et, pour les applications, figer des versions reproductibles.
- Préférer `pyproject.toml` pour configurer le projet et ses outils lorsque cela est pertinent.
- Ne jamais versionner `.venv/`, les caches, les secrets ou les fichiers générés temporaires.

## Architecture indicative

Pour un projet suffisamment structuré :

```text
mon-projet/
├── README.md
├── AGENTS.md
├── pyproject.toml
├── .gitignore
├── .env.example          # uniquement si nécessaire
├── src/
│   └── mon_projet/
│       ├── __init__.py
│       └── main.py
└── tests/
    └── test_main.py
```

Pour un petit script, une structure plus légère est préférable. Ne pas créer des dossiers vides inutilement.

## Style de code

- Respecter PEP 8 et adopter des noms explicites.
- Utiliser les annotations de type pour les interfaces importantes.
- Écrire des fonctions courtes avec une responsabilité claire.
- Ajouter des docstrings utiles aux fonctions publiques et aux comportements non évidents.
- Éviter les duplications, les constantes magiques et les abstractions prématurées.
- Utiliser `pathlib` pour manipuler les chemins et `logging` pour les journaux d'exécution.
- Isoler les effets de bord (fichiers, réseau, bases de données) du code métier quand c'est pertinent.

## Qualité et tests

- Préférer `pytest` pour les tests, sauf contrainte contraire.
- Couvrir les comportements critiques, les cas limites et les erreurs attendues.
- Utiliser `ruff` pour le lint et le formatage lorsque le projet le permet.
- Ajouter une vérification de types (par exemple `mypy` ou `pyright`) si la complexité le justifie.
- Avant livraison : exécuter les tests et contrôles disponibles ; signaler clairement ceux qui n'ont pas été exécutés.
- Ne jamais prétendre qu'un test est passé sans l'avoir lancé.

## Sécurité et robustesse

- Aucun secret, jeton, mot de passe ou clé API dans le code ou l'historique Git.
- Utiliser des variables d'environnement pour la configuration sensible et fournir `.env.example` sans valeurs confidentielles si nécessaire.
- Valider les données externes, gérer les erreurs de manière précise et éviter les `except:` silencieux.
- Définir des délais d'attente pour les appels réseau et limiter les tentatives répétées.
- Ne pas exécuter de commandes, supprimer des données ou modifier la production sans nécessité explicite.
- Maintenir les dépendances et éviter celles qui sont inutiles.

## Contrats, erreurs et résilience

- **Design by Contract** : documenter et vérifier les préconditions, postconditions et invariants utiles, sans imposer un framework de contrats.
- **Fail fast aux frontières** : valider les entrées externes avant la logique métier, avec des messages d'erreur compréhensibles.
- Lever des exceptions **spécifiques** et cohérentes ; préserver la cause avec `raise ... from exc` lorsque pertinent.
- Capturer les erreurs seulement là où l'on peut les traiter, les enrichir ou les traduire pour l'appelant.
- Ne jamais utiliser `except: pass` ni masquer un échec ; éviter `except Exception` sauf aux frontières de supervision, avec journalisation et réaction explicites.
- Distinguer erreur métier, validation, infrastructure et bug ; ne pas transformer un bug en succès silencieux.
- Ne pas enregistrer de secrets ou de données personnelles dans les logs ; éviter les logs multiples pour une même erreur.
- Pour les ressources externes : timeouts systématiques ; retries limités avec backoff seulement sur opérations sûres/idempotentes et erreurs transitoires.
- Nettoyer les ressources avec des gestionnaires de contexte (`with`) et prévoir des transactions/rollback lorsqu'il y a des écritures multiples.

## Stratégie de tests unitaires et d'intégration

- Utiliser **pytest** par défaut et privilégier des tests déterministes, indépendants et rapides.
- **Tests unitaires** : isoler une fonction ou un composant métier ; vérifier entrées/sorties, cas nominaux, limites et exceptions attendues ; mocker uniquement les frontières nécessaires.
- **Tests d'intégration** : vérifier que plusieurs composants fonctionnent ensemble (BDD, fichiers, API, sérialisation, configuration) ; préférer des ressources de test réelles et isolées quand c'est raisonnable.
- Ne jamais appeler un service de production ou modifier des données réelles depuis les tests.
- Ranger les tests dans `tests/unit/` et `tests/integration/` dès que leur séparation apporte un bénéfice ; un seul `tests/` suffit pour les petits projets.
- Marquer les tests d'intégration avec `@pytest.mark.integration` si pertinent, et documenter leurs prérequis.
- Exécuter les tests unitaires fréquemment ; exécuter les tests d'intégration en CI avec les services nécessaires.
- Pour chaque bug corrigé, ajouter si possible un test de non-régression.
- Mesurer la couverture sur les projets suivis si utile, mais **ne pas viser un pourcentage arbitraire au détriment de tests pertinents**.
- Tests de bout en bout, performance et charge : uniquement si les risques du projet le justifient.
- Commandes possibles : `pytest tests/unit`, `pytest tests/integration`, `pytest`. Adapter à la structure réelle.

## Sécurité, dépendances et refactoring

- **Security by Design** : valider les entrées, limiter les permissions, protéger les secrets et éviter toute exécution non maîtrisée de commandes ou contenu externe.
- Déclarer et suivre les dépendances directes ; utiliser un fichier de verrouillage ou une méthode reproductible adaptée au projet, et examiner les mises à jour et alertes de sécurité.
- **Refactoring incrémental** : stabiliser le comportement avec des tests avant toute modification structurelle ; effectuer de petits changements contrôlables et réexécuter les contrôles.
- Privilégier des migrations explicites et réversibles pour les changements de schéma ou de données.

## Documentation attendue par projet

Chaque projet doit expliquer :
1. Son objectif et son périmètre.
2. Les prérequis et l'installation.
3. Les commandes pour démarrer, tester et vérifier le code.
4. La configuration nécessaire, sans secrets.
5. Les principales décisions et limites connues.

## Façon de travailler

1. Comprendre la demande et examiner l'existant.
2. Proposer l'approche la plus simple qui couvre le besoin.
3. Modifier uniquement les fichiers nécessaires.
4. Ajouter ou adapter les tests pertinents.
5. Vérifier les résultats.
6. Résumer les changements, les commandes utiles et les points restant à traiter.

## Adaptation

Ce contexte est un point de départ. Les consignes propres à un projet, ses exigences métier, son environnement et ses choix techniques validés sont prioritaires. Mettre à jour ce document lorsque les conventions générales évoluent.
