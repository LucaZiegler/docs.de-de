---
title: Anweisungen (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- directives, Visual Basic compiler
- Visual Basic code, directives
- directives
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
ms.openlocfilehash: 38d54feae5cf7bf41a825d1f6000811e2b56f319
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="directives-visual-basic"></a>Anweisungen (Visual Basic)
In den Themen in diesem Abschnitt werden die Visual Basic-Quellcode-Compileranweisungen dokumentiert.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [#Const-Anweisung](../../../visual-basic/language-reference/directives/const-directive.md) --definieren Sie eine Compilerkonstante  
  
 [#ExternalSource-Direktive](../../../visual-basic/language-reference/directives/externalsource-directive.md) – Geben Sie eine Zuordnung zwischen Quellzeilen und Text für die Quelle extern  
  
 [#If... ... #Else-Direktiven](../../../visual-basic/language-reference/directives/if-then-else-directives.md) --kompilieren Sie ausgewählte Codeblöcke  
  
 [#Region-Direktive](../../../visual-basic/language-reference/directives/region-directive.md) --reduzieren und blenden Sie Codeabschnitte im Visual Studio-Editor  
  
 **#Disable, #Enable** --deaktivieren und aktivieren Sie bestimmte Warnungen für Codebereiche.  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
```  
  
 Sie können auch eine durch Kommas getrennte Liste von Warncodes deaktivieren und aktivieren.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Sprachreferenz zu Visual Basic](../../../visual-basic/language-reference/index.md)  
  
 [Visual Basic](../../../visual-basic/index.md)
