---
title: Benutzerdefinierte Lebensdauer
ms.date: 03/30/2017
ms.assetid: 52806c07-b91c-48fe-b992-88a41924f51f
ms.openlocfilehash: e41c970739b8036730fa601433ce7157e01d7e19
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="custom-lifetime"></a>Benutzerdefinierte Lebensdauer
Dieses Beispiel veranschaulicht, wie so schreiben Sie eine Windows Communication Foundation (WCF)-Erweiterung, um benutzerdefinierte Lebensdauerdienste für freigegebene Instanzen von WCF-Dienst bereitzustellen.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
## <a name="shared-instancing"></a>Freigegebene Instanziierung  
 WCF bietet mehrere instanziierungsmodi für Ihre Dienstinstanzen. Der freigegebene Instanziierungsmodus, der in diesem Thema behandelt wird, bietet eine Möglichkeit, eine Dienstinstanz zwischen mehreren Kanälen freizugeben. Clients können entweder die Endpunktadresse der Instanz lokal auflösen oder eine Factorymethode im Dienst kontaktieren, um die Endpunktadresse einer ausgeführten Instanz abzurufen. Sobald die Endpunktadresse vorliegt, kann ein neuer Kanal erstellt und die Kommunikation gestartet werden. Im folgenden Codeausschnitt wird gezeigt, wie eine Clientanwendung einen neuen Kanal zu einer vorhandenen Dienstinstanz erstellt.  
  
```  
// Create the first channel.  
IEchoService proxy = channelFactory.CreateChannel();  
  
// Resolve the instance.  
EndpointAddress epa = ((IClientChannel)proxy).ResolveInstance();  
  
// Create new channel factory with the endpoint address resolved by   
// previous statement.  
ChannelFactory<IEchoService> channelFactory2 =  
                new ChannelFactory<IEchoService>("echoservice",  
                epa);  
  
// Create the second channel to the same instance.  
IEchoService proxy2 = channelFactory2.CreateChannel();  
```  
  
 Der freigegebene Instanziierungsmodus unterscheidet sich von anderen Instanziierungsmodi in seiner einzigartigen Methode zum Freigeben von Dienstinstanzen. Wenn alle Kanäle für eine Instanz geschlossen sind, wird die WCF-Dienstlaufzeit ein Timer gestartet. Wenn niemand eine Verbindung herstellt, bevor das Timeout abläuft, wird WCF die Instanz frei und die Ressourcen. Im Rahmen der beendigungsprozedur ruft WCF die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> -Methode für alle <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> Implementierungen, bevor die Instanz freigegeben. Wenn alle Implementierungen `true` zurückgeben, wird die Instanz freigegeben. Andernfalls ist die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider>-Implementierung dafür zuständig, den `Dispatcher` unter Verwendung einer Rückrufmethode von dem Leerlaufzustand zu benachrichtigen.  
  
 Standardmäßig beträgt der Leerlauftimeoutwert von <xref:System.ServiceModel.InstanceContext> eine Minute. In diesem Beispiel wird jedoch gezeigt, wie Sie diesen Wert erweitern können, indem Sie die benutzerdefinierte Erweiterung verwenden.  
  
## <a name="extending-the-instancecontext"></a>Erweitern von InstanceContext  
 In WCF <xref:System.ServiceModel.InstanceContext> ist der Link zwischen der Dienstinstanz und die `Dispatcher`. WCF können Sie diese Laufzeitkomponente zu erweitern, indem mithilfe des erweiterbaren Objektmusters Zustand "Neu" oder Verhalten hinzufügen. Das erweiterbare Objektmuster wird in WCF verwendet, um vorhandene Laufzeitklassen neue Funktionen zu erweitern oder um neue Zustandsfunktionen zu einem Objekt hinzuzufügen. Es gibt drei Schnittstellen im erweiterbaren Objektmuster: `IExtensibleObject<T>`, `IExtension<T>` und `IExtensionCollection<T>`.  
  
 Die `IExtensibleObject<T>`-Schnittstelle wird von Objekten implementiert, um Erweiterungen zuzulassen, die ihre Funktionalität anpassen.  
  
 Die `IExtension<T>`-Schnittstelle wird von Objekten implementiert, die Erweiterungen von Klassen des Typs `T` sein können.  
  
 Die `IExtensionCollection<T>`-Schnittstelle ist eine Auflistung von `IExtensions`, die das Abrufen von `IExtensions` nach Typ zulässt.  
  
 Aus diesem Grund müssen Sie die <xref:System.ServiceModel.InstanceContext>-Schnittstelle implementieren, um den `IExtension` zu erweitern. In diesem Beispielprojekt enthält die `CustomLeaseExtension`-Klasse diese Implementierung.  
  
