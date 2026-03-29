# Analyse de la relation entre le niveau d'étude attendu et la difficulté à recruter dans les emplois de la transition écologique

Ce notebook poursuit le travail d'analyse entreprit dans le projet précédent "https://github.com/clementfays/projet-metiers-verts".
Dans ce dernier, nous avions identifié un excès de difficulté perçue par les employeurs à pourvoir les postes dits "verdissants", et qu'il existait des disparités régionales fortes quant à cette difficulté.

Ici, nous entreprenons l'inverstigation des facteurs explicatifs de ces difficultés de recrutement. Beaucoup de variables sont candidates pour expliquer ce phénomène, mais ici nous nous concentrerons sur le niveau d'étude attendu par métier. Le niveau d'étude attendu par métier est obtenu grâce à l'exploitation des offres d'emplois publiées sur France Travail en 2025, consultées grâce à l'API de ce dernier.

**L'objectif principal de l'analyse est de valider une des trois hypthèses concurrentese suivantes**

**- H1 => Les emplois les plus qualifiés sont les plus difficiles à pourvoir.** Cela pourrait s'expliquer par un deficit d'offre de formations supérieures dans les spécialités liées à la transition écologique en comparaison à la demande émanant du marché du travail

**- H2 => Les emplois les moins qualifiés sont les plus difficiles à pourvoir.** Cela pourrait s'expliquer par l'attrait des emplois de la transition écologique auprès de la main d'oeuvre qualifiée, ou à l'inverse par le deficit d'offre de formation professionnelle menant aux emplois les moins qualifiés

**- H3 => Pas de d'impact du niveau de diplôme attendu sur la difficulté à recruter.**

Nous chercherons ensuite à déterminer si l'hypothèse retenu s'applique également aux emplois sans lien avec la transition écologique.

## Données utilisées

- Les données concernant de l'enquête BMO 2025 sont utilisées pour calculer l'indicateur *difficulté à recruter* pour chaque famille professionnelle. Elles sont accessibles via ce lien : https://www.data.gouv.fr/datasets/enquete-besoins-en-main-doeuvre-bmo
- L'API *Offres d'emplois v2* de France Travail a été utilisé pour recenser les offres d'emploi en 2025, et identifier le niveau d'étude attendu pour chacunes d'entre elles.
- La classification des métiers verts et verdissants provient du Ministère de l'Écologie (ONEMEV) - https://www.ecologie.gouv.fr/sites/default/files/documents/Onemev_emploi_metiers.pdf

## Définitions

**- Métiers verts** - métier dont la finalité et/ou les compétences mises en œuvre contribuent à mesurer, prévenir, maîtriser, corriger les impacts négatifs et les dommages sur l’environnement

**- Métiers verdissants** - métier dont la finalité n’est pas environnementale, mais qui intègre de nouvelles « briques de compétence » pour prendre en compte de façon significative et quantifiable la dimension environnementale dans le geste métier

# Conclusion

Grâce à l'exploitation et la mise en concordance de plusieurs sources de données, nous avons ici pu réaliser une rapide analyse de la relation entre niveau d'étude attendu et difficulté à recruter sur les métiers de la transition écologiques.
**Les résultats obtenus ici permettent d'observer que les emplois *verts* semblent plus difficiles à pourvoir lorsqu'ils recquièrent un niveau d'étude faible. Ce constat ne s'applique pas aux autres emplois, ce qui suggère que des mécanismes propres aux métiers de la transition sont à l'oeuvre.**

**Deux hypothèses de travail sont à explorer :**

*- Les métiers hautements qualifiés dans le domaine de la transition sont particulièrement attractifs.* Cela s'expliquerait notamment par la "quête de sens" parmi les jeunes diplomés, qui valorisent relativement plus les métiers à fort impact social - définition incluant souvent les métiers à caractère écologique.

*- Les métiers faiblement qualifiés dans le domaine de la transition sont particulièrement inattractifs.* Cela pourrait s'expliquer par la pénibilité et le manque de reconnaissance économique et social associé à ces emplois (beaucoup d'emplois dans les secteurs de la construction, de l'entretion/rénovation, du transport routier de passagers).

**Des analyses complémentaires seraient nécessaires. Des exmples de perspectives sont :**

- Introduction de nouvelles variables de contrôle dans le modèle régression pour valider la causation entre niveau de diplôme et difficulté de recrutement

- Analyse temporelle pour valider la tendance observée sur un temps plus long

- L'analyse gagnerait également en précision si l'enquête BMO utilisait la nomenclature ROME, plus granulaire que les FAP et évitant ainsi d'avoir à matcher certaines catégories de manière semi-arbitraire.

**Recommandations**

Du fait des limitations de l'analyse, il est difficile de fournir des recommandations à ce stade. Toutefois, si le phénomène observé venait à être validé par des analyses approfondies, les recommandations suivantes pourraient être émises :

- Besoin de renforcer l'attractivité des métiers les moins qualifiés qui contribuent de manière significative à la transition écologiques du pays (secteurs de la construction, de la rénovation énergétique, des transports en commun). Par exemple grâce à un système de "primes écologies", similaire au dispositif de Prime Ségur du secteur de la santé.

- Besoin de renforcer les capacités de formation professionnelles des filières de la transition écologiques, par exemple en créant de nouveaux établissements de foramtion initiale ou en renforcant les dispositifs actuels de formation continue.


## Difficultés notables et limites des données employées

- La nomenclature d'emplois des deux jeux de données est différente. Les offres d'emploi recensées par France Travail sont rattachées à des codes ROME (Répertoire opérationnel des métiers et des emplois), alors que l'enquête BMO 2025 utilise les familles professionnelles (FAP 2021). Ces nomenclatures ne correspondant pas directement, le travail de matching a nécessité de faire des choix limitant la précision du travail d'analyse.
- Seulement un quart environ des offres d'emploi recensées sur France Travail avaient renseigné le champ formation, ce qui indique un potentiel risque de biais
- L'indicateur  *difficulté à recruter* est basé sur du déclaratif de la part des entreprises — il reflète la perception des employeurs, pas une mesure objective de la tension

  
## Structure de l'analyse


- Accès à l'API de France travail et exploration des offres
- Calcul de niveau d'étude attendu moyen par code ROME
- Import de la liste des codes ROME *verts* et *verdissants* (générée par ailleurs)
- Correspondance des ROME avec la nomenclature FAP 2021
- Calcul du niveau d'étude moyen attendu par FAP 2021 (moyenne pondérée des ROME par FAP)
- Chargement du BMO 2025 et calcul du taux de difficulté par FAP
- Création d'un dataframe unique incluant les niveaux d'études attendus et les taux de difficulté par FAP
- Analyse de la corrélation entre le niveau d'étude sur le taux de difficulté par FAP en 2025, sur les métiers verts et verdissants
- Reproduction des étapes précédentes  sur les métiers non verts/verdissants (grand échantillon), dans un but de comparaison



