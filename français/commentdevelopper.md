# Mise en place de votre dossier
Le seul fichier que vous devez créer se trouvera dans le répertoire suivant:
```..\City of Heroes\data\texts\French\help\help.txt```

Si vous n'utilisez pas un client anglais (vous êtes peut-être mes amis baguettes: D), vous devrez utiliser ChineseTraditional, English, German, Japanese, Korean, or uk à la place de "French".

___________________________________________________

# Syntaxe:
Help.txt est juste un fichier texte normal. Vous pouvez utiliser n’importe quel éditeur de texte, tel que le notepad ou le notepad++ (thèmes sublime / sombres, si vous tenez à avoir les yeux). Il peut également prendre en charge le format Unicode, à condition qu'il soit enregistré au format Unicode.

Dans le langage de balisage que nous utilisons, il est important d'aller de l'avant, d'échapper entièrement aux citations et d'utiliser les conteneurs de script de texte en bloc: `<& texte &>`


La syntaxe générale est la suivante:
```
Category "Nom de catégorie" Alignment
{
	Item "Nom de l'article" Alignment
	{
		Text <&
			...
		&>
	}
}
```

___________________________________________________

# Catégories

Les catégories situées à l'extrême gauche peuvent contenir plusieurs éléments en dessous. Ils peuvent également être marqués comme Hero, Villain ou Praetorian uniquement. Si vous êtes un héros, les catégories Villain n'apparaîtront que lorsque vous aurez changé de camp. "Masterminds" est un exemple de catégorie basée sur l'alignement dans le menu Aide en jeu. Cette catégorie n'apparaîtra dans le menu d'aide que si vous êtes un méchant.

je crois comprendre que la syntaxe du lecteur doit être écrite en anglais

La Catégories syntaxe générale est la suivante:

```
Category <NAME> <ALIGNEMENT> <COMMENT - Optional>
{
	...
}
```
### Notes:

- `NAME` est le texte que vous souhaitez afficher. Ce champ est limité en longueur. Le texte supplémentaire se répercutera dans la fenêtre Article s'il dépasse l'espace prévu à cet effet.

- `ALIGNMENT` peut être` All`, `HeroOnly`,` VillianOnly` ou `PraetorianOnly`. `All` apparaît pour tout le monde indépendamment de l'alignement.

- `COMMENT` est pour tous les commentaires que vous souhaitez mettre dans le fichier. Tout ce qui se trouve après le `//` sera ignoré lors de l'affichage en jeu

- `{` et `}` sont utilisés pour placer tous les éléments dans une catégorie. Évitez de mettre des commentaires n'importe où dans la même ligne que ceux-ci.

Nous ne voudrons probablement pas limiter cela aux allignments, alors voici un exemple d'une catégorie que nous allons utiliser:
```
Category "Catégorie pour tous" All //c'est là que les commentaires sont appropriés
{
	...
}
```

___________________________________________________

# Items
Sous chaque catégorie, vous pouvez avoir plusieurs 'Item'. Il ne semble pas y avoir de limite au nombre de ce type, mais seulement à la taille de chacun. Chaque élément ne peut contenir que 21 000 caractères environ. Cela inclut les espaces (espaces, retours à la ligne et nouvelles lignes, etc.). Item suivent une syntaxe très similaire aux catégories et peuvent également être définis pour l'alignement. La seule différence entre les catégories et les items dans la syntaxe réside dans le mot "item" ou "catégorie".

syntaxe d'une catégorie que nous allons utiliser:
```
Item <NAME> <ALIGNEMENT> <COMMENT - Optional>
{
	...
}
```

### Notes:
- `NAME` est pour tout le texte que vous voulez afficher. Ce champ est limité en longueur. Le texte supplémentaire débordera dans la fenêtre Élément s'il dépasse l'espace prévu.

- `ALIGNMENT` peut encore être` All`, `HeroOnly`,` VillianOnly` ou `PraetorianOnly`. `All` apparaît pour tout le monde indépendamment de l'alignement.

- `COMMENT` est l'endroit où tous les commentaires que vous souhaitez mettre dans le fichier. Tout ce qui suit les // sera ignoré lors de l'affichage en jeu

