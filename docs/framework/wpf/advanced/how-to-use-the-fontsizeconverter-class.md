---
title: 'Gewusst wie: Verwenden der FontSizeConverter-Klasse'
ms.date: 03/30/2017
helpviewer_keywords:
- FontSizeConverter objects [WPF]
- typography [WPF], FontSizeConverter objects
ms.assetid: 3b0592bd-7223-4860-a108-a5d72f3a9178
ms.openlocfilehash: 625beb06b526e2753abc6f982cf5834bfae1f202
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-use-the-fontsizeconverter-class"></a>Gewusst wie: Verwenden der FontSizeConverter-Klasse
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird gezeigt, wie zum Erstellen einer Instanz von <xref:System.Windows.FontSizeConverter> und verwenden, um die Schriftgröße zu ändern.  
  
 Im Beispiel definiert eine benutzerdefinierte Methode mit dem Namen `changeSize` , konvertiert den Inhalt der eine <xref:System.Windows.Controls.ListBoxItem>, wie definiert in einer separaten [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] -Datei, um eine Instanz von <xref:System.Double>, und höher in eine <xref:System.String>. Diese Methode übergibt der <xref:System.Windows.Controls.ListBoxItem> auf eine <xref:System.Windows.FontSizeConverter> -Objekt, das konvertiert der <xref:System.Windows.Controls.ContentControl.Content%2A> von einer <xref:System.Windows.Controls.ListBoxItem> mit einer Instanz von <xref:System.Double>. Dieser Wert wird dann wieder als Wert übergeben der <xref:System.Windows.Controls.TextBlock.FontSize%2A> Eigenschaft von der <xref:System.Windows.Controls.TextBlock> Element.  
  
 In diesem Beispiel definiert auch eine zweite benutzerdefinierte Methode, die aufgerufen wird `changeFamily`. Diese Methode konvertiert die <xref:System.Windows.Controls.ContentControl.Content%2A> von der <xref:System.Windows.Controls.ListBoxItem> auf eine <xref:System.String>, und übergibt dann diesen Wert auf die <xref:System.Windows.Controls.TextBlock.FontFamily%2A> Eigenschaft der <xref:System.Windows.Controls.TextBlock> Element.  
  
 Dieses Beispiel wird nicht ausgeführt.  
  
 [!code-csharp[FontSizeConverter#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSizeConverter/CSharp/Window1.xaml.cs#1)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.FontSizeConverter>
