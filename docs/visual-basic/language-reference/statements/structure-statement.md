---
title: Structure Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Structure
- Structure
helpviewer_keywords:
- user-defined types [Visual Basic], Structure statement
- compound data types [Visual Basic]
- Structure keyword [Visual Basic]
- Structure statement [Visual Basic]
- UDT (user-defined types)
- types [Visual Basic], user-defined
ms.assetid: 9bd1deea-2a89-4cdc-812c-6dcbb947c391
ms.openlocfilehash: 6a3626706b226b0be253fd35fa60b33a71b86007
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="structure-statement"></a>Structure Statement
Deklariert den Namen einer Struktur und führt die Definitionen der Variablen, Eigenschaften, Ereignisse und Prozeduren ein, aus denen die Struktur besteht.  
  
## <a name="syntax"></a>Syntax  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Partial ] _  
Structure name [ ( Of typelist ) ]  
    [ Implements interfacenames ]  
    [ datamemberdeclarations ]  
    [ methodmemberdeclarations ]  
End Structure  
```  
  
## <a name="parts"></a>Teile  
  
|Begriff|Definition|  
|---|---|  
|`attributelist`|Dies ist optional. Finden Sie unter [Attributliste](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Dies ist optional. Einer der folgenden Werte ist möglich:<br /><br /> -   [Öffentliche](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Geschützt](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   ["Friend"](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Finden Sie unter [Zugriffsebenen in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Dies ist optional. Finden Sie unter [Schatten](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`Partial`|Dies ist optional. Gibt eine partielle Definition der Struktur an. Finden Sie unter [partielle](../../../visual-basic/language-reference/modifiers/partial.md).|  
|`name`|Erforderlich. Name der Struktur. Finden Sie unter [deklarierte Elementnamen](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`Of`|Dies ist optional. Gibt an, dass dies eine generische Struktur ist.|  
|`typelist`|Erforderlich, wenn Sie mithilfe der [von](../../../visual-basic/language-reference/statements/of-clause.md) Schlüsselwort. Liste mit Typparametern für diese Struktur. Finden Sie unter [geben Liste](../../../visual-basic/language-reference/statements/type-list.md).|  
|`Implements`|Dies ist optional. Gibt an, dass diese Struktur die Member einer oder mehrerer Schnittstellen implementiert. Finden Sie unter [Anweisung implementiert](../../../visual-basic/language-reference/statements/implements-statement.md).|  
|`interfacenames`|Erforderlich, wenn Sie die `Implements`-Anweisung verwenden. Die Namen der von dieser Struktur implementierten Schnittstellen.|  
|`datamemberdeclarations`|Erforderlich. NULL oder mehr `Const`, `Dim`, `Enum`, oder `Event` Anweisungen deklarieren *Datenmember* der Struktur.|  
|`methodmemberdeclarations`|Dies ist optional. 0 (null) oder mehr Deklarationen der `Function`, `Operator`, `Property`, oder `Sub` Prozeduren, die als dienen *Methodenmember* der Struktur.|  
|`End Structure`|Erforderlich. Beendet die `Structure`-Definition.|  
  
## <a name="remarks"></a>Hinweise  
 Die `Structure`-Anweisung definiert einen zusammengesetzten Werttyp, den Sie anpassen können. Ein *Struktur* ist eine Verallgemeinerung des benutzerdefinierten Typs (UDT) von früheren Versionen von Visual Basic. Weitere Informationen finden Sie unter [Strukturen](../../../visual-basic/programming-guide/language-features/data-types/structures.md).  
  
 Strukturen unterstützen viele Funktionen, die auch von Klassen unterstützt werden. Strukturen können z. B. Eigenschaften und Prozeduren aufweisen, Schnittstellen implementieren und parametrisierte Konstruktoren enthalten. Allerdings bestehen zwischen Strukturen und Klassen erhebliche Unterschiede in den Bereichen Vererbung, Deklarationen und Verwendung. Außerdem sind Klassen Verweistypen, und Strukturen sind Werttypen. Weitere Informationen finden Sie unter [Strukturen und Klassen](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md).  
  
 `Structure` kann nur auf Namespace- oder Modulebene verwendet werden. Dies bedeutet, dass die *Deklarationskontext* für eine Struktur muss eine Quelldatei, Namespace, Klasse, Struktur, Modul oder Schnittstelle, und nicht mit einer Prozedur oder eines Blocks. Weitere Informationen finden Sie unter [Deklarationskontexte und Standardzugriffsebenen](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Strukturen standardmäßig ["Friend"](../../../visual-basic/language-reference/modifiers/friend.md) Zugriff. Sie können ihre Zugriffsebenen mit den Zugriffsmodifizierern anpassen. Weitere Informationen finden Sie unter [Zugriffsebenen in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## <a name="rules"></a>Regeln  
  
-   **Schachteln.** Sie können eine Struktur in einer anderen Struktur definieren. Die äußere Struktur wird als die *enthaltende Struktur*, und die innere Struktur wird aufgerufen, eine *geschachtelte Struktur*. Sie können jedoch nicht über die enthaltende Struktur auf die Member einer geschachtelten Struktur zugreifen. Stattdessen müssen Sie eine Variable mit dem Datentyp der geschachtelten Struktur deklarieren.  
  
-   **Memberdeklaration.** Sie müssen jeden Member einer Struktur deklarieren. Ein Strukturmember kann nicht [geschützte](../../../visual-basic/language-reference/modifiers/protected.md) oder `Protected Friend` da aus einer Struktur nicht geerbt werden kann. Die Struktur selbst kann jedoch `Protected` oder `Protected Friend` sein.  
  
     Sie können in einer Struktur null oder mehr nicht freigegebene Variablen oder nicht freigegebene nicht benutzerdefinierte Ereignisse deklarieren. Es ist nicht möglich, nur Konstanten, Eigenschaften und Prozeduren zu definieren, selbst wenn einige davon nicht gemeinsam genutzt werden.  
  
-   **die Initialisierung.** Der Wert von nicht freigegebenen Datenmembern einer Struktur kann nicht als Teil der Deklaration initialisiert werden. Sie müssen einen solchen Datenmember entweder mit einem parametrisierten Konstruktor auf Strukturebene initialisieren oder dem Member nach dem Erstellen einer Instanz der Struktur einen Wert zuweisen.  
  
-   **Vererbung.** Eine Struktur kann von keinem anderen Typ als von <xref:System.ValueType> erben, von dem alle Strukturen erben. Insbesondere kann eine Struktur nicht von einer anderen Struktur erben.  
  
     Können Sie keine der [Anweisung erbt](../../../visual-basic/language-reference/statements/inherits-statement.md) auch nicht zum angeben, in der Strukturdefinition eines <xref:System.ValueType>.  
  
-   **-Implementierung.** Wenn die Struktur verwendet, die [Implements-Anweisung](../../../visual-basic/language-reference/statements/implements-statement.md), müssen Sie jedes Element durch jede Schnittstelle, die Sie, in angeben definierten implementieren `interfacenames`.  
  
-   **Standardeigenschaft.** Eine Struktur kann höchstens eine Eigenschaft als angeben seiner *Standardeigenschaft*unter Verwendung der [Standard](../../../visual-basic/language-reference/modifiers/default.md) Modifizierer. Weitere Informationen finden Sie unter [Standard](../../../visual-basic/language-reference/modifiers/default.md).  
  
## <a name="behavior"></a>Verhalten  
  
-   **Zugriffsebene.** In einer Struktur können Sie jeden Member mit einer eigenen Zugriffsebene deklarieren. Alle Strukturmember standardmäßig [öffentlichen](../../../visual-basic/language-reference/modifiers/public.md) Zugriff. Beachten Sie, dass der Zugriff auf die Member einer Struktur automatisch eingeschränkt ist, wenn die Struktur selbst über eine restriktivere Zugriffsebene verfügt, selbst wenn Sie die Zugriffsebenen der Member mit den Zugriffsmodifizierern anpassen.  
  
-   **Bereich.** Der Gültigkeitsbereich einer Struktur umfasst den Namespace, die Klasse, Struktur oder das Modul, in dem bzw. der sich die Struktur befindet.  
  
     Der Gültigkeitsbereich eines Strukturmembers umfasst die gesamte Struktur.  
  
-   **Lebensdauer.** Eine Struktur selbst verfügt nicht über eine Lebensdauer. Stattdessen verfügt jede Instanz der Struktur über eine Lebensdauer, die von allen anderen Instanzen unabhängig ist.  
  
     Die Lebensdauer einer Instanz beginnt, während der Erstellung von einem [New-Operator](../../../visual-basic/language-reference/operators/new-operator.md) Klausel. Sie endet, wenn die enthaltende Lebensdauer der Variablen endet.  
  
     Sie können die Lebensdauer einer Strukturinstanz nicht verlängern. Eine den Funktionen einer statischen Struktur ähnelnde Funktionalität wird von einem Modul bereitgestellt. Weitere Informationen finden Sie unter [Modulanweisung](../../../visual-basic/language-reference/statements/module-statement.md).  
  
     Strukturmember verfügen über eine Lebensdauer, die davon abhängt, wie und wo sie deklariert werden. Weitere Informationen finden Sie unter "Lifetime" in [Class-Anweisung](../../../visual-basic/language-reference/statements/class-statement.md).  
  
-   **Qualifizierung.** In Code außerhalb einer Struktur muss der Name eines Members mit dem Namen dieser Struktur qualifiziert werden.  
  
     Wenn Code in einer geschachtelten Struktur einen nicht qualifizierten Verweis auf ein Programmierelement enthält, wird von Visual Basic das Element zunächst in der geschachtelten Struktur gesucht, anschließend in der enthaltenden Struktur und so weiter bis zum äußersten enthaltenden Element. Weitere Informationen finden Sie unter [Verweise auf deklarierte Elemente](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
-   **Speicherverbrauch.** Wie bei allen zusammengesetzten Datentypen können Sie den gesamten Speicherverbrauch auch bei Strukturen nicht dadurch zuverlässig berechnen, indem Sie die nominalen Speicherbelegungen ihrer Member addieren. Darüber hinaus können Sie nicht davon ausgehen, dass die Member im Speicher in derselben Reihenfolge wie in der Deklaration angeordnet sind. Wenn Sie das Speicherlayout einer Struktur steuern müssen, können Sie das <xref:System.Runtime.InteropServices.StructLayoutAttribute>-Attribut auf die `Structure`-Anweisung anwenden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die `Structure`-Anweisung für die Definition einer Gruppe verknüpfter Daten für einen Mitarbeiter verwendet. Es veranschaulicht die Verwendung von Membern mit dem Zugriff `Public`, `Friend` und `Private`, um den Grad der Vertraulichkeit der Datenelemente anzugeben. Es zeigt außerdem Prozedur-, Eigenschaften- und Ereignismember.  
  
 [!code-vb[VbVbalrStatements#57](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/structure-statement_1.vb)]  
  
## <a name="see-also"></a>Siehe auch  
 [Class-Anweisung](../../../visual-basic/language-reference/statements/class-statement.md)  
 [Interface-Anweisung](../../../visual-basic/language-reference/statements/interface-statement.md)  
 [Module-Anweisung](../../../visual-basic/language-reference/statements/module-statement.md)  
 [Dim-Anweisung](../../../visual-basic/language-reference/statements/dim-statement.md)  
 [Const-Anweisung](../../../visual-basic/language-reference/statements/const-statement.md)  
 [Enum-Anweisung](../../../visual-basic/language-reference/statements/enum-statement.md)  
 [Event-Anweisung](../../../visual-basic/language-reference/statements/event-statement.md)  
 [Operator-Anweisung](../../../visual-basic/language-reference/statements/operator-statement.md)  
 [Property-Anweisung](../../../visual-basic/language-reference/statements/property-statement.md)  
 [Strukturen und Klassen](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)
