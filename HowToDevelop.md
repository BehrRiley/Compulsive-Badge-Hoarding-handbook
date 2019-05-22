# Setting up your folder
The only file that you need to create will be located here:
```..\City of Heroes\Data\texts\English\Menus\help.txt```

If you are not using an English client(this may be you my baguette friends :D), you will need to use ChineseTraditional, French, German, Japanese, Korean, or uk in place of English.

___________________________________________________

# Syntax:
Help.txt is just a normal text file. Any text editor can be used, such as Notepad or Notepad++(sublime/dark themes if you value having eyes). It can also support Unicode, as long as it is saved in Unicode format.
In the markup language we utilize, it's important to just go ahead and escape quotations entirely and utilize the block text script containers: `<& stuff &>`

The general syntax is as follows:
```
Category "Category Name" Alignment
{
	Item "Item Name" Alignment
	{
		Text <&
			...
		&>
	}
}
```

___________________________________________________

# Categories

The Categories on the far left can contain multiple Items underneath them. They can also be flagged as Hero, Villain, or Praetorian Only. If you are a Hero, the Villain categories will not show until you switch sides. An example of alignment based categories in the InGame Help menu is "Masterminds". That category will only show in the help menu if you are a Villain. 

Category syntax is as follows:

```
Category <NAME> <ALIGNEMENT> <COMMENT - Optional>
{
	...
}
```
### Notes:

- Where `NAME` is Whatever text you want to have displayed. This field is limited in length. The extra text will bleed over into the Item window if it exceeds the space provided.

- Where `ALIGNMENT` can be `All`, `HeroOnly`, `VillianOnly`, or `PraetorianOnly`. `All` shows up for everyone regardless of alignment.

- Optimally (please), `COMMENT` is for Any comments you want to put in the file. Anything after the `//`'s will be ignored when displaying in game

- Lastly, `{` and `}` are used to place all the items under one category. Avoid putting comments anywhere in the same line as these.

We probably won't want to restrict this from allignments, so here's an example of a category we'll use:
```
Category "Category For Everyone" All //this is where comments are appropriate
{
	...
}
```

___________________________________________________

# Items
Under each category, you can have multiple Items. There does not appear to be a limit to the number of items, just the size of each one. Each Item can only be about 21,000 characters long. This includes whitespace (ie. spaces, carriage returns, and newlines). Items follow a very similar syntax to categories, and can also be set for alignment. The only difference in syntax from Categories to Items is the actual word 'Item' or 'Category'

Let's look at the syntax for items.
```
Item <NAME> <ALIGNEMENT> <COMMENT - Optional>
{
	...
}
```

### Notes:
- Where `NAME` Is for whatever text you want to have displayed. This field is limited in length. The extra text will bleed over into the Item window if it exceeds the space provided.

- Where `ALIGNMENT` again can be `All`, `HeroOnly`, `VillianOnly`, or `PraetorianOnly`. `All` shows up for everyone regardless of alignment.

- Optimally, `COMMENT` is where Any comments you want to put in the file. Anything after the //'s will be ignored when displaying in game

- Lastly, `{` and `}` is used to place all the items under one category. Avoid putting comments anywhere in the same line as these.

___________________________________________________


# ItemText

The markup for an Item is similar to the following
```
Text <&
Stuff for everyone
&>
```
Notice the `<&` and the `&>`. They are used to surround the text of the item. They must be present for it to display correctly. The word Text is used in two different ways. If it is an Item for all alignments, then "Text" means for everyone. If you are specifying alignments then "Text" means Heroes Only. Other options are V_Text for villains and P_Text for Praetorians. Look at this example:

```
Item "Transportation" All //the names of how to get around
{
		Text <&
			Use the tram lines. Used to be called Green and Yellow Line.
		&>
		V_Text <&
			Use the Rogue Island Ferries
		&>
		P_Text <&
			Use the CTA subway 
		&>
}
```
When this item is viewed, you will only see 1 of those options, depending on your alignment. If you do not care to specify alignment, simply use `Text`. 

