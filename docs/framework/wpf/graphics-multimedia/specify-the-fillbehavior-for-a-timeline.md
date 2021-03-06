---
title: 'Gewusst wie: Festlegen von FillBehavior für ein Timeline-Objekt, das das Ende des aktiven Zeitraums erreicht hat'
ms.date: 03/30/2017
helpviewer_keywords:
- FillBehavior property for inactive timelines [WPF]
- Timelines [WPF], FillBehavior property
ms.assetid: db805f59-d513-4dac-af15-47005dae3199
ms.openlocfilehash: 947be09140dc2d1d5e130ccb74472d8dce3408cb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-specify-the-fillbehavior-for-a-timeline-that-has-reached-the-end-of-its-active-period"></a>Gewusst wie: Festlegen von FillBehavior für ein Timeline-Objekt, das das Ende des aktiven Zeitraums erreicht hat
In diesem Beispiel wird gezeigt, wie an den <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> für die inaktiven <xref:System.Windows.Media.Animation.Timeline> einer animierten Eigenschaft.  
  
## <a name="example"></a>Beispiel  
 Die <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> Eigenschaft eine <xref:System.Windows.Media.Animation.Timeline> bestimmt, was auf den Wert einer animierten Eigenschaft geschieht, wenn es nicht gerade animiert, d. h., wenn die <xref:System.Windows.Media.Animation.Timeline> ist inaktiv, aber die übergeordneten <xref:System.Windows.Media.Animation.Timeline> befindet sich innerhalb einer aktiven oder haltezeitraum befindet. Beispielsweise bleibt eine animierte Eigenschaft an deren Ende Wert nach der Animation beendet oder es ist, den Wert vor der Animation gestartet wiederherstellen?  
  
 Im folgenden Beispiel wird eine <xref:System.Windows.Media.Animation.DoubleAnimation> zum Animieren der <xref:System.Windows.FrameworkElement.Width%2A> zweier Rechtecke. Jedes Rechteck verwendet ein anderes <xref:System.Windows.Media.Animation.Timeline> Objekt.  
  
 Eine <xref:System.Windows.Media.Animation.Timeline> hat eine <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> festgelegt <xref:System.Windows.Media.Animation.FillBehavior.Stop>, die bewirkt, dass der Breite des Rechtecks, das auf die nicht animiert wiederherstellen Wert der <xref:System.Windows.Media.Animation.Timeline> endet. Die andere <xref:System.Windows.Media.Animation.Timeline> verfügt über eine <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> von <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>, dies bedeutet, dass die Breite an deren Ende bleiben Wert der <xref:System.Windows.Media.Animation.Timeline> endet.  
  
 [!code-xaml[timingbehaviors_snip#FillBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/FillBehaviorExample.xaml#fillbehaviorwholepage)]  
  
 Das vollständige Beispiel finden Sie unter [Beispielsammlung](http://go.microsoft.com/fwlink/?LinkID=159969).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Media.Animation.DoubleAnimation>  
 <xref:System.Windows.FrameworkElement.Width%2A>  
 <xref:System.Windows.Media.Animation.Timeline>  
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>  
 <xref:System.Windows.Media.Animation.FillBehavior.Stop>  
 <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>  
 [Übersicht über Animationen](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)  
 [Animation und zeitlichen Steuerung](http://msdn.microsoft.com/library/7d83765b-d5ae-41b1-b423-80206e1124aa)  
 [Themen zu Vorgehensweisen](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)