```  
class CustomLeaseExtension : IExtension<InstanceContext>  
{  
}  
```  
  
 Die `IExtension`-Schnittstelle verfügt über zwei Methoden: `Attach` und `Detach`. Wie ihre Namen vermuten lassen, werden diese beiden Methoden aufgerufen, wenn die Laufzeit die Erweiterung an eine Instanz der <xref:System.ServiceModel.InstanceContext>-Klasse anfügt oder von der Instanz löst. In diesem Beispiel wird die `Attach`-Methode für die Nachverfolgung des <xref:System.ServiceModel.InstanceContext>-Objekts verwendet, das zur aktuellen Instanz der Erweiterung gehört.  
  
```  
InstanceContext owner;  
  
public void Attach(InstanceContext owner)  
{  
  this.owner = owner;   
}  
```  
  
 Darüber hinaus müssen Sie zur Bereitstellung der erweiterten Lebensdauerunterstützung die erforderliche Implementierung zur Erweiterung hinzufügen. Deswegen wird die `ICustomLease`-Schnittstelle mit den gewünschten Methoden deklariert und in der `CustomLeaseExtension`-Klasse implementiert.  
  
```  
interface ICustomLease  
{  
    bool IsIdle { get; }          
    InstanceContextIdleCallback Callback { get; set; }  
}  
  
class CustomLeaseExtension : IExtension<InstanceContext>, ICustomLease  
{  
}  
```  
  
 Wenn WCF aufruft der <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> Methode in der <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> Implementierung dieser Aufruf an die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> Methode der `CustomLeaseExtension`. Dann überprüft die `CustomLeaseExtension` den privaten Zustand, um festzustellen, ob sich der <xref:System.ServiceModel.InstanceContext> im Leerlauf befindet. Wenn er sich in Leerlauf befindet, wird `true` zurückgegeben. Andernfalls wird ein Zeitgeber für eine bestimmte erweiterte Lebensdauerperiode gestartet.  
  
```  
public bool IsIdle  
{  
  get  
  {  
    lock (thisLock)  
    {  
      if (isIdle)  
      {  
        return true;  
      }  
      else  
      {  
        StartTimer();  
        return false;  
      }  
    }  
  }  
}  
```  
  
 Im `Elapsed`-Ereignis des Zeitgebers wird die Rückruffunktion im Verteiler aufgerufen, um einen weiteren Bereinigungszyklus zu starten.  
  
```  
void idleTimer_Elapsed(object sender, ElapsedEventArgs args)  
{  
    idleTimer.Stop();  
    isIdle = true;    
    callback(owner);  
}  
```  
  
 Der ausgeführte Zeitgeber kann nicht erneuert werden, wenn eine neue Nachricht für die Instanz eingeht, die in den Leerlaufzustand verschoben wird.  
  
 Im Beispiel wird <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> implementiert, um die Aufrufe der <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A>-Methode abzufangen und diese zur `CustomLeaseExtension` weiterzuleiten. Die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider>-Implementierung ist in der `CustomLifetimeLease`-Klasse enthalten. Die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> Methode wird aufgerufen, wenn WCF Begriff ist, die Dienstinstanz freizugeben. Es gibt jedoch nur eine Instanz einer bestimmten `ISharedSessionInstance`-Implementierung in der <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider>-Auflistung von ServiceBehavior. Das bedeutet, dass es keine Möglichkeit, zu wissen, die <xref:System.ServiceModel.InstanceContext> geschlossen wird, die zum Zeitpunkt der WCF überprüft die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> Methode. Aus diesem Grund werden Anforderungen der <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A>-Methode in diesem Beispiel mit der Threadsperre serialisiert.  
  
> [!IMPORTANT]
>  Die Verwendung der Threadsperre wird nicht empfohlen, da die Leistung der Anwendung durch die Serialisierung deutlich beeinträchtigt werden kann.  
  
 Eine private Membervariable wird in der `CustomLeaseExtension`-Klasse verwendet, um den `IsIdle`-Wert nachzuverfolgen. Jedes Mal, wenn der Wert von <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> abgerufen wird, wird der private `IsIdle`-Member zurückgegeben und auf `false` zurückgesetzt. Dieser Wert muss auf `false` festgelegt werden, um sicherzustellen, dass der Verteiler die <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A>-Methode aufruft.  
  
```  
public bool IsIdle  
{  
    get   
    {  
       lock (thisLock)  
       {  
           bool idleCopy = isIdle;  
           isIdle = false;  
           return idleCopy;  
       }  
    }  
}  
```  
  
 Wenn die `ISharedSessionLifetime.IsIdle`-Eigenschaft `false` zurückgibt, registriert der Verteiler mithilfe der `NotifyIdle`-Methode eine Rückruffunktion. Diese Methode empfängt einen Verweis darauf, dass <xref:System.ServiceModel.InstanceContext> freigegeben wird. Daher kann der Beispielcode die Erweiterung des Typs `ICustomLease` abfragen und die `ICustomLease.IsIdle`-Eigenschaft im erweiterten Zustand überprüfen.  
  
