### Étape 1 : Identifier un scénario ou un problème du monde réel

**Problème Identifié :** 

Le problème identifié concerne la gestionde stock . Le but est de fournir un service minimaliste en serverless pour faire un inventaire le plus facilement possible, eviter les problemes liés aux probleme de lecture de fichier comme.

**Solution Proposée :** 

Pour palier ce problème, La mise en place d'un système de gestion d'inventaire automatisé semble être une très bonne solution. Pour cela, j'ai utilisé principalement des azures fonctions liées à la base de données Azure Cosmos DB pour effectuer les opérations suivantes : ajouter, modifier un produit et afficher tous les produits;

### Étape 2 : Conception de l'architecture de solution

#### 2.1. Stockage des données

J'ai utilisé **Azure Cosmos DB** pour stocker mes données concernant les produits. Ce choix est dû au fait qu'il s'agit d'une ressource serverless et donc m'offre une certaine allegement au niveau de la prise en charge et la disponibilité des données, et il est capable de d'assumer l'evolution des données.

#### 2.2. Traitement des données

Les **Azure Functions** pour traiter les données stockées dans **Azure Cosmos DB**. .

### Étape 3 : Mise en œuvre de la solution

1. Tout d'abord, j'ai créé une instance **Azure Cosmos DB** pour stocker mes données nommée : **_maBaseDeDonnees_**.

2.Prés cela, j'ai créé 3 **Azure Functions** de type HTTP Trigger pour automatiser : la premiere pour modifier un article, la deuxieme pour consulter tous les articles et le derniers pour en créer un nouveau.

### Étape 4 : Design de la solution
<img width="239" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/2145dd56-3ee9-4c46-b6cc-3e1edcf71d50">

Dans ce premier design correspondant à l'etat actuel de ma solution, on remarque 3 étapes importantes qui sont les sivantes : 

1 => Execution d'une requette http, qui va declencher une Azure fonction.

2 => Selon la requette exécutée, l'une des trois fonction sera éxécutée (impossible d'avoir deux des trois ou tous s'executer à la fois).

3 => Impact de l'Azure fonction sur la base de données.

Une evolution de cette solution est la suivante : 

<img width="586" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/8f4e7b7e-e7c7-44c8-b97c-0263fdb8776d">

1 => Execution d'une requette http, qui va declencher une Azure fonction.

2 => Selon la requette exécutée, l'une des trois fonction sera éxécutée (impossible d'avoir deux des trois ou tous s'executer à la fois).

3 => Impact de l'Azure fonction sur la base de données.

4 => Si l'Azure fonction exécutée entraine la baisse de stock à une quantité predifinie, la logic app est déclenchée et envoie une alerte à l'utilisateur pour lui notifier et le suggérer à ravitailler le produit en question

### Mes Azure fonctions
#### Modifier un article : type Post 
URL de la fonction : _https://projectben.azurewebsites.net/api/HttpTrigger1?code=iE0uzGctpt0SvWCE-FwCnmegGm4eZsdnT_FM6DpsZlTjAzFuuINpbg==_  
Voici le corps de la requette de test pour l'Azure fonction :  

<img width="423" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/9e79d6b9-927a-47ae-ab13-cd341549ffdd">  

 et voici le resultat : ça nous affiche son état precedent ainsi que l'etat après l'execution :   
 
<img width="716" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/b09b2fd0-6e75-4275-8604-63786ff71aea">  


#### Afficher tous les articles : type Get
URL de la fonction : _https://projectben.azurewebsites.net/api/HttpTrigger2?code=dN4HJAfeD4gSRQjl1vnbaMvUHoWoBnIyuuPb4F0OxCByAzFu4FyOjw==_  

Etant donnée que la fonction recupére toutes les donnée le corps de la requette est vide et voici son resultat :   
<img width="824" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/ac73983d-e791-4700-bb91-5918a87163c4">  

#### Ajouter un article : type Post
URL de la fonction : _https://projectben.azurewebsites.net/api/HttpTrigger3?code=0EWm7YpgRrgIrOnvZwAO4409CCb0d4HKG6L-nmE1BSDrAzFu19G_1g==_  
 Voici le corps d'un exemple que j'ai utilisé pour faire mon dernier test quant à l'ajout d'un nouveau produit:  

 <img width="407" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/5a6239f8-844a-4d12-98b2-5caa69c2b6c6">  

 ainsi que le resultat du test :   
<img width="900" alt="image" src="https://github.com/Ben-Hadji/serverless/assets/83819844/4cd1d702-4176-424f-9969-432d5e636e88">  





