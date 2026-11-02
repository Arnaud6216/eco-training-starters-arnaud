# Cartographie de Cadrage Éco-conception

## Projet Miroir : iLovePDF - heavy-ops

---

### 1. Présentation du service réel et justification du starter

- **Service réel de référence :** **iLovePDF** (outil web bureautique pour l'édition et la compression de fichiers PDF).
- **Catégorie retenue :** **Dashboard / outil métier / SaaS interne**
- **Repo miroir pédagogique associé :** `heavy-ops`

  _iLovePDF_ est un outil SaaS transactionnel à forte intensité de calcul et de flux de données. Le starter `heavy-ops` reproduit exactement ses anti-patterns d'impact : requêtes répétées de vérification d'état (polling), charges lourdes en mémoire, calculs serveurs/clients non filtrés et rétention de données/logs.

---

### 2. Unité Fonctionnelle

> **« Permettre à 1 utilisateur d’uploader un document PDF, d’exécuter la compression via le service et de télécharger le document allégé sur support desktop ou mobile. »**

---

### 3. Frontières du système et composants mobilisés

1. **Équipements terminaux (Client) :** Navigateurs Web (Chrome/Firefox/Safari sur PC ou mobile), mémoire vive (RAM) et CPU.
2. **Réseau :** Infrastructure de télécommunication (4G/5G, Fibre, Box ADSL, serveurs Edge / CDN Cloudflare), requêtes HTTP d'upload et de download.
3. **Infrastructure Serveur & Cloud :** Hébergeur (OVHcloud), serveurs de calcul pour les scripts de compression (Ghostscript / Python / Node), disques de stockage temporaire (fichiers sources et cibles), bases de données et rétention des journaux d'activité (logs).

---

### 4. Problèmes et Mécanismes d'impact identifiés (ACV préalable)

Ces constats s'articulent autour des 4 axes clés du diagnostic initial :

1. **Impact invisible (Choix à l'aveugle) :**
   - Les options de compression (Extrême, Recommandée, Faible) n'affichent absolument pas leur bénéfice écologique ni le gain estimé de bande passante.
   - L'utilisateur n'est pas incité à choisir l'option la plus sobre car il ignore le ratio qualité/sobriété.
2. **Transparence absente (Restitution d'impact nulle) :**
   - Aucune communication sur les performances énergétiques de l'opération, ni sur les gCO2e et Mo économisés lors des téléchargements et envois futurs par e-mail.
3. **Stack obsolète et poids du client web :**
   - Utilisation de bibliothèques vieillissantes et volumineuses (`jQuery`, `Tippy.css`, scripts de tracking tiers).
   - Bundle JavaScript surchargé et non minifié, dégradant la réactivité sur les terminaux plus anciens.
4. **Saturation serveur, réseau et rétention inutile :**
   - _Polling HTTP agressif :_ Le front-end interroge le serveur en boucle toutes les 2 secondes pour vérifier l'avancement de la compression, gaspillant bande passante et CPU.
   - _Rétention prolongée :_ Fichiers sources et compressés restant stockés sur les serveurs cloud au lieu d'une purge immédiate post-téléchargement.
   - _Absence de limitations d'usage :_ Risque de saturation par uploads démesurés (absence de quota journalier ou de rejet précoce d'en-tête).
