---
title: "64-Bit-Anwendungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "64-Bit-Anwendungen [C++]"
  - "64-Bit-Programmierung [C++]"
  - "Anwendungen [C++], 64-Bit"
ms.assetid: fd4026bc-2c3d-4b27-86dc-ec5e96018181
caps.latest.revision: 53
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 53
---
# 64-Bit-Anwendungen
Wenn Sie eine Anwendung kompilieren, können Sie festlegen, dass sie auf einem Windows\-Betriebssystem mit 64 Bit entweder als systemeigene Anwendung oder unter WOW64 \(Windows\-32\-Bit\-On\-Windows\-64\-Bit\) ausgeführt werden soll.  WOW64 ist eine Kompatibilitätsumgebung, die die Ausführung einer 32\-Bit\-Anwendung auf einem 64\-Bit\-System ermöglicht.  WOW64 ist allen in 64\-Bit\-Versionen des Windows\-Betriebssystems enthalten.  
  
## Ausführen von 32\-Bit\-Anwendungen im Vergleich zu64\-Bit\-Anwendungen unter Windows  
 Alle mit den Versionen 1.0 oder 1.1 von .NET Framework erstellten Anwendungen werden auf einem 64\-Bit\-Betriebssystem als 32\-Bit\-Anwendungen behandelt und immer unter WOW64 und der 32\-Bit\-Common Language Runtime \(CLR\) ausgeführt.  32\-Bit\-Anwendungen, die auf [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)] oder höheren Versionen erstellt werden, können auch unter WOW64 auf 64\-Bit\-Systemen ausgeführt werden.  
  
 Visual Studio installiert die 32\-Bit\-Version der CLR auf einem x86\-Computer und sowohl die 32\-Bit\-Version als auch die entsprechende 64\-Bit\-Version der CLR auf einem 64\-Bit\-Windows\-Computer.  \(Da Visual Studio eine 32\-Bit\-Anwendung ist, wenn sie in einem 64\-Bit\-System installiert ist, wird sie unter WOW64 ausgeführt.\)  
  
> [!NOTE]
>  Aufgrund des Designs der x86\-Emulation und des WOW64\-Subsystems für die Itanium\-Prozessorfamilie ist die Ausführung von Anwendungen auf einen Prozessor beschränkt.  Diese Faktoren beeinträchtigen die Leistung und Skalierbarkeit der 32\-Bit\-Version von .NET Framework\-Anwendungen, die unter Itanium\-basierten Systemen ausgeführt werden.  Sie sollten nach Möglichkeit [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)] verwenden, das systemeigene 64\-Bit\-Unterstützung für Itanium\-basierte Systeme zur Verbesserung von Leistung und Skalierbarkeit bietet.  
  
 Wenn Sie eine verwaltete 64\-Bit\-Anwendung auf einem 64\-Bit\-Windows\-Betriebssystem ausführen, können Sie standardmäßig ein Objekt mit einer Größe von maximal 2 Gigabyte \(GB\) erstellen.  In [!INCLUDE[net_v45](../../includes/net-v45-md.md)] können Sie diese Beschränkung aber erhöhen.  Weitere Informationen finden Sie in den Erläuterungen zum [\<gcAllowVeryLargeObjects\>\-Element](../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md).  
  
 Viele Assemblys können sowohl unter der 32\-Bit\-Version als auch der 64\-Bit\-Version der CLR ausgeführt werden.  Allerdings zeigen einige Programme je nach CLR möglicherweise ein anderes Verhalten, wenn Sie eine oder mehrere der folgenden Elemente aufweisen:  
  
-   Strukturen, die Member enthalten, deren Größe sich je nach Plattform ändert \(z. B. jeder beliebige Zeigertyp\).  
  
-   Zeigerarithmetik, die Größen von Konstanten einschließt.  
  
-   Fehlerhafter Plattformaufruf oder COM\-Deklarationen, die `Int32` statt `IntPtr` für Handles verwenden.  
  
