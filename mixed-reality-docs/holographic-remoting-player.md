---
title: Lecteur de communication à distance HOLOGRAPHIQUE
description: Le lecteur de communication à distance holographique est une application Compagnon qui se connecte à des applications de PC et des jeux qui prennent en charge la communication à distance HOLOGRAPHIQUE. Communication à distance HOLOGRAPHIQUE diffuse HOLOGRAPHIQUE contenu à partir d’un PC à votre Microsoft HoloLens dans en temps réel, à l’aide d’une connexion Wi-Fi.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, la communication à distance, la communication à distance HOLOGRAPHIQUE
ms.openlocfilehash: 16add6c72b594822cacbef6c92ce196ab9b13429
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597085"
---
# <a name="holographic-remoting-player"></a>Lecteur de communication à distance HOLOGRAPHIQUE

Le lecteur de communication à distance holographique est une application Compagnon qui se connecte à des applications de PC et des jeux qui prennent en charge la communication à distance HOLOGRAPHIQUE. Communication à distance HOLOGRAPHIQUE diffuse HOLOGRAPHIQUE contenu à partir d’un PC à votre Microsoft HoloLens dans en temps réel, à l’aide d’une connexion Wi-Fi.

Le lecteur de communication à distance HOLOGRAPHIQUE utilisable uniquement avec les applications PC conçus spécifiquement pour prendre en charge la communication à distance HOLOGRAPHIQUE.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="connecting-to-the-holographic-remoting-player"></a>Connexion à l’acteur de communication à distance HOLOGRAPHIQUE

Suivez les instructions de votre application pour se connecter à l’acteur de communication à distance HOLOGRAPHIQUE. Vous devez entrer l’adresse IP de votre appareil HoloLens, que vous pouvez voir sur l’écran principal du joueur de communication à distance comme suit :

![Lecteur de communication à distance HOLOGRAPHIQUE](images/holographicremotingplayer.png)

Chaque fois que vous voyez l’écran principal, vous savez que vous n’avez pas d’une application connectée.

Notez que la connexion de communication à distance holographique est **ne pas chiffré**. Vous devez toujours utiliser holographique de communication à distance via une connexion Wi-Fi sécurisée auxquels vous faites confiance.

## <a name="quality-and-performance"></a>Qualité et des performances

La qualité et les performances de votre expérience peut varier en fonction de trois facteurs :
* **L’expérience HOLOGRAPHIQUE que vous exécutez** -applications qui restituent contenu haute résolution ou extrêmement détaillés peuvent nécessiter un PC plus rapide ou le plus rapidement la connexion sans fil.
* **Matériel de votre PC** -votre PC doit être en mesure d’exécuter et de coder votre expérience HOLOGRAPHIQUE à 60 images par seconde. Pour une carte graphique, nous recommandons généralement un GeForce GTX 970 ou ou AMD Radeon R9 290 de mieux. Là encore, votre expérience spécifique peut nécessiter une carte supérieur ou inférieur en bout.
* **Votre connexion Wi-Fi** -votre expérience holographique est diffusé en continu via le Wi-Fi. Utiliser un réseau rapide avec une faible surcharge pour optimiser la qualité. À l’aide d’un PC qui est connecté via un câble Ethernet, plutôt que de Wi-Fi, peut également améliorer la qualité.

## <a name="diagnostics"></a>Diagnostics

Pour mesurer la qualité de votre connexion, par exemple **« activer les diagnostics »** tandis que dans l’écran principal de l’acteur de communication à distance HOLOGRAPHIQUE. Lorsque les diagnostics sont activés, l’application vous l’indiquera :
* **I/s** - le nombre moyen de trames rendues le joueur de communication à distance reçoit et rendu par seconde. L’idéal est de 60 i/s.
* **Latence** -la quantité moyenne de temps nécessaire pour un frame accéder à partir de votre PC à l’HoloLens. Faible mieux c’est. Il s’agit dépend en grande partie de votre réseau Wi-Fi.

Tandis que dans l’écran principal, vous pouvez dire **« désactiver les diagnostics »** pour désactiver les diagnostics.

## <a name="pc-system-requirements"></a>Configuration requise du PC
* Votre PC **doit** exécuter la mise à jour anniversaire de Windows 10.
* Nous recommandons un GeForce GTX 970 ou ou AMD Radeon R9 290 de meilleure carte graphique.
* Nous vous recommandons de que vous connecter à votre PC à votre réseau via ethernet pour réduire le nombre de tronçons de sans fil.

## <a name="see-also"></a>Voir aussi
* [Termes du contrat de licence de logiciel holographique de communication à distance](microsoft-holographic-remoting-software-license-terms.md)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
