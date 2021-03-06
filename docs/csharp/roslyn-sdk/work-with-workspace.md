---
title: Arbeiten mit dem Arbeitsbereichsmodell für .NET Compiler Platform SDK
description: In dieser Übersicht werden die Typen vorgestellt, die Sie zum Abfragen und Bearbeiten von Arbeitsbereichen und Projekten für Ihren Code verwenden.
author: billwagner
ms.author: wiwagn
ms.date: 10/15/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: c42795346c505f925c0b4cb232325085fa065201
ms.sourcegitcommit: b750a8e3979749b214e7e10c82efb0a0524dfcb1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2018
---
# <a name="work-with-a-workspace"></a>Arbeiten mit einem Arbeitsbereich

Die Ebene des **Arbeitsbereichs** stellt einen Startpunkt für die Codeanalyse und das Refactoring ganzer Projektmappen dar. Auf dieser Ebene unterstützt Sie die Arbeitsbereich-API bei der Aufteilung der Informationen zu den Projekten in einer Projektmappe in einzelne Objektmodelle. Sie gewährt Ihnen direkten Zugriff auf die Objektmodelle auf Compilerebene wie Quelltext, Syntaxstrukturen, Semantikmodelle und Kompilierungen, ohne dabei Dateien zu analysieren, Optionen zu konfigurieren oder Abhängigkeit zwischen einzelnen Projekten zu verwalten. 

Hostumgebungen wie eine IDE stellen einen Arbeitsbereich für zugehörige geöffnete Projektmappen zur Verfügung. Außerdem kann dieses Modell außerhalb einer IDE verwendet werden, wenn Sie eine Projektmappendatei laden.

## <a name="workspace"></a>Arbeitsbereich

Bei einem Arbeitsbereich handelt es sich um eine aktive Darstellung Ihrer Projektmappe als Auflistung von Projekten, die alle Auflistungen von Dokumenten enthalten. Arbeitsbereiche werden in der Regel an Hostumgebungen gebunden, die sich stetig verändern, während ein Benutzer eine Eingabe macht oder Eigenschaften verändert. 

Der <xref:Microsoft.CodeAnalysis.Workspace> stellt Zugriff auf das aktuelle Projektmappenmodell zur Verfügung. Wenn in der Hostumgebung eine Änderung vorgenommen wird, löst der Arbeitsbereich passende Ereignisse aus, und die <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType>-Eigenschaft wird aktualisiert. Wenn z.B. der Benutzer in einem Text-Editor eine Eingabe macht, die einem der Quelldokumente entspricht, verwendet der Arbeitsbereich ein Ereignis, um zu signalisieren, dass das gesamte Modell einer Projektmappe geändert wurde und welches Dokument geändert wurde. Sie können dann mit diesen Änderungen umgehen, indem Sie das neue Modell auf Richtigkeit prüfen, wobei wichtige Bereiche hervorgehoben werden oder Sie Vorschläge für Codeänderungen machen. 

Außerdem können Sie eigenständige Arbeitsbereiche erstellen, deren Verbindung mit der Hostumgebung getrennt wird, oder die in einer Anwendung ohne Hostumgebung verwendet werden.

## <a name="solutions-projects-documents"></a>Projektmappen, Projekte, Dokumente

Obwohl Arbeitsbereiche sich jedes Mal verändern können, wenn eine Taste gedrückt wird, können Sie mit einem separaten Modell der Projektmappe arbeiten. 

Bei einer Projektmappe handelt es sich um ein nicht veränderbares Modell des Projekts und der Dokumente. Das bedeutet, dass das Modell ohne Sperren oder Duplikate freigegeben werden kann. Sobald Sie eine Projektmappeninstanz von der <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType>-Eigenschaft erhalten haben, wird diese Instanz nicht mehr verändert. Trotzdem können Sie wie bei Syntaxstrukturen und Kompilierungen Projektmappen verändern, indem Sie neue Instanzen basierend auf bereits vorhandenen Projektmappen und bestimmten Änderungen erstellen. Damit der Arbeitsbereich Ihre Änderungen anzeigt, müssen Sie die veränderte Projektmappe explizit auf den Arbeitsbereich anwenden.

Projekte sind Bestandteile des gesamten nicht veränderbaren Projektmappenmodells. Sie stellen alle Quellcodedokumente, Analysen und Kompilierungsoptionen sowie Assemblyverweise und Verweise zwischen den einzelnen Projekten dar. Über ein Projekt können Sie auf die zugehörige Kompilierung zugreifen. Dabei müssen Sie keine Projektabhängigkeiten festlegen oder Quelldateien analysieren.

Dokumente sind ebenfalls Bestandteile des gesamten nicht veränderbaren Projektmappenmodells. Dokumente stellen einzelne Quelldateien dar, über die Sie auf den Text in der Datei, die Syntaxstruktur und das Semantikmodell zugreifen können.

Im folgenden Diagramm wird deutlich, in welcher Beziehung der Arbeitsbereich zu der Hostumgebung und den Tools steht und wie Bearbeitungen vorgenommen werden.

![Die Beziehungen zwischen verschiedenen Elementen eines Arbeitsbereichs, der Projekte und Quelldateien enthält](media/work-with-workspace/workspace-obj-relations.png)

## <a name="summary"></a>Zusammenfassung

Roslyn stellt mehrere Compiler-APIs und Arbeitsbereich-APIs zur Verfügung, die umfangreiche Informationen über Ihren Quellcode zur Verfügung stellen und uneingeschränkt mit den Sprachen C# und Visual Basic zusammenarbeiten.  Das .NET Compiler Platform SDK vereinfacht die Erstellung von codeabhängigen Tools und Anwendungen um ein Vielfaches. Es schafft zahlreiche Innovationsmöglichkeiten in Bereichen wie etwa folgenden: Metaprogrammierung, Codegenerierung und -transformation, interaktive Nutzung der C#- und VB-Sprachen und Einbettung von C# und VB in domänenspezifischen Sprachen.  
