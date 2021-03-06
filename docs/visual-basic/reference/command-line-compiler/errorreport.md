---
title: -errorreport
ms.date: 03/10/2018
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b8c6a81d3491f4876cfbca80aa8fda6640187176
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="-errorreport"></a>-errorreport
Gibt an, wie interne Compilerfehler von der Visual Basic-Compiler gemeldet werden sollen.  
  
## <a name="syntax"></a>Syntax  
  
```  
-errorreport:{ prompt | queue | send | none }  
```  
  
## <a name="remarks"></a>Hinweise  
 Diese Option bietet eine komfortable Möglichkeit, einen internen Compilerfehler (ICE) von Visual Basic, Visual Basic-Team bei Microsoft. Standardmäßig sendet der Compiler keine Informationen an Microsoft. Jedoch, wenn einen interner Compilerfehler auftreten, mit dieser Option können Sie den Fehler an Microsoft senden. Diese Informationen helfen Microsoft-Experten, die die Ursache zu identifizieren und die nächste Version von Visual Basic zu verbessern.  
  
 Die Fähigkeit eines Benutzers zum Senden von Berichten, hängt von Computer- und Richtlinienberechtigungen ab.  
  
 In der folgenden Tabelle werden die Auswirkungen der zusammengefasst die `-errorreport` Option.  
  
|Option|Verhalten|  
|---|---|  
|`prompt`|Wenn ein interner Compilerfehler auftritt, wird ein Dialogfeld hochgefahren, so, dass Sie die genauen Daten anzeigen können, die der Compiler gesammelt. Sie können bestimmen, ob es keine vertraulichen Informationen in den Fehlerbericht ist und treffen einer Entscheidung, ob sie sich an Microsoft senden. Wenn Sie sie senden möchten, und die Computer- und Benutzerrichtlinien zulassen, sendet der Compiler die Daten an Microsoft.|  
|`queue`|Der Fehlerbericht wird in die Warteschlange gesetzt. Wenn Sie sich mit Administratorrechten anmelden, können Sie Fehler melden, seit der letzten Ausführung mit dem Sie angemeldet waren (nicht werden Sie aufgefordert, Fehlerberichte Senden von mehr als einmal alle drei Tage). Dies ist das Standardverhalten bei der `-errorreport` nicht angegeben wird.|  
|`send`|Wenn ein interner Compilerfehler auftritt und die Computer- und Benutzerrichtlinien dies zulassen, sendet der Compiler die Daten an Microsoft.<br /><br /> Die Option `-errorreport:send` Fehlerinformationen automatisch an Microsoft zu senden versucht. Diese Option hängt von der Registrierung ab. Weitere Informationen zum Festlegen der entsprechenden Werte in der Registrierung finden Sie unter [Aktivieren der automatischen Fehlerberichterstattung in Visual Studio 2008-Befehlszeilentools](http://go.microsoft.com/fwlink/?LinkID=184695).|  
|`none`|Wenn ein interner Compilerfehler auftritt, wird er nicht erfasst oder an Microsoft übermittelt.|  
  
 Der Compiler sendet Daten, die in der Regel einige Quellcode enthält zum Zeitpunkt des Fehlers, der den Stapel enthält. Wenn `-errorreport` wird verwendet, mit der [- Bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) option, und klicken Sie dann die gesamte Quelldatei gesendet wird.  
  
 Diese Option ist am besten verwendet, mit der [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) option, da Microsoft-Techniker so einfach den Fehler reproduzieren können.  
  
> [!NOTE]
>  Die `-errorreport` Option ist nicht in der Visual Studio-Entwicklungsumgebung verfügbar; er ist nur bei verfügbar über die Befehlszeile kompilieren.  
  
## <a name="example"></a>Beispiel  
 Der folgende Code versucht, Kompilieren `T2.vb`, und wenn der Compiler einen interner Compilerfehler auftritt, sie werden aufgefordert, den Fehlerbericht an Microsoft zu senden.  
  
```  
vbc -errorreport:prompt t2.vb  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)  
 [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
