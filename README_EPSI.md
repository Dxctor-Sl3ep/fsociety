# fsociety - README EPSI

## Objectif du fork

Ce fork conserve la philosophie de `fsociety` (framework modulaire de lancement d'outils de pentest) mais se concentre sur un axe prioritaire: **rendre l'interface CLI plus ergonomique et plus accessible** pour un usage quotidien (apprentissage, labo, audit interne autorise).

L'objectif n'est pas de remplacer les outils existants, mais d'ameliorer l'experience utilisateur autour de leur decouverte, installation et execution.

## Constat apres exploration du projet source

Exploration effectuee sur:

- code source (menus, modules, configuration)
- documentation principale (`README.md`, `PACKAGES.md`, `CHANGELOG.md`)
- pages GitHub publiques (issues, pull requests, wiki)

Points observes:

- l'entree CLI est minimaliste (`-i` et `-s`) et le reste se fait via navigation interactive;
- l'interface est volontairement "terminal old-school" (banniere ASCII, listes textuelles), efficace mais peu guidee;
- l'onboarding depend fortement de la connaissance prealable des outils tiers;
- plusieurs signaux de tickets orientent vers des problemes d'execution/environnement (notamment mobile/Android), ce qui renforce le besoin de messages plus explicites et d'un parcours utilisateur plus robuste;
- le wiki ne constitue pas aujourd'hui un parcours tutoriel structure pour demarrer rapidement.

## Perimetre de maintenance (v1)

Ce document definit le perimetre de maintenance de ce fork. Il pourra evoluer, mais sert de contrat initial.

### 1) Ergonomie CLI

Ameliorations ciblees:

- clarifier les invites (`prompt`) et les options disponibles a chaque etape;
- afficher des messages d'erreur actionnables (cause probable + action conseillee);
- proposer des raccourcis de navigation coherents (`back`, `return`, `exit`, aide contextuelle);
- ameliorer le flux d'installation des outils (pre-check, confirmation claire, retour de statut lisible);
- standardiser les ecrans de confirmation et de fin d'execution.

Critere d'acceptation v1:

- un utilisateur debutant doit pouvoir lancer un outil en moins de 3 minutes sans lire le code;
- chaque erreur courante doit proposer au moins une action concrete de remediation.

### 2) Accessibilite

Ameliorations ciblees:

- reduire la dependance a la couleur seule pour comprendre l'etat d'une action;
- garantir des textes lisibles en terminaux a contraste faible;
- limiter les surcharges visuelles (bannieres/envahissement de sortie) quand non necessaire;
- preparer un mode d'affichage "simple" (sortie compacte, verbosite controlee) pour lecteurs d'ecran et petits terminaux;
- harmoniser les messages pour qu'ils restent comprehensibles hors contexte visuel.

Critere d'acceptation v1:

- tout message critique est comprehensible sans interpretation des couleurs;
- l'utilisateur peut obtenir une sortie concise et repetitive pour les usages scripts/lab.

### 3) Documentation orientee usage

Ameliorations ciblees:

- produire un tutoriel de prise en main (ce document);
- documenter les "capabilities" par module avec exemples d'utilisation;
- expliciter les pre-requis OS/outils pour eviter les echecs silencieux;
- formaliser les limites (ce que ce fork ne couvre pas).

Critere d'acceptation v1:

- la documentation permet de comprendre le workflow sans consulter le code source.

## Hors perimetre (v1)

Ce fork **ne** vise pas, dans cette premiere phase, a:

- reecrire tous les wrappers d'outils tiers;
- garantir l'execution sur Android/Termux;
- transformer fsociety en interface graphique (GUI);
- ajouter massivement de nouveaux outils avant stabilisation ergonomique.

## Tutoriel d'utilisation des capabilities

Important: utiliser uniquement dans un cadre legal, autorise et controle.

### Installation rapide

```bash
pip install fsociety
```

Ou en developpement:

```bash
git clone https://github.com/fsociety-team/fsociety.git
cd fsociety
pip install -e ".[dev]"
```

### Demarrer

```bash
fsociety
```

Au premier lancement:

1. accepter les termes;
2. choisir un module principal dans le menu;
3. choisir une capability (outil) dans le module;
4. suivre les invites (host, domaine, URL, options);
5. revenir avec `back`/`return` ou quitter avec `exit`.

### Commandes globales utiles

```bash
fsociety -h
fsociety -i
fsociety -s
```

- `-h`: aide generale
- `-i`: informations systeme et configuration fsociety
- `-s`: proposition d'un outil (ouvre la creation d'issue GitHub)

## Capabilities par module

### Information Gathering

Capabilities disponibles:

- `sqlmap`
- `striker`
- `sublist3r`
- `sherlock`
- `s3scanner`
- `gitgraber`
- `hydrarecon`

Exemple rapide (subdomain enum avec Sublist3r):

1. lancer `fsociety`
2. entrer `information_gathering`
3. entrer `sublist3r`
4. saisir le domaine cible

Le wrapper peut installer/mettre a jour le depot de l'outil avant execution.

### Networking

Capabilities disponibles:

- `nmap`
- `bettercap`

Exemple rapide (scan Nmap preset):

1. `fsociety`
2. `networking`
3. `nmap`
4. saisir un host
5. choisir un preset (`simple`, `common_ports`, `aggressive_scan`, etc.)

Le module Nmap propose des presets predefinis pour accelerer l'usage.

### Web Apps

Capabilities disponibles:

- `xsstrike`
- `photon`

Exemple rapide (XSStrike):

1. `fsociety`
2. `web_apps`
3. `xsstrike`
4. saisir une URL
5. confirmer options (`crawl`, `params`)

### Passwords

Capabilities disponibles:

- `cupp`
- `cr3dov3r`
- `hash_buster`
- `changeme`
- `traitor`

Exemple rapide (CUPP):

1. `fsociety`
2. `passwords`
3. `cupp`
4. suivre l'assistant interactif

### Obfuscation

Capabilities disponibles:

- `cuteit`

Exemple rapide:

1. `fsociety`
2. `obfuscation`
3. `cuteit`
4. entrer une IP

### Utilities

Capabilities disponibles:

- `host2ip`
- `base64_decode`
- `spawn_shell`
- `suggest_tool`
- `print_contributors`

Exemple rapide (host2ip):

1. `fsociety`
2. `utilities`
3. `host2ip`
4. saisir un host

## Workflow utilisateur recommande

Pour une experience plus propre et reproductible:

1. preparer un environnement dedie (venv);
2. verifier les dependances systeme (ex: nmap installe localement);
3. lancer une capability a la fois;
4. conserver les sorties importantes dans des notes de mission;
5. revenir au menu principal avec `back` avant de changer de module.

## Plan d'evolution du fork

### Milestone M1 - Ergonomie de base

- prompts et erreurs plus explicites
- feedback de statut installation/execution
- parcours debutant documente de bout en bout

### Milestone M2 - Accessibilite CLI

- mode d'affichage compact
- messages sans dependance couleur
- harmonisation des libelles et aides contextuelles

### Milestone M3 - Fiabilisation des parcours

- reduction des impasses interactives
- meilleure gestion des interruptions clavier
- verification de coherence des commandes entre modules

## Indicateurs de suivi

Pour piloter ce perimetre:

- temps moyen de premiere execution reussie;
- nombre d'erreurs non actionnables remontees;
- couverture de documentation des capabilities;
- taux de succes sur environnements desktop cibles (Linux/macOS/Windows).

## Ethique et conformite

Ce fork reste destine a l'apprentissage securite, au test autorise et a la recherche defensive. Toute utilisation hors cadre legal est exclue.

