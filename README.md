# Application de restauration rapide SushiFast

## Ressources pour le projet

[SushiFast](https://slam-vinci-melun.github.io/sio22/phase2/SP2-Angular-2021_22.pdf)

## Sommaire

### Premieres Partie 

* Présentation

* Attendus fonctionnels

    * Affichage de la liste des plateaux de Sushi
    * Possibilité de voir le détail d’un plateau
    * Achat d’un ou plusieurs plateaux sous la forme d’un panier
    * Visualisation des commandes sauvegardées localement
    * Page spécifique concernant la mise en place du RGPD

* Attendus techniques

    * Interrogation d’une API existante via la saisie d’informations dans un formulaire
    * Définition d’une entité objet pour la représentation des données
    * Affichage de la liste des objets, accès au détail, calcul de commande
    * Sauvegarde locale côté client (LocalStorage)
    * Prise en compte d’au moins 2 Evil User Stories
    * Test unitaire (au moins 3)

* Analyse de la demande

* Ce qui est attendu

### Présentation

Cette situation professionnelle repose sur le développement d’une application Front-end avec le framework Angular pour une prise de commande au niveau d’un point de vente.

Deux scénarios peuvent coexister : l’opérateur prend la commande par téléphone pour une livraison à domicile ou le serveur prend une commande pour une consommation sur place.

On comprend bien pourquoi, étant une application interne, il n’existe pas d’authentification pour l’instant.

Elle utilisera par ailleurs une application Back-end dans le cadre d’une API présentant la gamme de produits à la vente. On se base sur les SushiBoxes de l’entreprise SushiShop afin d’approcher le plus une réalité commerciale.

### Attendus fonctionnels

L’application Web aura pour résultat essentiel le calcul d’une commande de plateaux de Sushi.

Elle comportera :

    -> l’affichage de la liste des plateaux de Sushi,
    -> la possibilité de voir le détail d’un plateau,
    -> l’achat d’un ou plusieurs plateaux sous la forme d’un panier,
    -> la visualisation des commandes sauvegardées localement,
    -> une page spécifique concernant la mise en place du RGPD

### Attendus techniques

    1. Interrogation d’une API existante via la saisie d’informations dans un formulaire,
    2. Définition d’une entité objet pour la représentation des données,
    3. Affichage de la liste des objets, accès au détail, calcul de commande,
    4. Sauvegarde locale côté client (LocalStorage),
    5. Prise en compte d’au moins 2 Evil User Stories,
    6. Test unitaire (au moins 3).

### Analyse de la demande

Vous êtes chargé de faire l’analyse initiale du projet. À ce titre vous produirez un diagramme des cas d’utilisation concernant l’application JS cliente ainsi qu’un diagramme présentant les différents tiers participants à la solution (client, serveur...).

La liste des plateaux (ou Boxes) sera composée de données extraites de l’application Back-end SushiAPI, existante mais qui ne fait pas partie du projet. Elle s’utilisera simplement comme une ressource externe. L’utilisateur s’attend à voir, au minimum, le nom du plateau, son image, son prix et son nombre de pièces.

**Note : comme l’information n’existe pas dans l’API, la notation sera aussi absente dans l’application Front- end.**

L’utilisateur après sélection d’un plateau, aura la possibilité d’en voir les détails comme la composition et les saveurs.

**Note : l’image du plateau vous sera fournie (archive Zip) et dans un souci de simplification, elles seront placées dans l’application Front-end (dossier assets).**

Le dossier d’analyse présentera entre autres, les algorithmes mis en œuvre pour obtenir les informations complètes d’un plateau (via des requêtes exploitant SushiAPI, application existante) et décrira la structure (JSON) des objets sauvegardés sur le client.

Toujours dans la présentation de la liste, l’utilisateur aura la possibilité de mettre dans un panier la commande d’un (ou plusieurs) plateau. La technique classique consistera à positionner deux boutons (- et +) ainsi qu’un champ contenant le total des plateaux demandés.

Un menu supplémentaire permettra de voir l’état de la commande courante qui devra manuellement être sauvegardée en local après insertion d’un bouton de validation.

**Note : La communication des commandes au service de préparation ne fait pas partie du périmètre fonctionnel de l’application. Vous avez la possibilité - facultative mais recommandée - d’y ajouter un bouton permettant la suppression d’une commande.**

### Ce qui est attendu

Un rapport de projet de la mission (**présentation datée, analyse, développement front-end, tests, lien vers le dépôt git, conclusion**). L’application devra contenir au moins **3 tests unitaires** et **2 Evil Users Stories**.

Consignes de livraison :

    ● Rapport de projet sous la forme d’un README.adoc de votre projet sur github.com (donc consultable en ligne)
    ● Lors de la remise de votre rapport, vous transmettrez un mail en respectant la forme suivante :

    Objet du mail : SIO22 - Situation professionnelle 2 Destinataire principal : M. Chamillard

Destinataires CC : M.Capuozzo, **autres membres de l’équipe**

    1) Date butoir pour une version provisoire de votre projet : vendredi 10 décembre 2021 - 23 h 59

        Cette partie contiendra obligatoirement :

        -> la date, le nom de l’équipe et les participants au projet,
        -> les différents diagrammes demandés,
        -> des requêtes illustrées sur l’API concernant l’ensemble des plateaux,
        -> le champ d’utilisation du RGPD dans ce projet sachant qu’il sera amené à être plus tard en ligne,
        -> le format de la structure JSON (interface ts) des commandes enregistrées dans le LocalStorage.

    2) Date butoir pour la version finale du projet : vendredi 18 février 2022 - 23 h 59

