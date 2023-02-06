
## Introduction : 

#### Qu'est ce que c'est MONGO DB ? 

SGBD orienté document et complétement cross-plateform. 
On peut y accéder via le cloud
Mongo DB est un système de gestion de base de donnée qui viens stocker les dossier sous format JSON . 
Aucune structure n'est imposé 
Les documents permettent de regrouper des informations. 

#### Qu'est ce qu'une base de donnée (Database) 

La base de données est le conteneur physique des collections. (espace disque)
Chaque base de données possède ses propres fichiers dans le système de gestion de fichier sur la machine hôte


#### Collections  

Une collections est  un groupe de documents MongoDB. C'est l'équivalent d'une table dans un système de  gestion de base de données. 
Les collections n'imposent pas de schéma précis. 
Les documents au sein d'une même collection peuvent avoir des champs différents. 
Malgré tout les différent document reste pour le moins très similaire. 

#### Document 

Un document est un ensemble de clé valeur (Objet). 
Le schéma des document est dit "dynamique".


#### Résumer  

Une **Database** est composé de plusieurs **Collections** et les collections quand à eux sont composé de différent **Document**.


#### Comparaison avec SQL 

L'équivalent des **table** corresponde à une **collection** . 
**Des lignes**  = **Document** 
**Colonne**  = **field** 
**Jointure** = **Document imbriqués**

#### Avantage de Mongo DB 

Pas de schéma / Structure claire et simple : objet / pas de jointure complexe / 
Des requêtes imbriqués et dynamique (presque aussi performant que SQL) / 
Très facile de "squale " / Stockage sur disque / plus besoin d'ORM 

Mongo DB fait tout bien mais il ne sera jamais n°1 



#### Mongo DB

##### JSON  / BSON :

JSON est un format de données textuelles dérivé de la notation des objets du langages Javascript. 
Il est facile à lire et écrire pour l'humain.
Aisément analysable.

JSON se base sur deux structures : 
 -   Une collection de couples nom/valeur. Divers langages la réifient par un _objet_, un enregistrement, une structure, un dictionnaire, une table de hachage, une liste typée ou un tableau associatif.
-   Une liste de valeurs ordonnées. La plupart des langages la réifient par un _tableau_, un vecteur, une liste ou une suite.

BSON -> JSON 
JSON -> BSON 

Un document **BSON** peut être de taille 16Mo.
**BSON** est un codage binaire de la notation d'objet Javascript (JSON) 
une notation d'objet textuelle largement utilisée pour transmettre et stocker des données dans des applications web. 
**JSON** est plus facile à comprendre car il est lisible par l'homme, mais comparé à BSON, il supporte moins de types de données.
**BSON** encode également les informations de type et de longueur, ce qui facilite l'analyse par les machines.

- `{}` Ceci représente un Objet vide en JSON

Les propriété d'un objet JSON sont matérialisée par  un ou plusieurs paires cle/valeur :

```JSON 
{
"clé": "valeur", 
"uneAutreCle": {"autreclé": "uneautreValeur"},
"untableau": []
}
```

 ### JSON prend en charge de façon native  plusieurs formes de données : 