- `{` et `}` est utilisé pour placer tous les éléments dans une catégorie. Évitez de mettre des commentaires n'importe où dans la même ligne que ceux-ci.

___________________________________________________


# ItemText

La syntaxe pour un item est semblable à la suivante
```
Text <&
Des trucs pour tout le monde

&>
```
Notez le `<&` et le `&>`. Ils sont utilisés pour entourer le texte de item. Ils doivent être présents pour qu'il s'affiche correctement. Le mot Texte est utilisé de deux manières différentes. S'il s'agit d'un item pour tous les alignements, "Text" signifie pour tout le monde. Si vous spécifiez des alignements, alors "Text" signifie Héros uniquement. D'autres options sont V_Text pour les méchants et P_Text pour les prétoriens. Regardez cet exemple:

```
Item "Transport" All //les noms de comment se déplacer
{
		Text <&
			prendre le métro pour aller dans un autre quartier
		&>
		V_Text <&
			prendre le "Rogue Island Ferries"
		&>
		P_Text <&
			prendre le metro pour aller dans un autre quartier
		&>
}
```
Lorsque cet élément est affiché, vous ne verrez qu’une de ces options, en fonction de votre alignement. Si vous ne souhaitez pas spécifier l'alignement, utilisez simplement `Text`.

En ce qui concerne le contenu, vous pouvez faire toutes sortes de choses merveilleuses. Le texte de l'article est un document HTML simplifié que le client rend pour vous. Il utilise uniquement les balises HTML de base. Les tags les plus courants confirmés sont:

```
<table>, <tr>, <td> with attributes of Width, height, align
<BR>
&nbsp;
<span> avec des attributs d'aligner
<img> 
<a>
<color>

```
Voici un exemple de syntaxe

Texte simple avec codes de couleur et centrage:

```
Exemple de texte1  -- Imprime "Exemple de texte1" en lettres blanches
	<color HotPink>Exemple de texte2</color> -- Imprime "Exemple de texte2" dans une couleur rose vif
	<color #00FF00>Exemple de texte3</color> -- Imprime "Exemple de texte3" en couleur vert lime
	<span align=center>Exemple de texte4</span> -- Imprime "Exemple de texte4" au centre de la fenetre
	
```

Les codes de couleur peuvent être des noms de couleur HTML ou l'équivalent hexadecimal de la couleur. Les noms de couleur et hexadécimaux peuvent être trouvés en ligne en recherchant les codes de couleur HTML

### Liens: 
Les liens dans le fichier d'aide fonctionnent de la même manière que si vous deviez les saisir dans le chat. Toute commande de barre oblique peut être utilisée ici (/e dance). Vous devez également fournir les couleurs à utiliser pour afficher le lien, ainsi que lorsque le pointeur est survolé. L'omission des couleurs crée des liens invisibles.
c'est la syntaxe:
```

<linkhover #00FF00><link #00FF00><a href='cmd:<SLASH_COMMAND>'><LINKTEXT></a></link></linkhover>

```
##### Remarques

- `SLASH_COMMAND` est une commande valide /slash commande. Vous pouvez en chaîner plusieurs avec $$

- et `LINKTEXT` est le texte qui est affiche.

Exemples:
```
	<linkhover #7CFC00><link #32CD32><a href="cmd:t $self, Salut Je suis un lien">lien ample1</a></link></linkhover><br>
	<linkhover #00FF00><link #00FF00><a href='cmd:chansend "Un nom de chaîne avec des espaces" Ce que je veux dire...'>lien ample2</a></link></linkhover><br>
	<linkhover #00FF00><link #00FF00><a href='cmd:Stuck'>Cliquez ici pour débloquer</a></link></linkhover><br>
	
```

### Tables:
Les bordures de tableau dépendent beaucoup de la résolution / des paramètres et devraient probablement être évitées, mais vous pouvez toujours les utiliser pour organiser les éléments en colonnes. Vous pouvez également les aligner à droite, à gauche, au centre.

Exemples:
```
	<table>
		<tr>
			<td align=left>	Cell1</td>
			<td align=center>	Cell2</td>
			<td align=right>	Cell3</td>
		</tr>
		<tr>
			<td>	Cell4</td>
			<td><color #00FF00>Cell5</color></td>
			<td><linkhover #00FF00><link #00FF00><a href='cmd:t $self, C'est Cell 6'>Cell6</a></link></linkhover></td>
		</tr>
	</table>
	
```

