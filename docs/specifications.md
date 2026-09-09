# Spécifications fonctionnelles — Mediatek

## 1. Présentation

Mediatek est une application de gestion de collection personnelle de médias.

La première version de l'application prend en charge deux types de médias :

- les livres ;
- les vinyles.

L'application permet à une personne authentifiée de gérer sa collection, sa wishlist, ses listes personnalisées et ses prêts.

Certaines données peuvent volontairement être rendues accessibles à des personnes non connectées, notamment une collection publique, une wishlist publique ou une liste partagée.

Les fonctionnalités publiques sont toujours accessibles en lecture seule.

---

## 2. Gestion des médias

Un utilisateur authentifié peut gérer les livres et vinyles associés à son compte.

Il peut notamment :

- ajouter un média à sa collection ;
- consulter ses médias ;
- consulter le détail d'un média ;
- modifier les informations personnelles associées à un média ;
- supprimer un média de sa collection ;
- rechercher ses médias ;
- filtrer ses médias ;
- trier ses médias ;
- parcourir les résultats avec pagination ;
- ajouter des tags ;
- marquer certains médias comme favoris ;
- ajouter des informations personnelles telles que des notes.

Les informations propres à l'utilisateur sont distinctes des informations descriptives permettant d'identifier le média.

---

## 3. Collection personnelle

La collection représente les médias possédés par l'utilisateur.

Par défaut, une collection est privée.

L'utilisateur peut décider de rendre sa collection publiquement consultable.

La modification de la visibilité de la collection ne modifie pas automatiquement la visibilité de la wishlist ou des listes personnalisées.

### Consultation de la collection

Un utilisateur authentifié peut :

- consulter l'ensemble de sa collection ;
- rechercher un média ;
- filtrer les résultats ;
- trier les résultats ;
- naviguer entre plusieurs pages de résultats ;
- consulter le détail d'un média.

### Règle anti-doublon

Un même média ne doit pas être enregistré plusieurs fois de manière indépendante pour un même utilisateur lorsque cela représente le même élément de sa collection.

Le système doit privilégier l'évolution de l'état du média plutôt que la création inutile d'un doublon.

---

## 4. Wishlist

La wishlist contient les médias que l'utilisateur souhaite acquérir.

Elle est privée par défaut.

Un utilisateur peut :

- ajouter un média à sa wishlist ;
- retirer un média de sa wishlist ;
- consulter sa wishlist ;
- rechercher un média dans sa wishlist ;
- filtrer les résultats ;
- trier les résultats ;
- utiliser la pagination ;
- définir les informations utiles à son suivi personnel.

### Passage de la wishlist à la collection

Lorsqu'un média présent dans la wishlist est acquis par l'utilisateur, il doit pouvoir passer de l'état `WISHLIST` à l'état `OWNED`.

Cette opération ne doit pas créer un second exemplaire logique du même média pour l'utilisateur.

Les informations pouvant être conservées lors de ce changement d'état doivent l'être lorsque cela est pertinent.

---

## 5. Wishlist publique

L'utilisateur peut choisir de rendre sa wishlist publiquement accessible.

Cette fonctionnalité est notamment destinée à permettre à une autre personne de consulter les souhaits de l'utilisateur afin de lui offrir un cadeau.

La wishlist publique peut notamment présenter :

- les médias souhaités ;
- leur niveau de priorité lorsqu'il est renseigné ;
- un commentaire explicitement destiné à être public lorsqu'il existe.

La wishlist reste privée tant que son propriétaire n'active pas volontairement sa visibilité publique.

La visibilité de la wishlist est indépendante de celle de la collection.

Les combinaisons suivantes doivent donc être possibles :

- collection privée et wishlist privée ;
- collection publique et wishlist privée ;
- collection privée et wishlist publique ;
- collection publique et wishlist publique.

---

## 6. Consultation publique d'une collection

Une personne non authentifiée peut consulter la collection d'un utilisateur uniquement si celui-ci a activé sa visibilité publique.

La consultation publique peut proposer :

- la liste des médias publics ;
- la recherche ;
- les filtres ;
- le tri ;
- la pagination ;
- la consultation du détail public d'un média.

Une personne non authentifiée ne peut effectuer aucune modification.

L'activation de la collection publique ne doit exposer que les informations prévues pour cet usage.

Les informations privées associées aux médias restent invisibles.

---

## 7. Listes personnalisées

Un utilisateur peut créer ses propres listes de médias.

Une liste peut par exemple regrouper des médias selon un thème, une sélection ou un besoin personnel.

L'utilisateur peut :

- créer une liste ;
- lui donner un nom ;
- modifier la liste ;
- supprimer la liste ;
- ajouter des médias ;
- retirer des médias ;
- consulter son contenu.

Une liste personnalisée dispose d'un niveau de visibilité.

Les niveaux prévus sont :

### PRIVATE

La liste est accessible uniquement à son propriétaire.

### PUBLIC

La liste est publiquement consultable.

Elle ne permet aucune modification par les visiteurs.

### SHARED

La liste n'est pas nécessairement publique mais peut être consultée au moyen d'un lien de partage spécifique.

---

## 8. Partage par lien

