---
layout: post
title:  "Customiser Spotify avec Spicetify"
date:   2021-03-30 12:00:00 +0530
categories: posts spotify spicetify
image: /images/spicetify.png
---

J'utilise Spotify. C'est très orignal d'écouter de la musique (non). Donc j'utilise Spotify. J'écoute de la musique en faisant du sport, au bureau, en voyage et même sous la douche. Même si la plupart du temps c'est mon téléphone qui diffuse la musique à l'enceinte ou au casque qui est connecté à l'instant T, j'utilise surtout mon ordinateur quand je travaille.

J'aime avoir une interface claire et qui correspond à mon style sur la plupart des applications et logiciels que j'utilise. C'est le cas de Spotify. Il existe pour cela un projet open-source sur [GitHub](https://github.com/) : la plateforme où se trouve la majorité des logiciels open-source. Voici donc un tutoriel pour utiliser ```Spicetify : l'outil de personnalisation pour Spotify```.

## Le projet

Spicetify est un outil en ligne de commande permettant de modifier l'application spotify sur Windows et Linux. Il est possible de changer la couleur de toute l'interface et de modifier le style du plus petit détail à toute l'application.

Le projet se trouve à cette adresse : [https://github.com/khanhas/spicetify-cli](https://github.com/khanhas/spicetify-cli)

## Installer Spicetify 

*Toutes les méthodes ici : [https://github.com/khanhas/spicetify-cli/wiki/Installation](https://github.com/khanhas/spicetify-cli/wiki/Installation)*

### Sur Windows

Pour installer l'application il suffit de copier-coller une commande dans Powershell. Powershell c'est l'interface en ligne de commande de Windows. Pour l'ouvrir appuyez sur les touches Win+X. Sélectionnez Windows PowerShell. PowerShell s’ouvre.

<div class="text-center mb-2">
    <img src="/images/winXPowershell.jpg" alt="Menu Win+X" width="50%">
</div>

Voici les commandes à copier-coller (sans le dollar) :

{% highlight Powershell %}

$ Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/khanhas/spicetify-cli/master/install.ps1" | Invoke-Expression

{% endhighlight %}

### Sur Linux et MacOS

Sur MacOS comme sur Windows il y a une commande à executer. Pour cela, ouvrez l'application Terminal.

<div class="text-center mb-2">
    <img src="/images/terminalMac.jpg" alt="Terminal Mac" width="50%">
</div>

Voici la commande à copier-coller (sans le dollar) :

{% highlight sh %}

$ curl -fsSL https://raw.githubusercontent.com/khanhas/spicetify-cli/master/install.sh | sh

{% endhighlight %}

## Choisir un theme

Pour choisir un theme, il existe la page de [wiki](https://github.com/morpheusthewhite/spicetify-themes/wiki/Themes-preview) de la bibliothèque de thèmes.

#### Télécharger la bibliothèque de thèmes

Vous pouvez utiliser la commande git ou alors télécharger la bibliothèque à ce lien : [https://github.com/morpheusthewhite/spicetify-themes/archive/refs/heads/master.zip](https://github.com/morpheusthewhite/spicetify-themes/archive/refs/heads/master.zip)

Sur Windows on ouvre le repertoire des thèmes avec la commande (toujours sans le dollar) :

{% highlight Powershell %}

$ explorer "$(spicetify -c | Split-Path)\Themes\"

{% endhighlight %}

Puis on copie-colle le contenu du dossier téléchargé dans le repertoire que l'on vient d'ouvrir.

Sur MacOS on ouvre le repertoire des thèmes avec la commande (toujours sans le dollar) :

{% highlight shell %}

$ open "$(dirname "$(spicetify -c)")/Themes/"

{% endhighlight %}

Puis on copie-colle le contenu du dossier téléchargé dans le repertoire que l'on vient d'ouvrir.

#### Activer le thème

Pour activer un thème on trouve généralement les indications sur chacune des pages du wiki de la bibliothèque de thèmes. J'ai pour ma part utilisé le thème ```DribbblishDynamic```. Ce thème a la particularité de changer de couleur en fonction de la pochette du titre en cours de lecture.

Sur windows :

{% highlight Powershell %}

$ cd "$(spicetify -c | Split-Path)\Themes\DribbblishDynamic"
$ Copy-Item dribbblish-dynamic.js ..\..\Extensions
$ spicetify config extensions dribbblish-dynamic.js
$ spicetify config current_theme DribbblishDynamic color_scheme dark
$ spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
$ spicetify apply

{% endhighlight %}

Sur MacOS :

{% highlight shell %}

$ touch $HOME/.bash_profile
$ echo "export SPICETIFY_INSTALL=\"$spicetify_install\"" >> $HOME/.bash_profile
$ echo "export PATH=\"\$SPICETIFY_INSTALL:\$PATH\" >> $HOME/.bash_profile
$ source $HOME/.bash_profile
$ cd "$(dirname "$(spicetify -c)")/Themes/DribbblishDynamic"
$ mkdir -p ../../Extensions
$ cp dribbblish-dynamic.js ../../Extensions/.
$ spicetify config extensions dribbblish-dynamic.js
$ spicetify config current_theme DribbblishDynamic color_scheme dark
$ spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
$ spicetify backup apply
$ spicetify apply

{% endhighlight %}

***

Et voilà !

<div class="text-center mb-2">
    <img src="/images/spicetify.png" alt="Terminal Mac">
</div>
