---
title: 'Vorgehensweise: Abrufen aller Fenster in einer Anwendung'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- window objects [WPF], getting
ms.assetid: f120f06e-993b-4a97-9657-af0d1986981f
ms.openlocfilehash: 476905899f5f7d573a16ba876c72f28ea34bbf9d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-get-all-windows-in-an-application"></a>Vorgehensweise: Abrufen aller Fenster in einer Anwendung
In diesem Beispiel wird gezeigt, wie alle abzurufenden <xref:System.Windows.Window> Objekte in einer Anwendung.  
  
## <a name="example"></a>Beispiel  
 Jede instanziiert <xref:System.Windows.Window> Objekt sichtbar oder nicht, wird automatisch hinzugefügt, um eine Auflistung von Fensterverweisen, die von verwalteten <xref:System.Windows.Application>, und von verfügbar gemachten <xref:System.Windows.Application.Windows%2A>.  
  
 Sie können auflisten <xref:System.Windows.Application.Windows%2A> abzurufenden alle instanziierten Windows mithilfe des folgenden Codes:  
  
 [!code-csharp[HOWTOWindowManagementSnippets#GetAllWindows](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/CustomWindow.xaml.cs#getallwindows)]
 [!code-vb[HOWTOWindowManagementSnippets#GetAllWindows](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/customwindow.xaml.vb#getallwindows)]