### Informations du projets

* Date du projet : 2 décembre 2021
* Nom de l'équipe : Les alternants
* Participants au projet : Enzo Carpentier, Kilian Moliere et Corentin Bonifacio

### Les différents diagrammes demandés

### Diagram séquentiel

![diagram_sequentiel](assets_readme/diagram/diagram_sequentiel.png)

### Diagram cas d'utilisation
![diagram_cas](assets_readme/diagram/diagram_cas.png)

### Les requêtes illustrées sur l'API concernant l'ensemble des plateaux

API du repos :

Fichier : **sushi-shop.service.ts**

```
const apiRest = 'http://127.0.0.1:3000';
```

API de tous les plateaux Nodes JS :

Fichier : **boxes.js**

```
// Retourne tous les plateaux
router.get('/', function (req, res, next) {
  var db = req.db;
  var collection = db.get('boxes');
  collection.find({}, function (e, listeBoxes) {
    res.send(listeBoxes);
  });
});
```

Affichage de tous les plateaux Angular :

Fichier : **sushi-shop.service.ts**

```
getAllsushis(): Observable <any> {
    return this.http.get<any> (apiRest + '/boxes').pipe(
      catchError(this.handleError)
    );
  }
```

### Les requêtes illustrées sur l'API concernant un plateau

API du repos :

Fichier : **sushi-shop.service.ts**

```
const apiRest = 'http://127.0.0.1:3000';
```

API d'un plateau Nodes JS :

Fichier : **boxes.js**

```
// Affichage d'un plateau
router.get('/:id', (req, res) => {
  var db = req.db;
  var collection = db.get('boxes');
  let { id } = req.params;
  collection.find({ "id": parseInt(id) }, function (e, unBoxe) {
    res.send(unBoxe);
  });
});
```

Affichage d'un tableau Angular :

Fichier : **sushi-shop.service.ts**

```
getOnesushi(id : number): Observable<any> {
    return this.http.get<any> (apiRest + '/boxes/' + id)
  }
```

### Champ d'utilisation du RGPD dans le projet

