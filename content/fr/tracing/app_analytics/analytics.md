---
title: Visualiser les analyses
kind: documentation
description: Analyse des données de votre APM avec une cardinalité infinie
aliases:
  - /fr/tracing/trace_search_analytics/analytics
  - /fr/tracing/analytics
  - /fr/tracing/visualization/analytics
  - /fr/tracing/trace_search_and_analytics/analytics/
further_reading:
  - link: tracing/setup/
    tag: Documentation
    text: Découvrir comment configurer le tracing d'APM avec votre application
  - link: tracing/visualization/services_list/
    tag: Documentation
    text: Découvrir la liste des services transmettant des données à Datadog
  - link: tracing/visualization/service
    tag: Documentation
    text: En savoir plus sur les services dans Datadog
  - link: tracing/visualization/resource
    tag: Documentation
    text: Plonger au cœur des traces et des performances de vos ressources
  - link: tracing/visualization/trace
    tag: Documentation
    text: Comprendre comment lire une trace Datadog
  - link: tracing/app_analytics/search
    tag: Documentation
    text: Recherche globale sur toutes vos traces avec des tags
---
## Overview

Utilisez la vue [App Analytics][1] pour filtrer les métriques de performances des applications et les [spans analysées](#spans-analysees) en fonction de tags définis par l'utilisateur. Ces fonctionnalités vous permettent de plonger au cœur des requêtes Web transitant par votre service.

La fonction App Analytics peut être activée pour des [services][2] APM et des hosts spécifiques. Lorsqu'elle est activée pour un service, toutes ses spans analysées sont transmises à Datadog.

Les services en aval comme les bases de données et les couches du cache ne font pas partie des services disponibles (car ils ne génèrent pas leurs propres traces), mais les informations les concernant sont récupérées par les services de haut niveau qui les appellent.

Utilisez la vue App Analytics pour :

* [Interagir avec l'intervalle](#time-range)
* [Afficher des listes de traces](#trace-stream)
* [Filtrer votre flux de traces en appliquant des facettes](#facets)
* [Saisir des requêtes de recherche](#search-bar)

## Spans analysées

Lorsqu'une requête parvient à un [service][2] (par exemple, un serveur Web ou une base de données), l'Agent Datadog crée une span analysée. Il s'agit d'un enregistrement de la requête qui inclut sa durée, le code de réponse et toutes les [métadonnées personnalisées][3].
Une span analysée correspond à une span unique accompagnée de métadonnées concernant la requête gérée. Pour chaque service qui reçoit une requête, l'Agent crée une span analysée. Si une requête transite par un service Web, un service de référencement et un service de base de données, cette requête générera 3 spans analysées. Pour réduire le nombre de spans analysées générées, [activez ou désactivez explicitement toute collecte de spans analysées pour un service spécifique][4].

Pour commencer à recueillir des spans analysées, [activez la fonction App Analytics pour vos services][5].

### Traces complètes

Lorsque l'option Complete traces est sélectionnée, les spans analysées incluses dans le flux de traces disposent d'une trace, ce qui vous permet d'afficher la [trace][6] complète avec l'intégralité de la [span][7] associée.

## Requête App Analytics

Créez une requête pour contrôler les données affichées dans votre analyse App Analytics :

1. Choisissez la métrique `Duration` ou une [facette][1] à analyser. La métrique `Duration` vous permet de choisir la fonction d'agrégation, tandis que la [facette][1] affiche le nombre de valeurs uniques.

    {{< img src="tracing/app_analytics/analytics/choose_measure_facet.png" alt="choisir une mesure ou une facette" responsive="true" style="width:50%;">}}

2. Sélectionnez la fonction d'agrégation pour la métrique `Duration` :

    {{< img src="tracing/app_analytics/analytics/agg_function.png" alt="fonction d'agrégation" responsive="true" style="width:50%;">}}

3. Utilisez un [tag][2] ou une [facette][1] pour fractionner votre analyse.

    {{< img src="tracing/app_analytics/analytics/split_by.png" alt="fractionnement" responsive="true" style="width:50%;">}}

4. Choisissez d'afficher les *X* valeurs les plus **élevées** ou **faibles** en fonction de la [facette][1] ou de la `Duration` sélectionnée.

    {{< img src="tracing/app_analytics/analytics/top_bottom_button.png" alt="bouton top/bottom" responsive="true" style="width:20%;">}}

5. Sélectionnez les laps de temps de l'analyse.
  Le changement de l'intervalle de temps global modifie la liste des laps de temps disponibles.

    {{< img src="tracing/app_analytics/analytics/timesteps.png" alt="Intervalle" responsive="true" style="width:30%;">}}

## Visualisations

Sélectionnez un type de visualisation App Analytics à l'aide du sélecteur d'analyse.

Visualisations disponibles :

* [Série temporelle](#timeseries)
* [Top List (Valeurs les plus élevées)](#top-list)
* [Table (Tableau)](#table)

### Série temporelle

Visualisez l'évolution de la métrique `Duration` (ou d'une [facette][1] correspondant à un nombre unique de valeurs) pour un intervalle donné. Vous pouvez également fractionner le graphique en utilisant une [facette][1] disponible.

L'analyse App Analytics avec une série temporelle suivante illustre : l'évolution de la **durée** au **pc99** (99e centile) toutes les **5 minutes** pour chaque **service**.

{{< img src="tracing/app_analytics/analytics/timeserie_example.png" alt="exemple de série temporelle" responsive="true" style="width:90%;">}}

### Top List (Valeurs les plus élevées)

Visualisez les valeurs les plus élevées d'une [facette][1] en fonction de leur métrique `Duration` (ou d'une [facette][1] correspondant à un nombre unique de valeurs) :

L'analyse App Analytics suivante avec une Top List illustre :
la **durée** au **pc99** (99e centile) la plus élevée d'un **service**

{{< img src="tracing/app_analytics/analytics/top_list_example.png" alt="exemple de top list" responsive="true" style="width:90%;">}}

### Table (Tableau)

Visualisez la liste des valeurs les plus élevées d'une [facette][1] en fonction de la [mesure][2] choisie (la première mesure que vous choisissez dans la liste), et affichez la valeur des autres mesures dans la liste. Mettez à jour la requête de recherche ou explorez les logs correspondant à l'une des dimensions.

* Lorsque plusieurs dimensions sont définies, les valeurs les plus élevées sont déterminées en fonction de la première dimension, puis de la seconde dans la fourchette des valeurs les plus élevées de la première dimension, puis de la troisième dans la fourchette des valeurs les plus élevées de la seconde dimension.
* Lorsque plusieurs mesures sont définies, les valeurs les plus élevées ou faibles sont déterminées en fonction de la première mesure.
* Le sous-total peut différer de la somme réelle des valeurs au sein d'un groupe, étant donné qu'un seul sous-ensemble (celui des valeurs les plus élevées ou des valeurs les plus faibles) s'affiche. Les événements associés à une valeur nulle ou vide pour cette dimension ne s'affichent pas en tant que sous-groupe.

 **Remarque** : la visualisation d'une seule mesure et d'une seule dimension sous forme de tableau est identique à celle d'une top list. Seul l'affichage diffère.

 L'analyse de logs avec un tableau suivante illustre l'évolution des **premiers codes de statut** en fonction de leur **débit**, ainsi que le nombre moyen d'**IP client** uniques au cours des 15 dernières minutes :

{{< img src="tracing/app_analytics/analytics/trace_table_example.png" alt="exemple de top list" responsive="true" style="width:90%;">}}

## Traces associées

Sélectionnez une section du graphique ou cliquez dessus pour l'agrandir ou consulter la liste des [traces][3] correspondant à votre sélection :

{{< img src="tracing/app_analytics/analytics/view_traces.png" alt="visualiser les traces" responsive="true" style="width:40%;">}}

## Export

{{< img src="tracing/app_analytics/analytics/export_button.png" alt="bouton d'exportation de votre analyse" responsive="true" style="width:40%;">}}

Exportez votre analyse App Analytics :

* Pour créer un [monitor d'APM][4]
    (cette fonctionnalité n'est pas encore disponible).
* Vers un [timeboard][5] existant.
    Cette fonctionnalité est en version bêta : [contactez l'assistance Datadog][6] afin de l'activer pour votre organisation.

## Traces dans les dashboards

Exportez votre analyse [App Analytics][6] depuis la recherche de traces ou créez-en une directement dans votre [dashboard][7] aux côtés des métriques et des logs.

[En savoir plus sur le widget Série temporelle][9]

## Pour aller plus loin

{{< partial name="whats-next/whats-next.html" >}}

[1]: /fr/tracing/advanced/search/#facets
[2]: /fr/tracing/advanced/search/#measures
[3]: /fr/tracing/visualization/#trace
[4]: /fr/monitors/monitor_types/apm
[5]: /fr/graphing/dashboards/timeboard
[6]: /fr/help
[7]: /fr/graphing/widgets/timeseries
[8]: /fr/graphing/dashboards
[9]: /fr/graphing/widgets/timeseries