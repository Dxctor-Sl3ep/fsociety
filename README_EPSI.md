# Fork EPSI - Perimetre de maintenance

## Contexte

Ce fork part du constat suivant: l'interface actuelle est principalement une interface de commande orientee "menu texte", puissante mais peu ergonomique pour de nouveaux utilisateurs, et pas assez inclusive pour certains contextes d'usage.

Apres exploration du depot amont (sources, README, issues ouvertes, pull requests actives, wiki), ce fork se concentre sur un axe clair:

**ameliorer l'ergonomie et l'accessibilite de l'experience CLI sans changer la vocation du projet (framework de pentest modulaire).**

## Constats issus de l'exploration

1. Navigation CLI peu guidee: la decouverte des commandes repose surtout sur la memoire utilisateur.
2. Sorties terminal parfois denses: lisibilite reduite selon la taille du terminal et le niveau utilisateur.
3. Accessibilite limitee: pas de mode "sortie simple" explicite pour lecteurs d'ecran/outils de transcription.
4. Parcours de prise en main peu progressif: erreurs et invalid commands insuffisamment actionnables.
5. Signaux de friction multi-environnements dans les issues (notamment mobile/Android), suggerant des besoins de robustesse UX.

## Perimetre de maintenance de ce fork

## 1) Ergonomie de navigation (priorite haute)

Objectif: reduire le nombre d'essais/erreurs pour atteindre un outil.

Livrables prevus:
- menu principal avec numerotation optionnelle et navigation clavier plus explicite
- commandes d'aide contextuelle (`help`, `?`) a chaque niveau de menu
- harmonisation des commandes de retour (`back`, `return`) et message de guidance coherent
- affichage "resume" des commandes disponibles apres erreur utilisateur

Critere de succes:
- un utilisateur debutant doit lancer un outil cible en <= 3 interactions dans un parcours guide

## 2) Accessibilite terminal (priorite haute)

Objectif: rendre la sortie lisible et exploitable dans plus de contextes (petits terminaux, lecteurs d'ecran, themes differents).

Livrables prevus:
- mode `--plain` (ou equivalent) sans art ASCII decoratif, sans couleur obligatoire
- mode contraste eleve configurable
- reduction du bruit visuel en tete d'ecran (bannieres optionnelles)
- textes de prompt plus explicites (action attendue + exemples)

Critere de succes:
- l'outil reste utilisable et comprehensible sans couleur ANSI et sans rendu enrichi

## 3) Accessibilite fonctionnelle (priorite moyenne)

Objectif: permettre un usage non interactif pour scripts, CI, et assistance.

Livrables prevus:
- exposition progressive de sous-commandes directes (ex: `fsociety <categorie> <outil> [options]`)
- code de sortie fiable et documente
- format de sortie machine-readable (`--json`) pour certaines commandes d'information

Critere de succes:
- les parcours critiques peuvent etre executes sans navigation de menu interactive

## 4) Qualite des retours utilisateur (priorite moyenne)

Objectif: transformer les erreurs en indications actionnables.

Livrables prevus:
- messages d'erreur normalises avec "cause probable" + "action recommandee"
- suggestions automatiques de commande proche en cas de faute de frappe
- section de depannage orientee UX dans la documentation

Critere de succes:
- baisse du nombre d'erreurs bloquantes sans piste de resolution

## 5) Compatibilite UX sur environnements contraints (priorite moyenne)

Objectif: ameliorer l'experience sur terminaux non standards (ex: mobiles/Termux) quand possible.

Livrables prevus:
- tests manuels de parcours minimaux sur petits terminaux
- adaptation de l'affichage a des largeurs reduites
- documentation claire des limites non supportees

Critere de succes:
- comportement degrade proprement (pas de blocage silencieux, pas d'interface inutilisable)

## Hors-perimetre (pour l'instant)

Ce fork **ne vise pas**, a court terme:
- a ajouter massivement de nouveaux outils de pentest
- a reecrire toute l'architecture interne du framework
- a transformer le projet en application GUI

Le focus est volontairement limite a l'UX CLI et a l'accessibilite.

## Indicateurs de suivi

Pour maintenir ce perimetre, nous suivrons:
- taux d'erreurs de commande non reconnue
- temps moyen pour atteindre un outil cible (tests de parcours)
- nombre de parcours disponibles en mode non interactif
- couverture documentaire des cas d'erreur frequents

## Feuille de route initiale

1. Phase 1: quick wins UX (help contextuel, messages d'erreur utiles, bannieres optionnelles)
2. Phase 2: mode accessibilite (`--plain`, contraste, prompts explicites)
3. Phase 3: parcours non interactifs prioritaires + sorties structurees
4. Phase 4: consolidation multi-environnements et documentation de support

## Engagement de maintenance

Ce perimetre constitue la base de maintenance de ce fork EPSI. Il pourra evoluer selon les retours utilisateurs, les contraintes techniques, et l'avancement du projet, tout en conservant la priorite sur l'ergonomie et l'accessibilite.