### Images:
Le menu d'aide prend également en charge les images. Les noms d'image doivent être des noms d'image en jeu. Vous pouvez également lui demander de réduire ou d’élargir la hauteur et la largeur avec HTML standard. Si une image est trop grande pour s’adapter à la fenêtre, elle ne sera tout simplement pas affichée. Si une image liée ne peut pas être trouvée, un petit carré blanc sera utilisé à la place. Vous n'avez pas besoin de spécifier le chemin d'accès à l'image, mais simplement le nom du fichier.

Exemples:
`<img width=256 height=256 src="map_city_01_01.tga">`
...

___________________________________________________

# Exemple complet:

Exemple d'image de sortie en anglais:
https://media.discordapp.net/attachments/572533274992312330/580124225063354369/imqg6o.png?width=379&height=301

exemple de code:
```
Category "Category For Everyone" All //Tout le monde peut voir cela
{
	Item "Item for Everyone" All //Tout le monde peut voir cela
	{
	Text <&
			Sample Text1<BR>
			<color HotPink>Sample Text2</color><BR>
			<color #00FF00>Sample Text3</color><BR> 
			<span align=center>Sample Text4</span>
			<linkhover #7CFC00><link #32CD32><a href="cmd:t $self, Hiya. I'm a Link">Sample Link1</a></link></linkhover><br>
			<linkhover #00FF00><link #00FF00><a href='cmd:chansend "A Name with Spaces" What I want to say...'>Sample Link2</a></link></linkhover><br>
			<table>
				<tr>
					<td align=left>	Cell1</td>
					<td align=center>	Cell2</td>
					<td align=right>	Cell3</td>
				</tr>
				<tr>
					<td>	Cell4</td>
					<td><color #00FF00>Cell5</color></td>
					<td><linkhover #00FF00><link #00FF00><a href='cmd:t $self, This is Cell 6'>Cell6</a></link></linkhover></td>
				</tr>
			</table>
			<img width=256 height=256 src="map_city_01_01.tga">
		&>
	}
	Item " " All //Spacer
	{
		Text <&
		&>
	}
	Item "extes dépendants de l'alignement" All 
	{
		Text <&
			Hero Text
		&>
		V_Text <&
			Hero Text
		&>
		P_Text <&
			Hero Text
		&>
	}
 }
Category "Éléments dépendants de l'alignement" All //Tout le monde peut voir cela
{
	Item "Hero Item" HeroOnly 
	{
		Text <&
			Hero Text
		&>
	}
	Item "Hero Item" VillianOnly 
	{
		Text <&
			Villain Text
		&>
	}
	Item "Hero Item" PraetorianOnly 
	{
		Text <&
			Praetorian Text
		&>
	}  
}

Category "Hero Only Category" HeroOnly //Seuls les heroes peuvent voir cela
{
	Item "Hero Item" All 
	{
		Text <&
			Hero Text
		&>
	}	
}
Category "Villain Only Category" VillianOnly //Seuls les villains peuvent voir cela
{
	Item "Villain Item" All 
	{
		Text <&
			Villain Text
		&>
	}	
}
Category "Praetorian Only Category" PraetorianOnly //Praetorians Only can see this
{
	Item "Praetorian Item" All 
	{
		Text <&
			Praetorian Text
		&>
	}	
}

```

___________________________________________________

## TL;DR / "Remarques"

Quelques points à noter spécifiquement:

- Si vous apportez des modifications à help.txt, vous devez quitter le jeu complètement avant de voir les modifications entrer en vigueur.

- Le menu Help sera le même pour tous vos personnages sur tous les serveurs.

- Les commentaires peuvent être ajoutés en utilisant une double barre oblique (c.-à-d. //). Tout texte suivant les barres obliques sera ignoré par le client.

- Chaque Item a un maximum de 21 000 caractères. Rien de plus grand et le menu d'aide n'affichera que quelques lettres dans le champ Item.

- Le terme "VillianOnly" est correct car le fichier d'origine utilisait la même orthographe

- lorsque l'alignement des accolades n'est pas important, veuillez utiliser un alignement correct pour la santé mentale des autres :)