Pour visualiser notre champ d'utilisation du RGPD, référé vous à ce lien-ci : 
[RGPD](https://github.com/CorentinSIOdev/SushiFast/blob/main/src/app/component/rgpd/rgpd.component.html)

### Format de la structure JSON des commandes enregistrées dans le LocalStorage

### Deuxième Partie 

Page d'accueil Sushi Fast :

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/38391212/154764110-1db19ce6-979b-4c26-be65-66ab0450ab52.png">

Page Nos Plateaux :

<img width="1436" alt="image" src="https://user-images.githubusercontent.com/38391212/154764318-c9699ad2-afd5-4e53-a88f-ab0c4684b6fa.png">

Code HTML pour l'affichage des boxes :

<img width="950" alt="image" src="https://user-images.githubusercontent.com/38391212/154765486-361688f0-16bd-463a-91b0-aaa9e4d7217d.png">

Code Typescript :

<img width="854" alt="image" src="https://user-images.githubusercontent.com/38391212/154765546-39a3264f-cc24-4408-9b21-777549ce1eea.png">

Sur ce code il y a plusieurs fonctions la principale consiste bien a affiché toutes les boxes mais une autre consiste a ajouter au panier (sur une autre page en passant par un service qui lui l'ajoute au localStorage)

Page Mon panier :

<img width="1438" alt="image" src="https://user-images.githubusercontent.com/38391212/154765725-143e1f31-4c93-4c8f-bfc6-c184a9dfbaf6.png">
<img width="717" alt="image" src="https://user-images.githubusercontent.com/38391212/154765765-ef4154f0-3b93-4845-a956-e9dd70c4b2db.png">

Code  HTML : 

<img width="939" alt="image" src="https://user-images.githubusercontent.com/38391212/154765810-b672bc6a-27c0-4423-823e-65ce9b17c5a4.png">

Code TypeScript : 

La fonction pour supprimer 1 articles ou alors tous les articles :

<img width="775" alt="image" src="https://user-images.githubusercontent.com/38391212/154765861-34b6d71d-8009-4de2-b1db-95acc947cec8.png">

La fonction pour ajouter au payment :

<img width="935" alt="image" src="https://user-images.githubusercontent.com/38391212/154765950-f11c0e37-a941-4ac9-96c5-7511dd34b5bd.png">

Cette function va générer un nombre random compris entre 1 et 2 si deux fois, si les deux nombre générer sont identique alors le payment est validé cette function est juste pour éviter de faire valider la commande directement c'est un petit ajout car je n'ai pas pu faire de page pour rentrer une fausse carte comme ce que je voulais faire de base.
La function permet aussi de stocker la liste des articles / date de commande / prix total / nombre d'article acheté 
Et une fois le payment validé une redirection vers historique de commande est effectuer automatiquement et une suppresion du localStorage Commande est aussi effectuer.

Page Historiques de Commandes : 

<img width="1386" alt="image" src="https://user-images.githubusercontent.com/38391212/154766238-d957cb6e-1c0c-495c-8c34-d96ab77e2ce5.png">

Code HTML :

<img width="1021" alt="image" src="https://user-images.githubusercontent.com/38391212/154766284-ffbc62a4-a158-410e-9dcc-043cb108e964.png">

On affiche sous forme de tableau les résultat que nous avons au paravant insérer dans le local Storage sous la condition "Historique :"

Code Typescript : 

<img width="1022" alt="image" src="https://user-images.githubusercontent.com/38391212/154766385-4cd85d53-128d-4d9e-a77b-ded01e724965.png">

OnInit() donc a l'initialisation de la page je récupère l'historique des commandes et je l'affiche dans la boucle for ng for écrit dans la partie HTML
Pour la suppression je la trie en function de la date d'achat sous forme de caractères "Date Now = 1645221338524" et alors je supprime la commande en question 
ou alors je peux toujours supprimer toutes les commandes.

Page RGPD : 

<img width="1426" alt="image" src="https://user-images.githubusercontent.com/38391212/154764196-3b82c1ce-44fc-4910-bb5e-1bf643ca52f5.png">

Code HTML : 

<img width="945" alt="image" src="https://user-images.githubusercontent.com/38391212/154764243-90da23f7-b234-44a3-8354-4ab509a4747e.png">

Et pour finir voici les 3 cas d'Évil stories que j'ai pu trouver 

Evile Storie Sushi Fast

SushiFast est un logiciel uniquement disponible pour les employés pour la gestion de commande on peut comparer cela a la borne de commande au McDo
Evile Stories 1 :

En tant que personne voulant faire n’importe quoi et/ou nuire a SushiFast je me rend compte que la function pour supprimer une commande dans l’historique est filtré en fonction du prix donc si par exemple deux commande on le même prix je vais alors pouvoir supprimer les deux commandes d’un coup ! 

En tant que développeur ayant vue le problème je décide donc de choisir un autre filtre et ce filtre sera la date sous forme de numéro ce qui permettra d’être sur qu’il n’y est pas plusieurs commandes supprimé lors de la suppresion d’une Commande 

pour faire cela je vais donc rajouter dans ma classe historique.ts un endroit pour stocker ce date.now

￼![Untitled](https://user-images.githubusercontent.com/38391212/154766822-37215cc3-eb33-45d9-a6d2-864b952c3b87.png)


Et dans le code panier.component.ts je vais crée la date lors de la validation du payment et au passage je vais améliore mon historique de commande en transformant mon Date.now sous format Fri, 18 Feb 2022 20:38:33 GMT 

￼![Untitled 1](https://user-images.githubusercontent.com/38391212/154766842-8e066eec-cc82-489a-8728-e227f8e99e48.png)


Une fois cela effectuer et injecter dans mon historique service 

￼![Untitled 2](https://user-images.githubusercontent.com/38391212/154766847-c2ff9d0e-2338-43e0-a920-41ccd1f7d8e8.png)


Je vais maintenant filtré mon commandes.component.ts pour qu’il trie par date.now et qu’il arrête de trier par prix de cette manière :

￼![Untitled 3](https://user-images.githubusercontent.com/38391212/154766862-50239798-0f92-468d-bbd3-3155302454d1.png)


Evile Stories 2 : 

En tant que personne voulant faire n’importe quoi et/ou nuire a SushiFast je vais alors commander sans rien vraiment commander de manière vide et donc ajouter dans l’historique de commande des tableaux vides car rien n’a été commandé.

En tant que développeur ayant vue que l’on pouvais faire cela j’ajoute une condition qui stipule que si il n’y a pas de panier ajouter au panier alors j’affiche “Votre Panier est vide” et je ne permet pas de commander pour faire cela je vais juste ajouter : 

￼![Untitled 4](https://user-images.githubusercontent.com/38391212/154766870-89b073e2-be87-463b-9e8e-01c987b861ef.png)



il sera alors redirigé dans #commandeVide si lesCommandes.length > 0;

Evile Stories 3 :

En tant que personne voulant faire n’importe quoi et/ou nuire a SushiFast j’ai voulu ajouter plein de fois la même box et faire des commandes massivement sans les récupérer après.

En tant que développer je vais alors limiter l’ajout d’une box pour éviter ce genre de cas je vais donc le limiter a 10 / 12 pour faire cela il faut d’abord que je regarde si j’ai ajouter plusieurs fois la même boxe de cette manière : 

￼![Untitled 5](https://user-images.githubusercontent.com/38391212/154766876-bec4a9cc-9246-484a-a3ee-7dc6ac5aa265.png)


Je vais donc detecter si la même box a été ajouter plusieurs fois :

￼![Untitled 6](https://user-images.githubusercontent.com/38391212/154766881-01c9d783-a97e-4b46-9af7-e4e314b9f83c.png)


Pour aller plus loin je vais limiter l’ajout de cette même box a 10 malheureusement je n’ai pas pu finaliser ce cas du a un manque de temps :

￼![Untitled 7](https://user-images.githubusercontent.com/38391212/154766891-caac8340-f04b-4a56-8c8f-daa3ff2b692b.png)


Mais le code ressemblerais a cela et dans /// code here j’aurais du manipuler le localStorage pour qu’il enleve les commandes effectué en trop


Format [PDF](https://github.com/CorentinSIOdev/SushiFast/files/8100495/Evile_Storie_Sushi_Fast.pdf)

#   S u s h i - F a s t  
 