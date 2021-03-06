---
title: Verfügbarmachen von .NET Framework-Komponenten in COM
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
ms.assetid: e42a65f7-1e61-411f-b09a-aca1bbce24c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f11928388dba9b0e9b442578bfb7b6f751c2e172
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="exposing-net-framework-components-to-com"></a>Verfügbarmachen von .NET Framework-Komponenten in COM
Das Schreiben eines .NET-Typs und das Verwenden dieses Typs von nicht verwaltetem Code sind unterschiedliche Aktivitäten für Entwickler. Dieser Abschnitt beschreibt einige Tipps zum Schreiben von verwaltetem Code, der mit COM-Clients interagiert:  
  
-   [Qualifizieren von .NET-Typen für die Interoperation](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md).  
  
     Alle verwalteten Typen, Methoden, Eigenschaften, Felder und Ereignisse, die für COM verfügbar gemacht werden sollen, müssen öffentlich sein. Typen müssen über einen öffentlichen Standardkonstruktor verfügen, da dies der einzige Konstruktor ist, der über COM aufgerufen werden kann.  
  
-   [Anwenden von Interop-Attributen](../../../docs/framework/interop/applying-interop-attributes.md).  
  
     Benutzerdefinierte Attribute in verwaltetem Code können die Interoperabilität einer Komponente verbessern.  
  
-   [Verpacken einer Assembly für COM](../../../docs/framework/interop/packaging-an-assembly-for-com.md).  
  
     COM-Entwickler fordern möglicherweise, dass Sie die Schritte für Verweise und die Bereitstellung Ihrer Assemblys zusammenfassen.  
  
 Darüber hinaus werden in diesem Abschnitt die Aufgaben im Zusammenhang mit der Nutzung eines verwalteten Typs von einem COM-Client beschrieben.  
  
#### <a name="to-consume-a-managed-type-from-com"></a>Nutzen eines verwalteten Typs von COM  
  
1.  [Registrieren von Assemblys bei COM](../../../docs/framework/interop/registering-assemblies-with-com.md).  
  
     Typen in einer Assembly (und Typbibliotheken) müssen zur Entwurfszeit registriert werden. Wenn ein Installer die Assembly nicht registriert, weisen Sie die COM-Entwickler zur Nutzung von Regasm.exe an.  
  
2.  [Verweisen auf .NET-Typen in COM](../../../docs/framework/interop/how-to-reference-net-types-from-com.md).  
  
     COM-Entwickler können auf Typen in einer Assembly verweisen, indem sie dieselben Tools und Techniken nutzen, die sie heute bereits verwenden.  
  
3.  [Aufrufen eines .NET-Objekts](https://msdn.microsoft.com/library/40c9626c-aea6-4bad-b8f0-c1de462efd33(v=vs.100)).  
  
     COM-Entwickler können Methoden so für das .NET-Objekt aufrufen, wie sie Methoden für alle nicht verwalteten Typen aufrufen. Z.B. aktiviert die COM-API **CoCreateInstance** .NET-Objekte.  
  
4.  [Bereitstellen einer Anwendung für COM-Zugriff](https://msdn.microsoft.com/library/fb63564c-c1b9-4655-a094-a235625882ce(v=vs.100)).  
  
     Eine Assembly mit starkem Namen kann im globalen Assemblycache installiert werden und erfordert eine Signatur des Herausgebers. Assemblys, die keinen starken Namen haben, müssen im Anwendungsverzeichnis des Clients installiert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Interoperabilität mit nicht verwaltetem Code](../../../docs/framework/interop/index.md)  
 [COM-Interop-Beispiel: COM-Client und .NET-Server](../../../docs/framework/interop/com-interop-sample-com-client-and-net-server.md)
