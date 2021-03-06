---
title: '&lt;issuerTokenResolver&gt;'
ms.date: 03/30/2017
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 646833f277c3ef4675a835ca0af3daf647e01224
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ltissuertokenresolvergt"></a>&lt;issuerTokenResolver&gt;
Registriert die Aussteller-Resolver, die vom Handler in der Auflistung Tokenhandler verwendet wird. Die Aussteller-tokenresolver wird zum Auflösen von der signiertokens für eingehende Token und Nachrichten verwendet.  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<SecurityTokenHandlers >  
\<SecurityTokenHandlerConfiguration >  
\<IssuerTokenResolver >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|Typ|Gibt den Typ des Ausstellers token Konfliktlösers. Muss entweder der <xref:System.IdentityModel.Tokens.IssuerTokenResolver> Klasse oder ein Typ, der von abgeleitet ist die <xref:System.IdentityModel.Tokens.IssuerTokenResolver> Klasse. Erforderlich.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keiner  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<SecurityTokenHandlerConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Ermöglicht die Konfiguration für eine Auflistung der Tokenhandler.|  
  
## <a name="remarks"></a>Hinweise  
 Die Aussteller-tokenresolver wird zum Auflösen von der signiertokens für eingehende Token und Nachrichten verwendet. Es wird verwendet, um das kryptografische Material abzurufen, das für die Überprüfung der Signatur verwendet wird. Sie müssen angeben, die `type` Attribut. Der angegebene Typ kann entweder <xref:System.IdentityModel.Tokens.IssuerTokenResolver> oder einen benutzerdefinierten Typ abgeleitet, die die <xref:System.IdentityModel.Tokens.IssuerTokenResolver> Klasse.  
  
 Einige Tokenhandler können Sie token konfliktlösungseinstellungen der Aussteller in der Konfiguration angeben. Einstellungen für einzelne Tokenhandler überschreiben für die Sicherheit Tokenhandler Auflistung angegebenen.  
  
> [!NOTE]
>  Angeben der `<issuerTokenResolver>` Element als untergeordnetes Element von der [ \<IdentityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) Element wurde als veraltet markiert, aber noch für die Abwärtskompatibilität unterstützt. Einstellungen auf der `<securityTokenHandlerConfiguration>` Element, überschreiben Sie die auf die `<identityConfiguration>` Element.  
  
## <a name="example"></a>Beispiel  
 Das folgende XML zeigt die Konfiguration für einen Aussteller-Resolver, der für eine benutzerdefinierte Klasse basiert, die abgeleitet <xref:System.IdentityModel.Tokens.IssuerTokenResolver>. Die tokenresolver verwaltet ein Wörterbuch der Zielgruppe-Schlüssel-Paare, die von einem benutzerdefinierten Konfiguration-Element initialisiert wird (`<AddAudienceKeyPair>`) für die Klasse definiert. Die Klasse überschreibt die <xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A> Methode, um dieses Element zu verarbeiten. Die Außerkraftsetzung wird im folgenden Beispiel gezeigt; Allerdings werden die aufgerufenen Methoden aus Gründen der Übersichtlichkeit nicht angezeigt. Das vollständige Beispiel finden Sie unter der `CustomToken` Beispiel.  
  
```xml  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## <a name="example"></a>Beispiel  
  
```  
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.IdentityModel.Tokens.IssuerTokenResolver>
