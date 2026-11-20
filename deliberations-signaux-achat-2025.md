# Ce que les délibérations disent des achats à venir

*Mesure sur les délibérations 2025 des organismes adhérents de Mégalis Bretagne. Victor Lavolé, Temi, novembre 2026.*

Avant qu'un avis de marché paraisse, l'achat passe souvent par l'assemblée délibérante : on vote une enveloppe, on lance des études, on demande une subvention, on inscrit l'opération au budget. Ces actes sont publics. Cette note mesure la part des délibérations qui portent un tel signal.

## La source

Les [délibérations des organismes adhérents de Mégalis Bretagne](https://www.data.gouv.fr/datasets/60645c94e2bfd21cdc16c0be/), publiées sur data.gouv.fr au format SCDL délibérations, sous Licence Ouverte 2.0. Fichier de l'année 2025, lu en novembre 2026. Le fichier est régénéré chaque nuit : dans sa version du 9 novembre 2026, il compte 125 102 délibérations, cinq de plus que la base sur laquelle la mesure a été faite. L'écart ne change aucune part au dixième de point.

## La méthode

| Étape | 2025 |
|---|---|
| Délibérations de l'année | 125 097 |
| Avec un lien vers le PDF de l'acte | 113 533 |
| Lisibles, hors matières écartées | 98 019 |
| Textes lus dans l'échantillon (300 caractères au moins) | 2 662 |

- **Les matières écartées.** Les actes sur la fonction publique (matières 4.x), les assemblées (5.2) et l'aide sociale (8.2) ne sont jamais téléchargés : ils concernent des personnes.
- **L'échantillon.** Les PDF sont tirés au hasard, avec une graine fixe, dans chaque groupe de matières. Les résultats sont ensuite repondérés selon le poids réel de chaque groupe.
- **Les scans.** Ils sont lus par reconnaissance de caractères (OCR). En 2025, 1 683 des 3 016 PDF lus étaient des scans sans couche texte.
- **Le classement.** Chaque texte est rangé dans zéro, une ou plusieurs des 13 familles ci-dessous, par des expressions déterministes. Aucun modèle d'IA n'intervient. Les expressions elles-mêmes ne sont pas publiées.

## Les résultats

Part des textes lus qui portent chaque signal. Une délibération peut en porter plusieurs.

| Signal | Part en 2025 |
|---|---|
| Lancement d'une consultation | 2,3 % |
| Estimation préalable | 5,8 % |
| Phases de maîtrise d'œuvre | 2,0 % |
| Études, assistance à maîtrise d'ouvrage | 2,6 % |
| Gouvernance du projet | 3,4 % |
| Financement, demande de subvention | 12,3 % |
| Budget d'investissement | 12,1 % |
| Foncier préalable | 3,9 % |
| **Au moins un des huit signaux ci-dessus (signal amont)** | **34,0 %** |
| Achat sous les seuils | 8,4 % |
| Attribution d'un marché | 3,4 % |
| Exécution, avenant | 12,0 % |
| Délégation de service public, concession | 1,6 % |
| Groupement de commandes | 1,3 % |
| Au moins un montant en euros cité | 38,7 % |

Dans les délibérations classées en matière « commande publique » (330 textes lus), 53,3 % portent un signal amont, 46,1 % parlent d'exécution ou d'avenant, 40,3 % d'un achat sous les seuils et 18,8 % d'une attribution.

La même mesure sur 2022 donne 31,9 % de textes avec un signal amont. L'échantillon de 2022 est plus petit (1 378 textes) et ne couvre pas le groupe des actes budgétaires : la comparaison ne vaut que pour l'ordre de grandeur.

## Ce qu'on en retient

- **Une délibération lue sur trois prépare, finance ou annonce un projet avant tout appel d'offres.** Une commune qui vote des études de maîtrise d'œuvre pour une école prépare des marchés de travaux, si le projet aboutit.
- **Les achats sous les seuils se voient dans les délibérations** (8,4 % des textes), alors qu'ils ne donnent pas toujours lieu à un avis publié.
- **Un signal n'est pas une certitude.** Une étude peut ne jamais déboucher sur un marché.

## Les limites

- **La couverture.** Bretagne seulement, et seulement les organismes qui publient par Mégalis.
- **L'échantillon.** Il couvre 2,7 % des actes lisibles. Dans un groupe de matières où moins de 100 textes ont été lus, les parts sont bruitées.
- **La détection.** Une expression repère une mention, pas une intention.
- **Les actes sans document.** 11 564 délibérations de 2025 n'ont aucun lien vers un fichier dans le jeu : il n'y a rien à lire ni à passer à l'OCR. Seul leur objet est connu, une phrase de 52 caractères en médiane, trop courte pour cette mesure.

## Le code

La lecture du fichier, les matières écartées et la lecture des PDF, par leur couche texte ou par OCR, sont publiées dans [scdl-collectivites](https://github.com/V08-ai/scdl-collectivites), avec leurs tests. Le classement en familles de signaux ne l'est pas.

## Réutiliser cette note

Cette note est publiée sous licence [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.fr). Les chiffres viennent d'un jeu sous Licence Ouverte 2.0 : citer « Délibérations des organismes adhérents de Mégalis Bretagne, data.gouv.fr ».

Une erreur, une question : ouvrez une issue sur ce dépôt ou écrivez à contact@temiapp.com.
