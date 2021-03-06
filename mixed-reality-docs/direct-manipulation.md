---
title: Manipulation directe
description: Vue d’ensemble du modèle d’entrée de manipulation directe
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
keywords: Mixte réalité, les regards, les regards ciblant, interaction, concevoir
ms.openlocfilehash: d855955d44c1cf074849992e5dd7b36b54675fdd
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2019
ms.locfileid: "64581329"
---
# <a name="direct-manipulation"></a>Manipulation directe
Manipulation directe est un modèle d’entrée qui implique de toucher hologrammes directement avec vos mains. L’objectif de la manipulation directe est que les objets se comportent exactement comme dans le monde réel. Boutons peuvent être activées simplement en appuyant sur les objets peuvent être interceptés par s’emparer les et contenu 2D se comporte comme un écran tactile virtuel.  Pour cette raison, diriger manipulation est facile pour les utilisateurs pour en savoir plus, et il est passionnant trop.  Il est considéré comme un modèle d’entrée « proches », ce qui signifie qu’il est particulièrement adapté pour l’interaction avec du contenu qui est au sein des armes atteindre.

Un élément clé qui facilite la manipulation directe pour en savoir est qu’il est basé sur le caractère intuitif. Il n’y a aucune mouvements symboliques à apprendre aux utilisateurs. Toutes les interactions doivent être générées autour d’un élément visuel qui peut être touché ou saisi.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle d’entrée</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Manipulation directe (près l’interaction de la main)</td>
        <td>❌ Ne pas pris en charge</td>
        <td>✔️ Recommandé</td>
        <td>➕ Une autre option mais <a href="point-and-commit.md">Point et validation (interaction lointain)</a> est recommandé</td>
    </tr>
</table>

Manipulation directe est un modèle d’entrée principal sur HoloLens 2, utilisant la main articulée nouveau système de suivi. Le modèle d’entrée est également disponible sur des casques IMMERSIFS grâce à l’utilisation de contrôleurs de mouvement, mais n’est pas recommandé que principal moyen d’interaction en dehors de la manipulation des objets.  Manipluation directe n’est pas disponible sur HoloLens v1.

## <a name="collidable-fingertip"></a>Bout des doigts collidable
Sur HoloLens 2, mains réel de l’utilisateur sont reconnus et interprétés en tant que modèles squelettes gauche et droite. Pour implémenter l’idée de toucher hologrammes directement des mains, dans l’idéal, 5 colliders ne sont attachés à portée de 5 main de chaque modèle de squelette de main. Toutefois, en pratique, en raison du manque de rétroaction tactile, portée de main collidable 10 entraîne un grand nombre de collisions inattendus et imprévisibles avec hologrammes. Par conséquent, nous vous suggérons pour ne placer un collider sur chaque doigt de l’index. L’index collidable portée de main peut toujours servir de points de contact active pour diverses entrées tactiles multipoints impliquant autre doigt, telles que press 1 doigt, 1 doigt appuyez sur 2 Appuyez sur le doigt et appuyez sur 5 doigt.

![Image de collidable par un doigt](images/Collidable-Fingertip-720px.jpg)<br>

### <a name="sphere-collider"></a>Sphère collider
Au lieu d’utiliser la forme générique aléatoire, nous vous suggérons d’utiliser un collider sphère et rendre visuellement pour fournir une meilleure signaux pour le ciblage de quasiment. Diamètre de la sphère doit correspondre à l’épaisseur du doigt index pour augmenter la précision de tactile. Il sera facile de récupérer la variable d’épaisseur du doigt en appelant l’aiguille de l’API.

<br>

### <a name="fingertip-cursor"></a>Curseur du bout des doigts
Outre le rendu d’une sphère collidable sur le bout des doigts index, nous créons une solution d’avance, le curseur par un doigt, pour obtenir une meilleure près de l’expérience de ciblage de manière interactive. Il est un curseur de forme de graphique en anneau attaché sur le bout des doigts index. En fonction de la proximité, il dynamiquement réagit à une cible en termes de l’orientation et la taille comme indiqué ci-dessous :
* Lorsque votre index se déplace vers un hologramme, le curseur est toujours parallèle à la surface de l’hologramme et progressivement diminue sa taille en conséquence. 
* Dès que le doigt toucher la surface, le curseur est réduit à un point et émet un événement tactile.

<br> Avec les commentaires interactive, les utilisateurs peuvent obtenir une haute précision près de ciblage des tâches, telles que le déclenchement d’un lien hypertexte sur un contenu web ou en appuyant sur un bouton. <br>

![Image de curseur par un doigt](images/Fingertip-Cursor-720px.jpg)<br>

## <a name="bounding-box-with-proximity-shader"></a>Zone englobante avec le nuanceur de proximité
L’hologramme lui-même nécessite également de fournir des commentaires visuels et audio pour compenser l’absence de rétroaction tactile. Pour ce faire, nous générons le concept du cadre englobant avec le nuanceur de proximité. Un rectangle englobant est une zone volumétriques minimales qui englobe un objet 3D. La zone englobante a un mécanisme interactive de rendu appelé nuanceur de proximité. Le nuanceur de proximité se comporte comme suit :

