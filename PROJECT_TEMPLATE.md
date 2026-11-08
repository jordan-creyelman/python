# Modèle de contexte — Nouveau projet Python

> Copier et adapter ce fichier au démarrage d'un projet. Supprimer les rubriques non pertinentes. Respecter `CONTEXT.md` et `AGENTS.md` du dépôt de référence.

## Présentation
- Nom :
- Objectif :
- Utilisateurs / contexte d'exécution :
- Fonctionnalités essentielles :
- Hors périmètre :

## Contraintes et choix techniques
- Version Python :
- Environnement de déploiement :
- Dépendances et justification :
- Configuration et secrets (sans valeurs sensibles) :

## Taille et architecture
- Complexité : petit / moyen / grand (motif) :
- Structure minimale retenue :
- Frontières métier / I/O :
- Évolutions réellement prévues :
- Patterns ou abstractions nécessaires (justification) :

## Contrats et gestion des erreurs
- Données d'entrée et validations :
- Données de sortie et invariants :
- Erreurs métier et exceptions attendues :
- Traitement des erreurs d'infrastructure :
- Logs et informations sensibles :
- Timeouts, retries et nettoyage des ressources :

## Stratégie de tests
- Tests unitaires (règles métier, limites, erreurs) :
- Tests d'intégration (BD, fichiers, API, services) :
- Fixtures / environnement de test :
- Données de test isolées :
- Cas de non-régression prioritaires :
- Commandes de lancement :
  - Tous : `pytest`
  - Unitaires (si répertoire créé) : `pytest tests/unit`
  - Intégration (si répertoire créé) : `pytest tests/integration`
- Vérifications CI souhaitées :

## Critères de livraison
- [ ] Fonctionnalités attendues vérifiées
- [ ] Code conforme à PEP 8 et lisible
- [ ] Architecture proportionnée ; pas de surarchitecture
- [ ] Gestion d'erreurs explicite et sûre
- [ ] Tests unitaires adaptés au risque exécutés
- [ ] Tests d'intégration nécessaires exécutés en environnement isolé
- [ ] Documentation, configuration et dépendances à jour
- [ ] Limites et contrôles non exécutés signalés

## Décisions et suivi
- Décisions majeures et motifs :
- Risques et limites :
- Prochaines étapes :