As far as the content goes, you can do all sorts of wonderful things. Item text is a simplified HTML document that the client renders for you. It uses only the basic HTML tags. The most common tags confirmed are:

```
<table>, <tr>, <td> with attributes of Width, height, align
<BR>
&nbsp;
<span> with attributes of align
<img> 
<a>
<color>

```
Here is some example syntax

Simple Text with color codes and centering:

```
Sample Text1  -- Prints out "Sample Text1" in white letters
	<color HotPink>Sample Text2</color> -- Prints out "Sample Text2" in a Hot Pink color
	<color #00FF00>Sample Text3</color> -- Prints out "Sample Text3" in a Lime Green Color
	<span align=center>Sample Text4</span> -- Prints Sample Text4 centered in the window
	
```

Color codes can be either HTML Color names or the Hex equivalent of the color. Hex and color names can be found online by searching for HTML Color codes

### Links: 
Links in the help file function the same way as if you were to type them into chat. Any slash command can be used here. You must also provide the colors to be used to show the link, as well as when the pointer is hovered over it. Omitting the colors results in invisible links.
The format is
```

<linkhover #00FF00><link #00FF00><a href='cmd:<SLASH_COMMAND>'><LINKTEXT></a></link></linkhover>

```
##### Notes

- Where `SLASH_COMMAND` is any valid /slash command. You can string multiple ones with $$

- and `LINKTEXT` is the text that is displayed.

Examples:
```
	<linkhover #7CFC00><link #32CD32><a href="cmd:t $self, Hiya. I'm a Link">Sample Link1</a></link></linkhover><br>
	<linkhover #00FF00><link #00FF00><a href='cmd:chansend "A Channel Name with Spaces" What I want to say...'>Sample Link2</a></link></linkhover><br>
	<linkhover #00FF00><link #00FF00><a href='cmd:Stuck'>Click here to UnStuck</a></link></linkhover><br>
	
```

### Tables:
Table borders are highly dependant on resolution/settings, and likely should be avoided, but you can still use them for organizing things into columns. You can also Right,Left,Center align them as well.

Example:
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
			<td><linkhover #00FF00><link #00FF00><a href='cmd:t $self, This is Cell 6'>Cell6</a></link></linkhover></td>
		</tr>
	</table>
	
```

### Images:
The help menu also supports images. The image names must be in-game image names. You can also tell it to shrink or expand the height and width through standard HTML. If an image is to big to fit the window, it will simply not show. If an image that is linked can not be found, a small white square will be used instead. You do not need to specify the path to the image, just the filename.
Examples are:
`<img width=256 height=256 src="map_city_01_01.tga">`
...

___________________________________________________

# Full Based Example & Code:

Example Output Image:
https://media.discordapp.net/attachments/572533274992312330/580124225063354369/imqg6o.png?width=379&height=301

Example Code:
```
Category "Category For Everyone" All //Everyone can see this
{
	Item "Item for Everyone" All //Everyone can see this
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
	Item "Alignment Dependent Texts" All 
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
Category "Alignment Dependent Items" All //Everyone can see this
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

Category "Hero Only Category" HeroOnly //Heroes Only can see this
{
	Item "Hero Item" All 
	{
		Text <&
			Hero Text
		&>
	}	
}
Category "Villain Only Category" VillianOnly //Villains Only can see this
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

## TL;DR / "Notes"
If you've skipped to the bottom for advanced topics to wing the basics with understanding of the advanced, have fun. Some things to note specifically:

- If you make changes to help.txt, you must exit the game completely before seeing the changes take effect.

- The Help Menu will be the same for all of your characters on all servers.

- Comments can be added by using a double forward slash (ie //). Any text following the slashes will be ignored by the client.

- Each Item has a max of 21,000 characters. Anything greater and the help menu will display only a few letters in the Item field.

- The term "VillianOnly" is correct as the original file used the same spelling

- where alignment of braces are not important, please utilize correct alignment for the sanity of others :)
