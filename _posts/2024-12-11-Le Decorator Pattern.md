Dans cet article nous allons nous mettre dans la peau de Luigi. 

Luigi est le fils de Mario, un patron de pizzeria. 

Luigi veut développer un outil de commandes de pizza pour son père, fatigué de le voir courrir systématiquement après les commandes et les factures.

Chez Mario on propose 3 pizzas : margarita, napolitaine, reine.

![best pizza in town](https://images.unsplash.com/photo-1528137871618-79d2761e3fd5?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3wzNjAwOTd8MHwxfHNlYXJjaHwzfHxwaXp6YXxlbnwwfDB8fHwxNzMyMjg1MDEwfDA&ixlib=rb-4.0.3&q=80&w=400)

*Photo by [Vita Marija Murenaite](https://unsplash.com/@runningvita?utm_source=Obsidian%20Image%20Inserter%20Plugin&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=Obsidian%20Image%20Inserter%20Plugin&utm_medium=referral)*

Il propose aussi des suppléments : burrata, champignons et légumes.

![Healthy Grocery Shopping](https://images.unsplash.com/photo-1418669112725-fb499fb61127?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3wzNjAwOTd8MHwxfHNlYXJjaHw4fHx2ZWdldGFibGVzfGVufDB8MHx8fDE3MzIyODUwMzd8MA&ixlib=rb-4.0.3&q=80&w=400)

*Photo by [leonie wise](https://unsplash.com/@leoniewise?utm_source=Obsidian%20Image%20Inserter%20Plugin&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=Obsidian%20Image%20Inserter%20Plugin&utm_medium=referral)*


Jusque là, tout va bien. 

A présent, en tant que développeur, Luigi dois m'occuper de modéliser toutes ces infos pour les implementer dans son outil de gestion de commandes.

Car, je ne l'ai pas dit, mais le prix et la description d'une pizza dépendent de ce qu'elle contient, évidemment. 

Donc je vais créer une classe pour modéliser ma margarita (c'est assez bizarre comme phrase). 

Par exemple

```csharp 
public class Margarita 
{

     private int Cost = 12;
     private string Description = "I'm a Margarita";
     public Margarita() { }

	 public int GetCost()
	 {
		 return Cost;
	 }
	
	 public string GetDescription()
	 {
		 return Description;
	 }
}
```

Ce n'est pas une bonne pratique d'écrire les valeurs en dur comme c'est fait ainsi, mais le focus n'est pas sur cette bonne pratique. On y reviendra dans un autre article.

Maintenant si je veux une Margarita avec des champignons et de la burrata, ou encore une Margarita avec juste de la burrata, ou bien juste des légumes ... vous avez compris, le nombre de possibilités est assez important pour créer un type de classe par combinaison possible.

C'est là que le Decorator pattern intervient. 

Ce pattern consiste à découpler le produit au sens logiciel de ce qu'il le "décore", c'est à dire découpler la pizza de ses suppléments. 

Voici donc ce que nous avons pour l'instant :


![alt text](https://raw.githubusercontent.com/fayssal-az/fayssal-az.github.io/master/images/classes.png)

Et donc comment faire pour ajouter de la burrata sur cette pizza : eh bien on invoque l'abstraction.

![alt alt2 text](https://raw.githubusercontent.com/fayssal-az/fayssal-az.github.io/master/images/uml_diagram.png)

Qu'est ce qu'on vient de faire ?
Nous sommes partis du fait que notre pizza et notre burrata avaient deux méthodes : `GetCost()` et `GetDescription()`

Nous avons ensuite fait une première abstraction, ce qui a donnée la classe `Nourriture`. 
Chaque nourriture ayant un prix et une description, on peut admettre de les faire hériter de la même classe abstraite. 

Puis nous avons ajouté une classe : `SupplementsDecorator` dont vont hériter tous nos suppléments.

Pourquoi me diriez vous ? Eh bien parce que c'est comme ça !

Plus sérieusement, cette classe permet **d'appliquer le décorateur au produit désiré.**

Vous remarquerez que cette classe hérite de la classe mère mais qu'elle est aussi composée de cette même classe mère (la flèche avec un losange traduit une relation de composition, pour les fans d'UML)

Donc non seulement elle hérite de ses méthodes mais elle se compose aussi de la même classe mère, c'est ce qui permet de passer une pizza en argument du constructeur et ainsi de récupérer le prix et la description d'une pizza. 

Bon, si tout n'est pas clair, c'est normal, j'ai aussi eu du mal à comprendre du premier coup jusqu'à ce que ... j'écrive moi même le code à partir du diagramme UML.

Donc si vous êtes arrivés jusque là, bravo. Encore un effort, et essayer d'écrire le code. 

Dans mon prochain article je donnerai le code et expliquerai les détails d'implémentation.





