---
title: Erstellen der Game1-Klasse
ms.date: 03/30/2017
ms.assetid: 47932ce3-2ba5-476f-a26b-3ddfd5226f27
ms.openlocfilehash: 6a828dce2eed00c0a42e49d00358d836dc5ccde7
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-the-game1-class"></a>Erstellen der Game1-Klasse
Wie bei allen Microsoft XNA-Projekten ist die Game1-Klasse von der [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx)-Klasse abgeleitet, die die Initialisierung von einfachen Grafikgeräten, die Spiellogik und das Rendern von Code für XNA-Spiele bereitstellt. Die Game1-Klasse ist recht einfach, da die meiste Arbeit in den Klassen "GamePiece" und "GamePieceCollection" erledigt wird.  
  
## <a name="creating-the-code"></a>Erstellen des Codes  
 Die privaten Member der Klasse bestehe aus einem **GamePieceCollection**-Objekt, das die Spielsteine enthält, einem [GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx)-Objekt und einem [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx)-Objekt zum Rendern von Spielsteinen.  
  
 [!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]  
  
 Während der Spielinitialisierung werden diese Objekte instanziiert.  
  
 [!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]  
  
 Wenn die [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx)-Methode aufgerufen wird, werden die Spielsteine erstellt und einem **GamePieceCollection**-Objekt zugewiesen. Es gibt zwei Typen von Spielsteinen: Der Skalierungsfaktor für die Spielsteine wird leicht geändert, sodass es einige kleinere und einige größere Spielsteine gibt.  
  
 [!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]  
  
 Die [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx)-Methode wird beim Ausführen des Spiels wiederholt von XNA Framework aufgerufen. Die [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx)-Methode ruft die Methoden **ProcessInertia** und **UpdateFromMouse** in der Auflistung der Spielsteine auf. Diese Methoden sind unter [Creating the GamePieceCollection Class (Erstellen der GamePieceCollection-Klasse)](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) beschrieben.  
  
 [!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]  
  
 Die [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx)-Methode wird beim Ausführen des Spiels ebenfalls wiederholt von XNA Framework aufgerufen. Die [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx)-Methode rendert Spielsteine, indem sie die **Draw**-Methode des **GamePieceCollection**-Objekts aufruft. Diese Methode ist unter [Creating the GamePieceCollection Class (Erstellen der GamePieceCollection-Klasse)](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) beschrieben.  
  
 [!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]  
  
## <a name="see-also"></a>Siehe auch  
 [Manipulationen und Trägheit](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)  
 [Verwenden von Manipulationen und Trägheit in einer XNA-Anwendung](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)  
 [Erstellen der GamePiece-Klasse](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)  
 [Erstellen der GamePieceCollection-Klasse](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)  
 [Vollständige Codeauflistungen](../../../docs/framework/common-client-technologies/full-code-listings.md)