```  
public void NotifyIdle(InstanceContextIdleCallback callback,   
            InstanceContext instanceContext)  
{  
    lock (thisLock)  
    {  
       ICustomLease customLease =  
           instanceContext.Extensions.Find<ICustomLease>();  
       customLease.Callback = callback;   
       isIdle = customLease.IsIdle;  
       if (isIdle)  
       {  
             callback(instanceContext);  
       }  
    }   
}  
```  
  
 Bevor die `ICustomLease.IsIdle`-Eigenschaft überprüft wird, muss die Rückrufeigenschaft festgelegt werden, damit die `CustomLeaseExtension` den Verteiler benachrichtigen kann, sobald sie in den Leerlauf wechselt. Wenn `ICustomLease.IsIdle` `true` zurückgibt, wird der private `isIdle`-Member einfach in `CustomLifetimeLease` auf `true` festgelegt, und die Rückrufmethode wird vom Member aufgerufen. Da im Code eine Sperre enthalten ist, können andere Threads den Wert dieses privaten Members nicht ändern. Wenn der Verteiler das nächste Mal die `ISharedSessionLifetime.IsIdle`-Eigenschaft überprüft, gibt sie `true` zurück, und der Verteiler kann die Instanz freigeben.  
  
 Jetzt da die Vorarbeit für die benutzerdefinierte Erweiterung abgeschlossen ist, muss sie in das Dienstmodell eingebunden werden. Zum Einbinden der `CustomLeaseExtension` -Implementierung, die die <xref:System.ServiceModel.InstanceContext>, WCF bietet die <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> Schnittstelle, um das bootstrapping von ausführen <xref:System.ServiceModel.InstanceContext>. In diesem Beispiel implementiert die `CustomLeaseInitializer`-Klasse diese Schnittstelle und fügt eine `CustomLeaseExtension`-Instanz zur <xref:System.ServiceModel.InstanceContext.Extensions%2A>-Auflistung aus der einzigen Methodeninitialisierung hinzu. Diese Methode wird vom Verteiler aufgerufen, während <xref:System.ServiceModel.InstanceContext> initialisiert wird.  
  
```  
public void Initialize(InstanceContext instanceContext, Message message)  
{  
  IExtension<InstanceContext> customLeaseExtension =  
    new CustomLeaseExtension(timeout);  
  instanceContext.Extensions.Add(customLeaseExtension);  
}  
```  
  
 Schließlich die `System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime` und <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> Implementierungen sind ist hakenförmigen bis zu das Dienstmodell mithilfe der <xref:System.ServiceModel.Description.IServiceBehavior> Implementierung. Diese Implementierung wird in der `CustomLeaseTimeAttribute`-Klasse eingefügt, und sie wird außerdem von der `Attribute`-Basisklasse abgeleitet, um dieses Verhalten als Attribut verfügbar zu machen. In der `IServiceBehavior.ApplyBehavior`-Methode werden Instanzen von der <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer>-Implementierung und der `System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime`-Implementierung zu der `System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextLifetimes`-Auflistung bzw. der <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextInitializers%2A>-Auflistung von <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> hinzugefügt.  
  
```  
public void ApplyBehavior(ServiceDescription description,   
           ServiceHostBase serviceHostBase,   
           Collection<DispatchBehavior> behaviors,  
           Collection<BindingParameterCollection> parameters)  
{  
    CustomLifetimeLease customLease = new CustomLifetimeLease();  
    CustomLeaseInitializer initializer =   
                new CustomLeaseInitializer(timeout);  
  
    foreach (DispatchBehavior dispatchBehavior in behaviors)  
    {  
        dispatchBehavior.InstanceContextLifetimes.Add(customLease);  
        dispatchBehavior.InstanceContextInitializers.Add(initializer);  
    }  
}  
```  
  
 Dieses Verhalten kann einer Beispieldienstklasse hinzugefügt werden, indem es mit dem `CustomLeaseTime`-Attribut kommentiert wird.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Shareable)]  
[CustomLeaseTime(Timeout = 20000)]  
public class EchoService : IEchoService  
{  
  //…  
}  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Dienst- und Clientkonsolenfenster angezeigt. Drücken Sie die EINGABETASTE in den einzelnen Konsolenfenstern, um den Dienst und den Client zu schließen.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Setupprozedur für die Windows Communication Foundation-Beispiele zum einmaligen](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Um die C#- oder Visual Basic .NET-Edition der Projektmappe zu erstellen, befolgen Sie die unter [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)aufgeführten Anweisungen.  
  
3.  Um das Beispiel in einer einzelnen oder computerübergreifenden Konfiguration ausführen möchten, folgen Sie den Anweisungen [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Lifetime`  
  
## <a name="see-also"></a>Siehe auch