Une liste peut être partagée au moyen d'un lien.

Le lien doit permettre à une personne non authentifiée de consulter la liste.

Le partage est strictement en lecture seule.

Le lien repose sur un identifiant de partage suffisamment difficile à deviner pour empêcher la découverte triviale des listes partagées.

Le propriétaire doit pouvoir révoquer un partage.

Après révocation, le lien précédemment distribué ne doit plus permettre d'accéder à la liste.

Le système doit également pouvoir prendre en charge une expiration du partage lorsque cette fonctionnalité est activée.

Le partage d'une liste ne doit jamais rendre automatiquement publique :

- la collection complète de l'utilisateur ;
- sa wishlist ;
- ses autres listes ;
- ses données personnelles.

---

## 9. Export des listes

Une liste peut être exportée afin d'être utilisée ou transmise en dehors de Mediatek.

Deux formats sont prévus :

- PDF ;
- Excel au format `.xlsx`.

Les exports doivent contenir uniquement les informations pertinentes pour la liste exportée.

Les données privées qui ne sont pas nécessaires à l'export ne doivent pas apparaître dans le document produit.

---

## 10. Gestion des prêts

Un utilisateur peut suivre les médias qu'il prête.

Les informations relatives aux prêts font partie des données privées de l'utilisateur.

Cela comprend notamment les informations permettant de suivre :

- le média prêté ;
- l'emprunteur ;
- l'état du prêt ;
- l'historique du prêt.

Les informations concernant les prêts ne doivent jamais être exposées :

- dans une collection publique ;
- dans une wishlist publique ;
- dans une liste publique ;
- dans une liste accessible par un lien partagé ;
- dans un export destiné au partage public.

---

## 11. Recherche, filtres, tri et pagination

Les écrans présentant un nombre potentiellement important de médias doivent permettre une navigation adaptée.

Selon le contexte, l'utilisateur peut disposer de :

- recherche ;
- filtres ;
- tri ;
- pagination.

Ces fonctionnalités concernent notamment :

- la collection ;
- la wishlist ;
- leurs versions publiques lorsque cela est pertinent.

Les critères précis seront définis au moment de la conception des interfaces et de l'API.

---

## 12. Visibilité et confidentialité

### Principe de confidentialité par défaut

Toute donnée personnelle ou privée est considérée comme privée par défaut.

Une information ne devient publique que lorsqu'une fonctionnalité prévue à cet effet est explicitement activée par son propriétaire.

### Réglages indépendants

Les niveaux de visibilité de la collection, de la wishlist et des listes personnalisées sont indépendants.

La modification de l'un d'eux ne doit pas modifier automatiquement les autres.

### Lecture seule des contenus publics

Une personne non authentifiée peut uniquement consulter les contenus auxquels elle a accès.

Elle ne peut jamais :

- ajouter un média ;
- modifier un média ;
- supprimer un média ;
- modifier une liste ;
- modifier une wishlist ;
- modifier les informations d'un autre utilisateur.

### Données strictement privées

Les données sensibles ou personnelles ne doivent pas être exposées dans les représentations publiques.

Cela concerne notamment :

- l'adresse e-mail de l'utilisateur ;
- les prix ou informations d'achat considérés comme privés ;
- l'emplacement personnel d'un média ;
- les notes privées ;
- les informations de prêt ;
- les informations concernant les emprunteurs ;
- l'historique des prêts.

### Séparation entre données privées et données publiques

Les informations utilisées dans les espaces authentifiés peuvent être plus complètes que celles présentées dans les espaces publics.

Une représentation publique ne doit contenir que les données explicitement autorisées pour cet usage.

Cette règle s'applique également aux exports et aux données accessibles par un lien de partage.

---

## 13. Règles métier principales

1. Les collections sont privées par défaut.

2. Les wishlists sont privées par défaut.

3. La visibilité de la collection et celle de la wishlist sont indépendantes.

4. Une personne non authentifiée dispose uniquement d'un accès en lecture aux contenus publics ou partagés.

5. Un lien de partage doit pouvoir être révoqué par son propriétaire.

6. Un lien révoqué ne permet plus d'accéder à son contenu.

7. Les informations relatives aux prêts restent toujours privées.

8. Les données privées ne doivent jamais apparaître accidentellement dans une représentation publique ou un export public.

9. Un même média ne doit pas être dupliqué inutilement pour un même utilisateur.

10. Le passage d'un média de `WISHLIST` à `OWNED` doit être traité comme une évolution de son état lorsque le média correspond au même élément.

11. Le partage d'une liste ne modifie pas la visibilité des autres données de l'utilisateur.

12. Les contenus publics et partagés sont consultables sans permettre de modification.

---

## 14. Hors périmètre de ce document

Ce document définit le comportement fonctionnel de Mediatek.

Il ne définit pas encore :

- le modèle de base de données ;
- les entités backend ;
- les DTO ;
- les endpoints de l'API ;
- la structure des composants frontend ;
- les bibliothèques utilisées ;
- l'architecture technique détaillée ;
- les mécanismes précis d'authentification ;
- le format interne des tokens de partage.

Ces décisions sont documentées séparément lors de la conception technique.
