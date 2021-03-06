---
title: '&lt;chunkedCookieHandler&gt;'
ms.date: 03/30/2017
ms.assetid: 7220de45-1d14-4aec-a29e-4a2ea8ac861f
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 193b783e44fe4386d3575e180dc5baa6a7f9a8be
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ltchunkedcookiehandlergt"></a>&lt;chunkedCookieHandler&gt;
Konfiguriert die <xref:System.IdentityModel.Services.ChunkedCookieHandler>. Dieses Element kann nur vorhanden sein, wenn die `mode` Attribut des der `<cookieHandler>` Element ist "Default" oder "Aufgeteilte".  
  
 \<system.identityModel.services >  
\<FederationConfiguration >  
\<"cookiehandler" >  
\<ChunkedCookieHandler >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Chunked||Default" >  
      <chunkedCookieHandler size=xs:int >  
      </chunkedCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|chunkSize|Die maximale Größe in Zeichen, die HTTP-Cookie-Daten für alle HTTP-Cookie. Sie müssen vorsichtig Segmentgröße anpassen können. Webbrowser haben verschiedene Grenzwerte auf die Größe des Cookies und Anzahl pro Domäne zulässig. Die ursprünglichen Netscape-Spezifikation vorgesehenen z. B. diese Grenzwerte: 300 Cookies addieren, 4096 Bytes pro Cookie-Header (einschließlich Metadaten, nicht nur den Cookiewert) und 20 Cookies pro Domäne. Der Standardwert ist 2000. Erforderlich.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keiner  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<"cookiehandler" >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|Konfiguriert die <xref:System.IdentityModel.Services.CookieHandler> , die die <xref:System.IdentityModel.Services.SessionAuthenticationModule> (SAM) zum Lesen und Schreiben von Cookies verwendet.|  
  
## <a name="remarks"></a>Hinweise  
 Geben Sie bei einer <xref:System.IdentityModel.Services.ChunkedCookieHandler> durch Festlegen der `mode` Attribut des der `<cookieHandler>` Element "Default" oder "Chunked", Sie können die Blockgröße, die der Cookie-Handler verwendet wird, zum Lesen und Schreiben von Cookies durch einschließen angeben eine `<chunkedCookieHandler>` untergeordnetes Element und Festlegen der `chunkSize` Attribut. Wenn die `<chunkedCookieHandler>` -Element nicht vorhanden ist, wird die Standardblockgröße 2000 Bytes verwendet. Dieses Element nicht angegeben, wann die `mode` -Attribut auf "Custom" festgelegt ist.  
  
 Die `<chunkedCookieHandler>` Element dargestellt ist, durch die <xref:System.IdentityModel.Services.ChunkedCookieHandlerElement> Klasse.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel konfiguriert einen aufgeteilte Cookie-Handler, der Cookies in Abschnitten von 3000 Bytes schreibt.  
  
```xml  
<cookieHandler mode="Chunked">  
    <chunkedCookieHandler chunkSize=3000/>  
</cookieHandler>  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.IdentityModel.Services.ChunkedCookieHandler>
