---
title: "Nouveautés de Flows for APEX 21.1"
last_modified_at: 2021-09-27T10:00:00+02:00
toc: true
categories:
  - Oracle APEX
  - Flows for APEX
tags:
  - workflow
  - APEX
  - bpmn
  - En français
---

La version 21.1 de Flows for APEX a été publié le vendredi 24 septembre, il est maintenant temps de voir quels sont les principaux changements et nouvelles fonctionnalités apportées par cette version majeure (la liste complète est disponible <a href="https://github.com/mt-ag/apex-flowsforapex/blob/v21.1/changelog.md">ici</a>).
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Here it is: Flows for APEX 21.1! Thanks to <a href="https://twitter.com/commi235">@commi235</a> <a href="https://twitter.com/FlowquestR">@FlowquestR</a> <a href="https://twitter.com/moreaux_louis">@moreaux_louis</a> <a href="https://twitter.com/dennisamthor">@dennisamthor</a> as well as our beta testers for making this possible. <a href="flowsforapex.mt-ag.com">flowsforapex.mt-ag.com</a></p>&mdash; Niels de Brujin (@nielsdb) <a href="https://twitter.com/nielsdb/status/1441368868614664194">September 24, 2021</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

#### Expressions de variables
Précédemment, pour définir des variables de processus, vous deviez utiliser l'api PL/SQL ou les plug-ins. La version 21.1, introduit une nouvelle fonctionalité : les expressions de variables. 
Il suffit de cliquer sur une activité dans le modeleur et sur le panneau de propriétés, un nouvel onglet vous permet de définir une ou plusieurs expression(s) de la variable(s).

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/varExpression.apng){: .align-center}

Une expression de variable peut être définit en utilisant :
- Une valeur statique
- La valeur d'une autre variable de processus
- Une requête SQL retournant une valeur
- Une requête SQL retournant plusieurs valeurs (liste séparée par des deux-points)
- Une expression PL/SQL
- Une fonction PL/SQL

Un cas d'usage de cette fonctionnalité est, par exemple, la possibilité de définir la route à prendre pour une passerelle en se basant des données présentes dans la base de données.

#### Une meilleure gestion des erreurs
Un grand changement dans cette version est que le système de transaction a été complètement réécrit. Le résultat est que désormais chaque étape d'un processus utilise une transaction de base de données séparée. Le principal bénéfice est la gestion des erreurs qui en résulte. Le moteur de processus est maintenant capable de capturer les erreurs, de les enregistrer et d'indiquer que l'étape ainsi que l'instance sont en erreur. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/errorHandling.apng){: .align-center}

#### Améliorations de l'éditeur de diagramme
L'éditeur BPMN a été amélioré en rendant le panneau de propriétés extensible ainsi que par la prise en charge des raccourcis claviers permettant le copier/coller, la suppression et les opérations annuler/rétablir.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/keyboardShortcuts.apng){: .align-center}

#### Plug-ins
Dans la version 5.1.2, nous avons commencé à travailler sur des plug-ins pour Oracle APEX afin de faciliter l'intégration de Flows for APEX dans vos applications. Dans cette nouvelle version, 3 nouveaux plug-ins font partis de la distribution :
- Manage Flow Instance
- Manage Flow Instance Step
- Manage Flow Instance Variables

#### Export/Import multiples des modèles
Une fonctionnalité pensée pour faciliter vos déploiements de modèles est l'export/import en 1 clic. Sur la page de gestion des modèles, sélectionnez les modèles à exporter puis utilisez le menu d'en-tête et choisissez Exporter. Vous pourrez alors choisir entre l'export au format BPMN ou scripts SQL. Le résultat de cet export est une archive zip contenant les modèles sélectionnés. Pour la version script SQL, vous n'aurez qu'à exécuter le script import.sql pour réaliser l'import. La version BPMN permet elle de récupérer l'ensemble des diagrammes au format BPMN ainsi qu'un fichier import.json contenant les attributs de chaque modèle (nom, version, category). Cette archive peut être utilisée dans la fenêtre d'import pour importer l'ensemble des modèles en 1 clic, il suffit de choisir l'option Plusieurs modèles.
