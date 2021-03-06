---
title: Serviceorientierte Architektur
description: ".NET-Microservicesarchitektur für .NET-Containeranwendungen | Serviceorientierte Architektur"
keywords: Docker, Microservices, ASP.NET, Container
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 6a5f0f53f4208c9944adea33fe1aa3f35fed81ab
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="service-oriented-architecture"></a>Serviceorientierte Architektur 

Der Begriff „serviceorientierte Architektur“ (SOA) wurde zu häufig verwendet und hat daher verschiedene Bedeutungen entwickelt. Der gemeinsame Nenner der Bedeutung von „serviceorientierter Architektur“ ist jedoch, dass die Anwendung strukturiert wird, indem sie in mehrere Dienste zerlegt wird (meistens HTTP-Dienste), die als unterschiedliche Typen klassifiziert werden können, z.B. Subsysteme oder Ebenen.

Diese Dienste können nun als Docker-Container bereitgestellt werden. Dadurch werden Bereitstellungsprobleme gelöst, da alle Abhängigkeiten im Containerimage enthalten sind. Wenn Sie jedoch SOA-Anwendungen hochskalieren müssen, können Probleme mit der Skalierbarkeit und Verfügbarkeit auftreten, wenn Sie die Bereitstellung auf Grundlage eines einzelnen Docker-Hosts durchführen. Hierbei kann Docker-Clusteringsoftware oder ein Orchestrator Sie unterstützen. Dies wird in den folgenden Abschnitten erläutert, in denen Ansätze für die Bereitstellung von Microservices beschrieben werden.

Für herkömmliche serviceorientierte Architekturen und erweiterte Microservicesarchitekturen sind Docker-Container nützlich, jedoch nicht erforderlich.

Microservices werden von serviceorientierten Architekturen abgeleitet, die sich jedoch von Microservicesarchitekturen unterscheiden. Features wie große zentrale Broker, zentrale Orchestratoren auf Organisationsebene und der [Enterprise Service Bus (ESB)](https://en.wikipedia.org/wiki/Enterprise_service_bus) sind typisch für serviceorientierte Architekturen. In den meisten Fällen sind diese Muster in der Microservicescommunity jedoch nicht beliebt. Einige Benutzer argumentieren, dass die Microservicesarchitektur die geglückte Form der serviceorientierten Architektur sei.

Der Schwerpunkt dieses Handbuchs liegt auf Microservices, da der SOA-Ansatz weniger ausführlich als die Anforderungen und Techniken ist, die in Microservicesarchitekturen verwendet werden. Wenn Sie eine auf Microservices basierte Anwendung erstellen können, können Sie ebenfalls eine einfachere, serviceorientierte Anwendung erstellen.




>[!div class="step-by-step"]
[Zurück] (docker-application-state-data.md) [Weiter] (microservices-architecture.md)