* Lorsque le doigt de l’index se trouve dans une plage, un coup de projecteur par un doigt est converti sur l’aire du cadre englobant. 
* Lorsque le bout des doigts se rapproche la surface, actualités condense en conséquence. 
* Dès que le bout des doigts toucher la surface, la totalité de zone englobante modifie la couleur ou générer un effet visuel pour refléter l’état tactile. 
* Pendant ce temps, un effet audio peut être activé pour améliorer le feedback de saisie visual.

![Zone englobante avec l’image de nuanceur de proximité](images/Bounding-Box-With-Proximity-Shader-720px.jpg)<br>

## <a name="pressable-button"></a>Bouton PRESSEE
Avec un par un doigt collidable, les utilisateurs sont maintenant prêtes à interagir avec le composant interface utilisateur de HOLOGRAPHIQUE très fondamental, bouton PRESSEE. Un bouton PRESSEE est un bouton HOLOGRAPHIQUE adapté pour press du doigt direct. Là encore, en raison du manque de rétroaction tactile, un bouton PRESSEE doter les deux mécanismes pour aborder la rétroaction tactile les problèmes liés. 
* Le premier mécanisme est englobant avec le nuanceur de proximité, ce qui a déjà été résolu dans le paragraphe qui précède. Il sert à fournir une meilleure idée de proximité permettant aux utilisateurs de l’approche et assurez-vous contact avec un bouton. 
* Le second est DÉPRESSION. Il crée le sens de presse, après qu’un par un doigt contacte le bouton. Le mécanisme est que le bouton se déplace étroitement avec le bout des doigts sur l’axe de profondeur. Le bouton peut être déclenché dès qu’atteindre une profondeur désignée (sur Presse) ou en laissant la profondeur (sur la mise en production) après le passage par son intermédiaire. 
* L’effet audio doit être ajouté pour améliorer les commentaires, lorsque le bouton est déclenché. 

![Image du bouton PRESSEE](images/Pressable-Button-720px.jpg)<br>

## <a name="2d-slate-interaction"></a>Interaction ardoise 2D
Une ardoise 2D est un conteneur HOLOGRAPHIQUE hébergement de contenu application 2D, comme navigateur web. Le concept de conception permettant d’interagir avec une ardoise 2D via la manipulation directe consiste à tirer parti du modèle mental de l’interaction avec un écran tactile physique.<br> <br>
Pour l’interaction avec le contact ardoise :<br> 
* Les utilisateurs utiliser votre index à appuyer sur un bouton ou un lien hypertexte. 
* Les utilisateurs utiliser votre index pour faire défiler un contenu ardoise diminué. 
* Les utilisateurs utiliser deux doigts de l’index pour effectuer un zoom et de sortie au contenu ardoise selon un mouvement relatif des doigts. 
![Image d’ardoise 2D](images/2D-Slate-Interaction-720px.jpg)<br>

<br>Pour la manipulation 2D d’ardoise lui-même :<br>
* Les utilisateurs peut permettre d’approcher les mains vers des angles et des bords pour révéler l’intuitivité de manipulation le plus proche. 
* En saisissant l’intuitivité de manipulation, les utilisateurs peuvent effectuer la mise à l’échelle uniforme via l’affordnaces coin et redistribution via l’intuitivité edge. 
* En saisissant le holobar en haut de l’ardoise 2D peuvent utilisateurs déplacer l’ardoise entière.<br><br>

![Image d’ardoise manipulation](images/Manipulate-2d-slate-720px.jpg)


## <a name="3d-object-manipulation"></a>Manipulation des objets 3D
HoloLens 2, les utilisateurs sont activés pour utiliser les mains pour manipuler directement les objets 3D hologramphic en appliquant un cadre englobant à chaque objet 3D. La zone englobante fournit une meilleure perception de profondeur via son nuanceur de proximité. Avec la zone englobante, il existe deux approches de conception pour la manipulation des objets 3D :      
### <a name="affordance-based-manipulation"></a>Le caractère intuitif en fonction de manipulation :
C’est un moyen permettant aux utilisateurs de manipuler l’objet 3D via la boîte englobante et l’intuitivité de manipulation autour d’elle. Dès que la part de l’utilisateur est proche d’un objet 3D, la zone englobante et la plus proche intuitif sont dévoilées. Les utilisateurs peuvent saisir la zone englobante pour déplacer l’objet entier, l’intuitivité edge pour faire pivoter et le coner permettant à l’échelle de manière uniforme.<br>

![Image de manipulation d’objet 3D](images/3D-Object-Manipulation-720px.jpg)<br>