- Boolean
- Numérique
- Chaine de caractère 
- Tableau 
- Objet 
- Null (indique l'absence de valeur)

 ### Mongo DB viens à sont tour rajouté de types : 

- Le type **Date** stocke sous ma forme d'un entier signe de 8 octets
Pour que une durée devienne une date, il nous faut un point départ. 

**EPOCH** (1 janvier 1970) est  une convention donc on se base sur cette date.
Représente le temps écouler depuis le temps UNIX

**UNIX**  est une famille de systèmes d'exploitation multitâche et multi-utilisateur dérivé du Unix d'origine créé par AT&T, le développement de ce dernier ayant commencé dans les années 1970.
Comme Linux / GNU / BSD.

-  Le type **ObjetId** stocke 12 octets, utilise en interne / Mongo DB afin de gérer les identifiants.

-  Le type **NumberLong** et le type **NumberInt** :  par default Mongo DB considérer toutes valeur numérique comme un nombre à virgule code sur 8 octets.
   Représentent des entiers signes sur 8 et 4 octets.

-  Le type **BinData** : pour stocker des chaînes de caractères ne possédant pas de représentation dans l'encodage **UTF-8** 
 **UTF8** (_UCS transformation format_ 8 bits) est un format de codage de caractères. Il permet de gérer tous les caractères dits unicodes.
 Chaque caractère est codé sur un ou plusieurs points de code.


### Mongo DB en ligne de commande : 

#### Lancement de Mongo DB : 

```Bash 

mongod

||

mongod --port 27017

||

mongod --port 27017 --dbpath /data/databases --logpath /tmp/mongodb.log --logappend


```


#### Commande sur Compass : 

```mongoShell

show database  || show collections 

db  (affiche la base de donnée)

use + ... (permet de changer de base de donnée)

db.createUser ({"user": "Root", "pwd": "root", "roles": [{"userAdmin", "db": "admin"}, "readWriteAnyDatabase"]}) (Créé un utilisateur et lui confie certain droit)




```


Pour créé une base de donnée sur Mongo DB il n'existe pas une commande implicite venant nous la générer. 
C'est en utilisant **use + nom** de la **Base** et une fois que on aura ajouté une **Collection** à l'intérieur  avec un **Document** dans ce dernier 
Alors notre BDD sera alors créer et affiché.

Pour crée votre DB : 
```Javascript
use + Le nom de votre bdd

db.uneCollection.insert({"uneCle": "uneValeur"}) (Crée notre collections )
```


Pour supprimé votre DB  : 
 ```Javascript
use + nom de votre bdd a supprimer

db.dropDatabase()
```

Affiche les éléments de votre collections de votre BDD : 
```Javascript
use + nom de votre BDD

db.uneCollection.find() (Permer dafficher les Documents de ma Collections)
(Equivaut au Select *)

```

Afficher les détails d'une collections : 

```Javascript

db.runCommand({"collstats": "uneCollection"})
```


### Gestion des collections : 

Collations sert à définir des règles sur les chaines de caractère.

```Javascript
{
	**locale**: <string>,
	caseLevel: <boolean>,
	caseFirst: <string>,
	strength: <entier>,
	numeriOrdering: <boolean>,
	...
}
```

Au sein de ce type de document le champ locale est obligatoire.


On est pas dans l'obligation pour créer une collection de recréer une BDD.
On peut passer directement à la création une collection. 

```Javascript
Créé une collection : 
db.createCollection("newCollection", {"collation": {"locale": "fr"}})

Supprimer une collection : 
db.newCollection.drop()

Renommer une collection : 
db.ewCollection.renameCollection("newCollection")
```



### Les documents

Une collections possèdes diverse documents.
Lors de notre création de notre base de donnée accompagné de sa collection.
On remarque que on créé aussi un document par la même occasion. 

```Javascript
Insert un Document dans la Collection "uneCollection" : 

db.uneCollection.insert({"uneCle": "uneValeur"})

insersion d'une collection personnes possédant deux document distinct : 

db.personnes.insert([
{"Nom": "leNom", "Prénom": "lePrénom"},
{"Nom": "Test", "Prénom": "BOB", "age": 20}
])


```


Mise  à part créer de nouveau document on peut également les mettre à jour avec une Update : 
```Javascript
db.collection.updateOne(<filtre>, <modification>)

Change le Prénom du document ayant comme Nom "leNom" : 

db.personnes.update({"Nom": "leNom"},{
$set: {"Prénom": "Toto"}
})

```

Validation de Document : 

```Javascript 
var athletes = [{
"nom": "Eclair",
"prenom": "Jean-Michel",
"discipline": "Course"
},{
"nom": "Allen",
"prenom": "Barry",
"discipline": "Course"
},{
"nom": "Cena",
"prenom": "John",
"discipline": "Catcher"
}   
]

 
```

Exemple de validation de document : 

```Javascript
var proprietes = [{
"nom": {
"bsonType": "string",
"pattern": "^[A-Z].*",
"description": "Chaine de caractere + RegEXP - obligatoire"},
"prenom":{
"bsonType": "string",
"description": "Chaine de caractere  - obligatoire"},
"discipline": {
"enum": ["Course", "Catcher"],
"description": "Liste de sport possibles - obligatoire"},
}]
```

Une fois nos règles établies, on va modifier notre collection a l'aide d'un commande : 

```Javascript

db.runCommand(
{
	"collMod": "athletes",
	"validator": {
		$jsonSchema: {
			"bsonType": "object",
			"required": ["nom", "prenom", "discipline"],
			"properties": "proprieties"
		}
	}
}
)
```


#### Retourner des données spécifique 

Quand on des collections composé d'un nombre important de documents.
Pour ce faire une peut employer une command Find nous permettant de retourner les données demander selon nos conditions spécifier : 

```Javascript 
db.collection.find({"age": {$eq: 76}})

Retourne tout les document de notre collection possédant un age égale à 76
```

D'autre opérateur sont à notre disposition : 

$ne : different de ...
$gt : superieur a ... 
$gte : superieur ou egal ...
$in et $nin : absence ou presence

On peut egalement combiner  ces operateur pour effectuer des recherches sur des intervalles : 

```javascript 
db.collection.find({"age": {$lt: 50, $gt: 20}})
Retourne tout document de notre collections possédant un age compris entre 50 et 20 
db.collection.find({"age": {$exists: true}})
Retourne tout document possédant le champ âge.
```

#### Agrégation 

Les opérations d'agrégation traitent plusieurs documents et renvoient des résultats calculés.
Vous pouvez utiliser les opérations d'agrégation pour :
- Regrouper les valeurs de plusieurs documents.
- Effectuer des opérations sur les données groupées pour renvoyer un résultat unique.
-  Analyser l'évolution des données dans le temps.

Exemple d'agrégation : 
 ```Javascript 
 db.orders.aggregate( [

   // Stage 1: Filter pizza order documents by pizza size
   {
      $match: { size: "medium" }
   },

   // Stage 2: Group remaining documents by pizza name and calculate total quantity
   {
      $group: { _id: "$name", totalQuantity: { $sum: "$quantity" } }
   }
] )
```