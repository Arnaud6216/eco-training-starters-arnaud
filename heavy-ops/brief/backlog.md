## User story 1 : Éco-guidage et transparence sur les modes de compression (Pré-traitement)

- **Contexte :** En tant qu'utilisateur sur le point de compresser un document, je veux visualiser le bénéfice écologique estimé de chaque niveau de compression (gain de données, émissions évitées), afin de choisir l'option la plus sobre adaptée à mon besoin sans dégrader inutilement mon fichier.
- **Objectif :** Guider au moins 60% des utilisateurs vers le mode de compression éco-responsable grâce à un affichage comparatif clair de l'impact écologique des options.
- **Bonne pratique d'éco-conception ciblée :** _Le service numérique indique-t-il à l'utilisateur que l'utilisation d'une fonctionnalité a des impacts environnementaux importants ?_ (RGESN 4.12).
- **KPI associé :** Taux de sélection du mode sobre éco-recommandé (%).
- **Repo ou écran concerné :** `heavy-ops/frontend` (composant de sélection du niveau de compression / panneau d'options).
- **Critère de réussite :** Chaque profil (Faible, Recommandé, Extrême) affiche son estimation de gain en données et son impact environnemental, avec une mise en avant par défaut de l'option sobre optimale.
- **Niveau de priorité :** Haute.

---

## User story 2 : Bilan d'impact et restitution des ressources économisées (Post-traitement)

- **Contexte :** En tant qu'utilisateur ayant compressé mon document, je veux recevoir un bilan clair de la réduction de poids (Mo) et de l'empreinte carbone évitée lors des futurs transferts et stockages, afin de valoriser ma démarche de sobriété et de prendre conscience de l'impact de mes fichiers numériques.
- **Objectif :** Restituer un rapport d'impact visuel et pédagogique sur 100% des fichiers compressés téléchargés.
- **Bonne pratique d'éco-conception ciblée :** _Le service numérique fournit-il à l'utilisateur un moyen de contrôle sur ses usages afin de suivre et de réduire les impacts environnementaux associés ?_ (RGESN 4.15).
- **KPI associé :** Score de compréhension de l'impact par les utilisateurs et taux de clics sur le bouton d'effacement immédiat.
- **Repo ou écran concerné :** `heavy-ops/frontend` (écran de confirmation et de téléchargement du fichier traité).
- **Critère de réussite :** L'écran de téléchargement affiche une carte d'impact lisible avec : % de réduction de poids, gCO2e estimés épargnés lors d'envois futurs, et un bouton « Supprimer définitivement mon fichier du serveur maintenant ».
- **Niveau de priorité :** Haute.

---

## User story 3 : Purge automatique immédiate et rétention minimale des données

- **Contexte :** En tant qu'administrateur système et éco-concepteur, je veux que les fichiers uploadés et compressés soient purgés dès leur téléchargement par l'utilisateur ou après un délai d'inactivité de 60 minutes, afin de ne pas saturer inutilement les disques des serveurs et d'éliminer la consommation énergétique liée au stockage persistant.
- **Objectif :** Atteindre 0 fichier orphelin conservé au-delà de 1 heure et réduire l'empreinte disque temporaire moyenne de 80%.
- **Bonne pratique d'éco-conception ciblée :** _Le service numérique met-il en place des durées de conservation sur les données et documents en vue de leur suppression ou archivage passé ce délai ?_ (RWEB 0079 / RGESN 7.2).
- **KPI associé :** Volume total de stockage consommé par les fichiers temporaires sur disque serveur (Go).
- **Repo ou écran concerné :** `heavy-ops/backend` (service de gestion des uploads, contrôleur de fichiers et tâche planifiée de purge automatique).
- **Critère de réussite :** Tout fichier téléchargé est supprimé immédiatement du disque ; tout fichier non réclamé sous 60 minutes est automatiquement détruit sans archivage permanent.
- **Niveau de priorité :** Haute.

---

## User story 4 : Modernisation de la stack front-end et suppression du code mort (jQuery / Tippy)

- **Contexte :** En tant qu'utilisateur sur terminal mobile ou ordinateur à puissance modeste, je veux que l'interface se charge en moins de 1,5 seconde, afin d'accéder au service de manière réactive sans surcharger mon processeur ni gaspiller de forfait données.
- **Objectif :** Réduire la taille du bundle JavaScript initial sous 500 Ko et supprimer les librairies obsolètes.
- **Bonne pratique d'éco-conception ciblée :** _Limiter le nombre de CSS / Choisir les technologies les plus adaptées / Minifier les fichiers CSS, JavaScript, HTML et SVG_ (RWEB 0035 / RWEB 0067 / RWEB 0077).
- **KPI associé :** Poids total des ressources JS transférées au chargement (Ko) et Largest Contentful Paint (LCP < 1,5 s).
- **Repo ou écran concerné :** `heavy-ops/frontend` (dépendances du projet, configuration Vite, suppression de jQuery/Tippy au profit d'outils natifs légers).
- **Critère de réussite :** Poids du bundle JavaScript réduit d'au moins 40%, First Contentful Paint < 1 s et absence totale de dépendances legacy inutilisées.
- **Niveau de priorité :** Haute.

---

## User story 5 : Quotas d'usage et garde-fous anti-saturation des serveurs

- **Contexte :** En tant que responsable d'infrastructure, je veux plafonner la taille des fichiers uploadables à 50 Mo et limiter les traitements anonymes à 5 conversions par jour, afin d'empêcher les abus, le scraping sauvage et d'éviter de surdimensionner les serveurs pour absorber des pics de charge évitables.
- **Objectif :** Plafonner la charge CPU instantanée des serveurs sous un seuil nominal de 70% et éviter les traitements disproportionnés.
- **Bonne pratique d'éco-conception ciblée :** _Le service numérique informe-t-il l’utilisateur, avant le transfert, des poids et formats de fichier attendus ?_ (RGESN 4.11 / RWEB 0002).
- **KPI associé :** Pic maximal d'utilisation CPU serveur (%) et nombre de requêtes rejetées en amont.
- **Repo ou écran concerné :** `heavy-ops/backend` (middleware de validation de taille multipart et gestionnaire de rate-limiting par IP/compte).
- **Critère de réussite :** Les fichiers dépassant 50 Mo sont refusés dès l'analyse des en-têtes HTTP (avant transfert complet), avec un message pédagogique expliquant la politique de sobriété.
- **Niveau de priorité :** Moyenne.