### <a name="non-affordance-based-manipulation"></a>Le caractère non-intuitif en fonction de manipulation :
Dans cette mechanisom, aucun intuitif n’est attaché à la zone englobante. Les utilisateurs peuvent uniquement afficher la zone englobante, puis interagir directement avec lui. Si la zone englobante est saisie avec une main, la traduction et la rotation de l’objet sont associés au mouvement et l’orientation de la main. Lorsque l’objet est saisi avec deux mains, les utilisateurs peuvent traduire, mettre à l’échelle et faire pivoter en fonction des mouvements relatifs de deux mains.<br><br> 

<br><br>
Pour la manipulation exige la précision, nous vous recommandons afforance basé manipulation, en fournissant un niveau élevé de granularité. Pour une manipulation flexible, non intuitif manipulation sera un bon choix, offrant aux utilisateurs des expériences instantanés et amusant.


## <a name="instinctual-gestures"></a>Mouvements instinctual
Contrairement à HoloLens (1er gen), mouvements utilisateurs enseignement quelques prédéfinis, tels que Bloom et appuyez sur Air, HoloLens 2, nous ne demandons aux utilisateurs de mémoriser tout mouvement symbolique. Tous les gestes que les utilisateurs ont besoin pour interagir avec hologrammes et le contenu sont instinctual. Pour réaliser le mouvement instinctual consiste à guider les utilisateurs pour effectuer des mouvements de la conception d’intuitivité de l’interface utilisateur. Par exemple, si nous encourageons les utilisateurs à la capture d’un objet ou un point de contrôle avec pincement de deux doigts, l’objet ou le point de contrôle doit être petit. Si nous aimerions aux utilisateurs d’effectuer cinq manipulation doigt, l’objet ou le point de contrôle doit être relativement important. Comme pour les boutons, un petit bouton limiterait les utilisateurs pour appuyer sur avec un seul doigt, tandis qu’un bouton énorme encourage les utilisateurs à appuyer sur avec leurs paumes.
![](images/Instinctual-Gestures-720px.jpg)<br>

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a>Conception symétrique entre les mains et 6 contrôleurs DDL
Vous avez peut-être remarqué qu’il existe désormais parallels interaction que nous pouvons dessiner entre les mains dans les contrôleurs AR et mouvement dans VR. Les deux entrées peuvent servir à déclencher les manipulations directes dans leurs environnements respectifs. Dans les 2 HoloLens, faisant des mains au fonctionnement de la distance fermer une grande partie de la même façon que le bouton de manipulation glisser effectuent sur les contrôleurs de mouvement dans WMR. Cela fournit à vos utilisateurs avec une bonne connaissance de l’interaction entre les deux plateformes et peut s’avérer utile devez jamais vous décidez de migrer votre application à partir d’un à l’autre.

## <a name="optimizing-with-eye-tracking"></a>Optimisation avec suivi de le œil
Manipulation directe peut se sentent magique si elle fonctionne comme prévu, mais peut également rapidement devenir frustrante si vous ne pouvez pas déplacer n’importe où votre main plus sans par inadvertance déclencher un hologramme.
Suivi de le œil peut potentiellement utile dans une meilleure identification des éléments intention de l’utilisateur. 

* **Lorsque**: Réduire faussement déclencher une réponse de manipulation. Suivi de le œil permet de mieux comprendre qu’un utilisateur actuellement engagé avec. Par exemple, imaginez la que lecture dans un texte (démonstration) HOLOGRAPHIQUE lorsque vous atteignez plus vous attraper l’outil de travail réel.
En procédant ainsi, vous accidentellement déplacer votre main sur certains boutons HOLOGRAPHIQUE interactifs qui vous auriez pas remarqué même avant (par exemple, qu'il était même en dehors du champ de vision de l’utilisateur).
Pour faire court : Si l’utilisateur n’a pas examiné un hologramme pendant un certain temps, mais un événement tactile ou comprendre a été détecté pour celle-ci, il est probable que l’utilisateur n’a pas été réellement qui a l’intention d’interagir avec ce hologramme. 

* **Celui**: À part l’adressage false activations positif, un autre exemple comprend mieux identifier les hologrammes pour saisir ou examiner le point d’intersection précise ne peut pas être clair à partir de votre point de vue en particulier si plusieurs hologrammes sont positionnés proximité les uns autres. Alors que suivi d’yeux sur HoloLens 2 a une certaine limite sur la façon de précisément, elle peut déterminer vous regards des yeux, elle peut être très utile pour près interactions en raison d’une disparité de profondeur lors de l’interaction avec la main d’entrée. Cela signifie qu’il est parfois difficile de déterminer si votre main est derrière ou devant un hologramme précisément Attrapez par exemple un widget de manipulation.

 * **Où**: Utilisez les informations qu’un utilisateur recherche des gestes levant rapides. Saisissez un hologramme et à peu près jeter celui-ci vers votre destination prévue. Parfois, cela peut fonctionner parfaitement, effectuer rapidement les mouvements de main peut entraîner des destinations hautement inexactes.
Il s’agit où yeux peut aider à appuyer la main levée vecteur précédent de votre position prévue.

## <a name="see-also"></a>Voir aussi
* [Regards et validation](gaze-and-commit.md)
* [Point et validation](point-and-commit.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)