-   Code, der `IntPtr` in `Int32` umwandelt.  
  
 Weitere Informationen zum Portieren einer 32\-Bit\-Anwendung auf die 64\-Bit\-CLR finden Sie in der MSDN Library unter [Migrieren von verwaltetem Code \(32 Bit\) zu Code mit 64 Bit](http://go.microsoft.com/fwlink/?LinkId=150542).  
  
## Allgemeine Informationen zur 64\-Bit\-Programmierung  
 Allgemeine Informationen zur 64\-Bit\-Programmierung finden Sie in den folgenden Dokumenten:  
  
-   Weitere Informationen zur 64\-Bit\-Version der CLR auf einem 64\-Bit\-Windows\-Computer finden Sie auf der MSDN\-Website im [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=37079).  
  
-   In der [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)]\-Dokumentation finden Sie unter [Programmierhandbuch für Windows \(64 Bit\)](http://go.microsoft.com/fwlink/p/?LinkId=253512) weitere Informationen.  
  
-   Informationen zum Herunterladen einer 64\-Bit\-Version der CLR finden Sie auf der MSDN\-Website unter [.NET Framework Developer Center – Downloads](http://go.microsoft.com/fwlink/?LinkId=50953).  
  
-   Informationen zur Visual Studio\-Unterstützung für das Erstellen von 64\-Bit\-Anwendungen finden Sie unter [Visual Studio\-IDE\-64\-Bit\-Unterstützung](../Topic/Visual%20Studio%20IDE%2064-Bit%20Support.md).  
  
## Compilerunterstützung für das Erstellen von 64\-Bit\-Anwendungen  
 Wenn Sie .NET Framework verwenden, um eine Anwendung auf einem 32\-Bit\- oder 64\-Bit\-Computer zu erstellen, wird die Anwendung auf einem 64\-Bit\-Computer als systemeigene Anwendung ausgeführt \(d. h. nicht unter WOW64\).  In der folgenden Tabelle werden die Dokumente aufgelistet, die Anweisungen zur Verwendung von Visual Studio\-Compilern für die Erstellung von 64\-Bit\-Anwendungen enthalten, die als systemeigene Anwendungen, unter WOW64 oder in beiden Varianten ausgeführt werden.  
  
|Compiler|Compileroption|  
|--------------|--------------------|  
|Visual Basic|[\/platform](../Topic/-platform%20\(Visual%20Basic\).md)|  
|Visual C\#|[\/platform \(Specify Output Platform\)](../Topic/-platform%20\(C%23%20Compiler%20Options\).md)|  
|Visual C\+\+|Sie können plattformagnostische Microsoft Intermediate Language \(MSIL\)\-Anwendungen erstellen, indem Sie **\/clr:safe** verwenden.  Weitere Informationen finden Sie unter [\/clr \(Common Language Runtime\-Kompilierung\)](../Topic/-clr%20\(Common%20Language%20Runtime%20Compilation\).md).<br /><br /> Visual C\+\+ enthält einen gesonderten Compiler für jedes 64\-Bit\-Betriebssystem.  Weitere Informationen zur Verwendung von Visual C\+\+ für die Erstellung von systemeigenen Anwendungen, die auf einem 64\-Bit\-Windows\-Betriebssystem ausgeführt werden, finden Sie unter [64\-Bit\-Programmierung](http://msdn.microsoft.com/library/h2k70f3s\(v=vs.80\)).|  
  
## Bestimmen des Status einer EXE\- oder DLL\-Datei  
 Um zu bestimmen, ob eine EXE\- oder DLL\-Datei nur auf einer bestimmten Plattform oder unter WOW64 ausgeführt werden soll, verwenden Sie das [CorFlags.exe \(CorFlags Conversion Tool\)](../../docs/framework/tools/corflags-exe-corflags-conversion-tool.md) ohne Optionen.  Weiterhin können Sie mit "CorFlags.exe" auch den Plattformstatus einer EXE\- oder DLL\-Datei ändern.  Im CLR\-Header einer Visual Studio\-Assembly ist die Nummer der Hauptversion der Laufzeit auf 2 und die Nummer der Nebenversion auf 5 festgelegt.  Anwendungen, für die die Nebenversionsnummer der Laufzeit auf 0 festgelegt ist, werden als ältere Anwendungen behandelt und auf 64\-Bit\-Computern unter WOW64 ausgeführt.  
  
 Wenn Sie eine EXE\- oder DLL\-Datei programmgesteuert abfragen möchten, um festzustellen, ob sie nur auf einer bestimmten Plattform oder unter WOW64 ausgeführt werden kann, verwenden Sie die <xref:System.Reflection.Module.GetPEKind%2A?displayProperty=fullName>\-Methode.