---
title: Implementieren des RangeValue-Steuerelementmusters der Benutzeroberflächenautomatisierung
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Range Value
- Range Value control pattern
- UI Automation, Range Value control pattern
ms.assetid: 225feaa4-918e-418b-938e-7389338d0a69
author: Xansky
ms.author: mhopkins
manager: markl
ms.openlocfilehash: 219f460906d2892ae6cd76d13a2b17378e02b9b7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="implementing-the-ui-automation-rangevalue-control-pattern"></a>Implementieren des RangeValue-Steuerelementmusters der Benutzeroberflächenautomatisierung
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]-Klassen verwenden möchten, die im <xref:System.Windows.Automation>-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]finden Sie auf der Seite zur [Windows-Automatisierungs-API: UI-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Dieses Thema enthält Richtlinien und Konventionen für das Implementieren von <xref:System.Windows.Automation.Provider.IRangeValueProvider>, einschließlich Informationen über Ereignisse und Eigenschaften. Links zu zusätzlichen Referenzen sind am Ende dieses Themas aufgelistet.  
  
 Das <xref:System.Windows.Automation.RangeValuePattern> -Steuerelementmuster dient zur Unterstützung von Steuerelementen, die auf einen Wert innerhalb eines Bereichs festgelegt werden können. Beispiele für Steuerelemente, die dieses Steuerelementmuster implementieren, finden Sie unter [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Implementierungsrichtlinien und -konventionen  
 Beachten Sie beim Implementieren des RangeValue-Steuerelementmusters die folgenden Richtlinien und Konventionen:  
  
-   Steuerelemente lassen eine erneute Kalibrierung der unterstützten Eigenschaften auf Grundlage des Gebietsschemas oder einer Benutzereinstellung zu. Ein Beispiel hierfür ist ein Thermometersteuerelement, das so festgelegt werden kann, dass die Temperatur in Fahrenheit oder Celsius angezeigt wird.  
  
-   Für Steuerelemente, die über mehrdeutige Bereichswerte verfügen, z. B. Statusanzeigen oder Schieberegler, sollten diese Werte normalisiert werden.  
  
 ![Statusanzeige auf. ] (../../../docs/framework/ui-automation/media/uia-rangevaluepattern-progress-bar.PNG "UIA_RangeValuePattern_Progress_Bar")  
Beispiel für eine Statusanzeige, in der der Wert eine ganze Zahl ist und die minimalen und maximalen Eigenschaftswerte auf 0 (null) beziehungsweise 100 normalisiert werden  
  
<a name="Required_Members_for_the_IRangeValueProvider"></a>   
## <a name="required-members-for-irangevalueprovider"></a>Erforderliche Member für „IRangeValueProvider“  
  
|Erforderliche Member|Memberart|Hinweise|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.LargeChangeProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.SmallChangeProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.MaximumProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>|Eigenschaft|Keiner|  
|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A>|Methoden|Keiner|  
  
 Diesem Steuerelementmuster sind keine Ereignisse zugeordnet.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Ausnahmen  
 Anbieter müssen die folgenden Ausnahmen auslösen.  
  
|Ausnahmetyp|Bedingung|  
|--------------------|---------------|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A> wird mit einem Wert aufgerufen, der entweder größer als <xref:System.Windows.Automation.RangeValuePattern.MaximumProperty> oder kleiner als <xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Steuerelementmuster für Benutzeroberflächenautomatisierung](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [Unterstützung von Steuerelementmustern in einem Benutzeroberflächenautomatisierungs-Anbieter](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)  
 [Steuerelementmuster für Benutzeroberflächenautomatisierung für Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)  
 [Übersicht über die Benutzeroberflächenautomatisierungs-Struktur](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
 [Verwenden der Zwischenspeicherung in der Benutzeroberflächenautomatisierung](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
