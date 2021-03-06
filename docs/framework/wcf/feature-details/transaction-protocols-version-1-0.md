---
title: Transaktionsprotokolle, Version 1.0
ms.date: 03/30/2017
ms.assetid: 034679af-0002-402e-98a8-ef73dcd71bb6
ms.openlocfilehash: d510a74560369a132822e980e7812ca4deff55a3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="transaction-protocols-version-10"></a>Transaktionsprotokolle, Version 1.0
Windows Communication Foundation (WCF) Version 1 implementiert Version 1.0 der Protokolle WS-Atomic Transaction und WS-Coordination. Weitere Informationen zu Version 1.1, finden Sie unter [Transaktionsprotokolle](../../../../docs/framework/wcf/feature-details/transaction-protocols.md).  
  
|Spezifikation/Dokument|Link|  
|-----------------------------|----------|  
|WS-Coordination|http://msdn.microsoft.com/ws/2005/08/ws-coordination/|  
|WS-AtomicTransaction|http://msdn.microsoft.com/ws/2005/08/ws-atomictransaction/|  
  
 Die Interoperabilität für diese Protokolle ist für zwei Ebenen erforderlich: zwischen Anwendungen und zwischen Transaktions-Managern (siehe folgende Abbildung). In den Spezifikationen werden die Nachrichtenformate und der Nachrichtenaustausch für beide Interoperabilitätsebenen ausführlich beschrieben. Bestimmte Sicherheits- und Zuverlässigkeitsstufen sowie Codierungen gelten für einen Austausch von Anwendung zu Anwendung wie bei einem normalen Anwendungsaustausch. Für eine erfolgreiche Interoperabilität zwischen den Transaktions-Managern ist eine Einigung auf eine bestimmte Bindung erforderlich, weil diese in der Regel nicht vom Benutzer konfiguriert wird.  
  
 In diesem Thema wird die Verbindung der WS-Atomic-Transaktion (WS-AT)-Spezifikation und der Sicherheitsfunktion beschrieben. Außerdem wird die für eine Kommunikation zwischen den Transaktions-Managern verwendete sichere Bindung beschrieben. Der in diesem Dokument beschriebene Ansatz wurde erfolgreich mit anderen Implementierungen von WS-AT und WS-Coordination getestet, u.&#160;a. IBM, IONA und Sun Microsystems.  
  
 In der folgenden Abbildung wird die Interoperabilität zwischen zwei Transaktions-Managern beschrieben, Transaktions-Manager 1 und Transaktions-Manager 2, sowie zwischen zwei Anwendungen, Anwendung 1 und Anwendung 2.  
  
 ![Transaktionsprotokolle](../../../../docs/framework/wcf/feature-details/media/transactionmanagers.gif "Transaktionsergebnis")  
  
 Betrachten Sie ein typisches WS-Coordination/WS-Atomic-Transaktionsszenario mit einem Initiator (I) und einem Teilnehmer (P). Sowohl Initiator als auch Teilnehmer verfügen über Transaktions-Manager (ITM und PTM). In diesem Thema wird das Zweiphasen-Commit als 2PC bezeichnet.  
  
|||  
|-|-|  
|1. CreateCoordinationContext|12. Anwendungsnachrichtenantwort|  
|2. CreateCoordinationContextResponse|13. Commit (Abschluss)|  
|3. Register (Abschluss)|14. Prepare (2PC)|  
|4. RegisterResponse|15. Prepare (2PC)|  
|5. Anwendungsnachricht|16. Prepared (2PC)|  
|6. CreateCoordinationContext mit Kontext|17. Prepared (2PC)|  
|7. Register (Durable)|18. Commit ausgeführt (Abschluss)|  
|8. RegisterResponse|19. Commit (2PC)|  
|9. CreateCoordinationContextResponse|20. Commit (2PC)|  
|10. Register (Durable)|21. Commit ausgeführt (2PC)|  
|11. RegisterResponse|22. Commit ausgeführt (2PC)|  
  
 In diesem Dokument wird die Verbindung der WS-Atomic-Transaktion (WS-AT)-Spezifikation und der Sicherheitsfunktion beschrieben. Außerdem wird die für eine Kommunikation zwischen den Transaktions-Managern verwendete sichere Bindung beschrieben. Der in diesem Dokument beschriebene Ansatz wurde erfolgreich mit anderen Implementierungen von WS-AT und WS-Coordination getestet.  
  
 In der Abbildung und in der Tabelle werden vier Nachrichtenklassen vom Standpunkt der Sicherheit dargestellt:  
  
-   Aktivierungsnachrichten (CreateCoordinationContext und CreateCoordinationContextResponse).  
  
-   Registrierungsnachrichten (Register und RegisterResponse)  
  
-   Protokollnachrichten (Prepare, Rollback, Commit, Aborted usw.).  
  
-   Anwendungsnachrichten.  
  
 Die ersten drei Nachrichten werden als Transaktions-Manager-Nachrichten betrachtet, deren Bindungskonfiguration weiter unten in diesem Thema unter "Anwendungsnachrichtenaustausch" behandelt wird. Bei der vierten Klasse von Nachrichten handelt es sich um Nachrichten von Anwendung zu Anwendung, die weiter unten in diesem Thema im Abschnitt "Nachrichtenbeispiele" beschrieben werden. Dieser Abschnitt beschreibt die protokollbindungen für jede dieser Klassen von WCF verwendet.  
  
 Die folgenden XML-Namespaces und zugeordneten Präfixe werden in diesem Thema verwendet.  
  
|Präfix|Namespace-URI|  
|------------|-------------------|  
|s11|http://schemas.xmlsoap.org/soap/envelope|  
|wsa|http://www.w3.org/2004/08/addressing|  
|wscoor|http://schemas.xmlsoap.org/ws/2004/10/wscoor|  
|wsat|http://schemas.xmlsoap.org/ws/2004/10/wsat|  
|t|http://schemas.xmlsoap.org/ws/2005/02/trust|  
|o|http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd|  
|xsd|http://www.w3.org/2001/XMLSchema|  
  
## <a name="transaction-manager-bindings"></a>Transaktions-Manager-Bindungen  
 R1001: Transaktions-Manager müssen SOAP&#160;1.1 und WS-Adressierung&#160;2004/08 für den WS-AtomicTransaction- und den WS-Coordination-Nachrichtenaustausch verwenden.  
  
 Anwendungsnachrichten werden nicht auf diese Bindungen eingeschränkt und werden später beschrieben.  
  
### <a name="transaction-manager-https-binding"></a>HTTPS-Bindungen des Transaktions-Managers  
 Die HTTPS-Bindung des Transaktions-Managers richtet sich lediglich nach der Transportsicherheit, um Sicherheit zu gewährleisten und eine Vertrauenswürdigkeit zwischen den einzelnen Absender-Empfänger-Paaren in der Transaktionsstruktur herzustellen.  
  
#### <a name="https-transport-configuration"></a>HTTPS-Transportkonfiguration  
 X.509-Zertifikate werden verwendet, um eine Transaktions-Manager-Identität herzustellen. Die Client/Server-Authentifizierung ist erforderlich, und die Client/Server-Autorisierung wird als Implementierungsdetail beibehalten:  
  
-   R1111: Über die Verbindung vorgestellte X.509-Zertifikate müssen einen Antragstellernamen aufweisen, der dem vollqualifizierten Domänennamen (FQDN) des sendenden Computers entspricht.  
  
-   B1112: DNS muss zwischen den einzelnen Absender-Empfänger-Paaren im System funktionieren, damit eine Prüfung der X.509-Antragstellernamen erfolgreich ist.  
  
#### <a name="activation-and-registration-binding-configuration"></a>Bindungskonfiguration von Aktivierung und Registrierung  
 WCF erfordert Anforderung/Antwort-duplexbindung mit Korrelation über HTTPS. (Weitere Informationen über Korrelation und Beschreibungen der Anforderungs-/Antwortnachrichten-Austauschmuster finden Sie unter WS-Atomic-Transaktion, Abschnitt 8.)  
  
#### <a name="2pc-protocol-binding-configuration"></a>Bindungskonfiguration des 2PC-Protokolls  
 WCF unterstützt unidirektionale (Datagramm-) Nachrichten über HTTPS. Korrelation unter den Nachrichten wird als Implementierungsdetail beibehalten.  
  
 B2131: Implementierungen müssen unterstützen `wsa:ReferenceParameters` wie beschrieben in WS-Adressierung, die Korrelation von WCF 2PC-Nachrichten zu erreichen.  
  
### <a name="transaction-manager-mixed-security-binding"></a>Gemischte Sicherheitsbindung des Transaktions-Managers  
 Dies ist eine alternative Bindung, verwendet transportsicherheit kombiniert mit dem WS-Coordination Issued Token-Modell zu identitätserstellungszwecken (Gemischter Modus).  Aktivierung und Registrierung sind die einzigen Elemente, die sich zwischen den beiden Bindungen unterscheiden.  
  
#### <a name="https-transport-configuration"></a>HTTPS-Transportkonfiguration  
 X.509-Zertifikate werden verwendet, um eine Transaktions-Manager-Identität herzustellen. Die Client/Server-Authentifizierung ist erforderlich, und die Client/Server-Autorisierung wird als Implementierungsdetail beibehalten:  
  
#### <a name="activation-message-binding-configuration"></a>Bindungskonfiguration von Aktivierungsnachrichten  
 Aktivierungsnachrichten nehmen in der Regel nicht an der Interoperabilität teil, da sie normalerweise zwischen einer Anwendung und dem lokalen Transaktions-Manager auftreten.  
  
 B1221: WCF verwendet duplex HTTPS-Bindung (beschrieben [Messaging-Protokolle](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)) für Aktivierungsnachrichten. Anforderungs- und Antwortnachrichten werden mithilfe von WS-Addressing&#160;2004/08 korreliert.  
  
 In der WS-Atomic Transaktion-Spezifikation, Abschnitt 8, werden die Korrelation und die Nachrichtenaustauschmuster ausführlich beschrieben.  
  
-   R1222: Beim Eingang eines `CreateCoordinationContext` muss der Koordinator ein `SecurityContextToken` mit zugewiesenem geheimen `STx` ausgeben. Dieses Token wird entsprechend der WS-Trust-Spezifikation in einem `t:IssuedTokens`-Header zurückgegeben.  
  
-   R1223: Falls die Aktivierung innerhalb eines bereits vorhandenen Koordinationskontexts stattfindet, muss der `t:IssuedTokens`-Header, bei dem `SecurityContextToken` dem bereits vorhandenem Kontext zugewiesen ist, in der `CreateCoordinationContext`-Nachricht fließen.  
  
 Ein neues `t:IssuedTokens` Header generiert werden soll, zum Anfügen an den ausgehenden `wscoor:CreateCoordinationContextResponse` Nachricht.  
  
#### <a name="registration-message-binding-configuration"></a>Bindungskonfiguration von Registrierungsnachrichten  
 B1231: WCF verwendet duplex HTTPS-Bindung (beschrieben [Messaging-Protokolle](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)). Anforderungs- und Antwortnachrichten werden mithilfe von WS-Addressing&#160;2004/08 korreliert.  
  
 In der WS-AtomicTransaction-Spezifikation, Abschnitt 8, werden weitere Details zur Korrelation und die Nachrichtenaustauschmuster ausführlich beschrieben.  
  
 R1232: Ausgehende `wscoor:Register` Nachrichten verwenden müssen die `IssuedTokenOverTransport` Authentifizierungsmodus in beschriebenen [Sicherheitsprotokolle](../../../../docs/framework/wcf/feature-details/security-protocols.md).  
  
 Die `wsse:Timestamp` Element muss signiert sein, mit der `SecurityContextToken``STx` ausgegeben. Diese Signatur ist Beweis für den Besitz des einer bestimmten Transaktion zugewiesenen Tokens und wird für die Authentifizierung einer Teilnehmerliste während der Transaktion verwendet. Die RegistrationResponse-Nachricht wird über HTTPS zurückgesendet.  
  
#### <a name="2pc-protocol-binding-configuration"></a>Bindungskonfiguration des 2PC-Protokolls  
 WCF unterstützt unidirektionale (Datagramm-) Nachrichten über HTTPS. Korrelation unter den Nachrichten wird als Implementierungsdetail beibehalten.  
  
 B2131: Implementierungen müssen unterstützen `wsa:ReferenceParameters` wie beschrieben in WS-Adressierung, die Korrelation von WCF 2PC-Nachrichten zu erreichen.  
  
## <a name="application-message-exchange"></a>Austausch von Anwendungsnachrichten  
 In Anwendungen können beliebige Bindungen für Nachrichten verwendet werden, die von Anwendung zu Anwendung gesendet werden, solange die Bindung die folgenden Sicherheitsanforderungen erfüllt:  
  
-   R2001: Nachrichten von Anwendung zu Anwendung müssen im Nachrichtenheader den `t:IssuedTokens`-Header zusammen mit `CoordinationContext` aufweisen.  
  
-   R2002: Integrität und Vertraulichkeit von `t:IssuedToken` müssen bereitgestellt werden.  
  
 Der `CoordinationContext`-Header enthält `wscoor:Identifier`. Während die Definition von `xsd:AnyURI` ermöglicht die Verwendung der absoluten und relativen URIs WCF unterstützt nur `wscoor:Identifiers`, wobei es sich um absolute URIs handelt.  
  
 Wenn die `wscoor:Identifier` von der `wscoor:CoordinationContext` ist ein relativer URI-Transaktionsdiensten aus transaktionalen WCF-Dienste.  
  
## <a name="message-examples"></a>Nachrichtenbeispiele  
  
### <a name="createcoordinationcontext-requestresponse-messages"></a>CreateCoordinationContext-Anforderungs-/Antwortmeldungen  
 Die folgenden Nachrichten folgen einem Anforderungs-/Antwortmuster.  
  
#### <a name="createcoordinationcontext"></a>CreateCoordinationContext  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://.../ws/2004/10/wscoor/CreateCoordinationContext</Action>  
    <a:MessageID>urn:uuid:069f5104-fd88-4264-9f99-60032a82854e</MessageID>  
    <a:ReplyTo>  
      <Address>https://...</a:Address>  
    </a:ReplyTo>  
    <a:To>https://...</a:To>  
    <wsse:Security>  
      <u:Timestamp>  
        <wsu:Created>2005-12-15T23:36:09.921Z</u:Created>  
        <wsu:Expires>2005-12-15T23:41:09.921Z</u:Expires>  
      </u:Timestamp>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:CreateCoordinationContext>  
      <wscoor:CoordinationType>...</wscoor:CoordinationType>  
    </wscoor:CreateCoordinationContext>  
  </s:Body>  
</s11:Envelope>  
```  
  
#### <a name="createcoordinationcontextresponse"></a>CreateCoordinationContextResponse  
  
```xml  
<s:Envelope>  
  <!-- Data below is shown in the clear for  
       illustration purposes only. -->  
  <s:Header>  
    <a:Action>./ws/2004/10/wscoor/CreateCoordinationContextResponse </a:Action>  
    <a:RelatesTo>urn:uuid:069f5104-fd88-4264-9f99-60032a82854e</a:RelatesTo>  
    <a:To s:mustUnderstand="1">https://... </a:To>  
    <t:IssuedTokens>  
 <wst:RequestSecurityTokenResponse     
    xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
    xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd"   
    xmlns:wst="http://schemas.xmlsoap.org/ws/2005/02/trust"  
    xmlns:wsc="http://schemas.xmlsoap.org/ws/2005/02/sc"  
    xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">  
    <wst:TokenType>http://schemas.xmlsoap.org/ws/2005/02/sc/sct</wst:TokenType>  
    <wst:RequestedSecurityToken>  
      <wsc:SecurityContextToken>  
        <wssu:Identifier>  
          http://fabrikam123.com/SCTi  
        </wssu:Identifier>  
      </wsc:SecurityContextToken>   
    </wst:RequestedSecurityToken>  
    <wsp:AppliesTo>  
        http://fabrikam123.com/CCi  
    </wsp:AppliesTo>    
    <wst:RequestedAttachedReference>  
      <wsse:SecurityTokenReference >  
        <wsse:Reference   
           ValueType="http://schemas.xmlsoap.org/ws/2005/02/sc/sct"  
           URI="http://fabrikam123.com/SCTi"/>  
      </wsse:SecurityTokenReference>  
    </wst:RequestedAttachedReference>  
    <wst:RequestedUnattachedReference>  
      <wsse:SecurityTokenReference>  
        <wsse:Reference   
          ValueType="http://schemas.xmlsoap.org/ws/2005/02/sc/sct"  
          URI="http://fabrikam123.com/SCTi"/>  
      </wsse:SecurityTokenReference>  
    </wst:RequestedUnattachedReference>  
    <wst:RequestedProofToken>  
      <wst:BinarySecret   
        Type="http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey">  
        <!-- base64 encoded value -->  
      </wst:BinarySecret>  
    </wst:RequestedProofToken>  
    <wst:Lifetime>  
      <wssu:Created>2005-10-24T20:19:26.526Z</wssu:Created>  
      <wssu:Expires>2005-10-25T06:24:26.526Z</wssu:Expires>  
    </wst:Lifetime>  
    <wst:KeySize>256</wst:KeySize>  
</wst:RequestSecurityTokenResponse>  
    </t:IssuedTokens>  
    <o:Security xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="_0">  
        <u:Created>2005-12-15T23:36:12.015Z</u:Created>  
        <u:Expires>2005-12-15T23:41:12.015Z</u:Expires>  
      </u:Timestamp>  
    </o:Security>  
  </s:Header>  
  <s:Body>  
    <wscoor:CreateCoordinationContextResponse>  
      <wscoor:CoordinationContext>  
        <wscoor:Identifier>  
     http://fabrikam123.com/CCi  
      </wscoor:Identifier>  
        <wscoor:Expires>...</wscoor:Expires>  
        <wscoor:CoordinationType>...</wscoor:CoordinationType>  
        <wscoor:RegistrationService>  
          <a:Address>https://...</a:Address>  
          <a:ReferenceParameters>  
             ...  
          </a:ReferenceParameters>  
        </wscoor:RegistrationService>  
      </wscoor:CoordinationContext>  
    </wscoor:CreateCoordinationContextResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="registration-messages"></a>Registrierungsnachrichten  
 Bei den folgenden Nachrichten handelt es sich um Registrierungsnachrichten.  
  
#### <a name="register"></a>Register  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://schemas.xmlsoap.org/ws/2004/10/wscoor/Register</a:Action>  
    <a:MessageID>urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088e</a:MessageID>  
    <a:ReplyTo>  
      <a:Address>https://...</a:Address>        
    </a:ReplyTo>  
    <a:To>https://...</a:To>  
    <wsse:Security   
      s:mustUnderstand="1"   
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp wssu:Id="_0" >  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
      <wsc:SecurityContextToken>  
      <wssu:Identifier>  
          http://fabrikam123.com/SCTi  
      </wssu:Identifier>  
      </wsc:SecurityContextToken>  
      <!-- supporting signature over the timestamp -->  
      <wsse:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">  
        <ds:SignedInfo>  
          <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
          <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#hmac-sha1"/>  
          <ds:Reference URI="#_0">  
            <ds:Transforms>  
              <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
            </ds:Transforms>  
            <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>  
            <ds:DigestValue>  
              alRzyhjLgoUOYoh8cx4n75eTcUk=  
            </ds:DigestValue>  
          </ds:Reference>  
        </ds:SignedInfo>  
        <ds:SignatureValue>YZYjnVvSOVasAQqQxaaviTSWtqI=</ds:SignatureValue>  
        <ds:KeyInfo>  
          <wsse:SecurityTokenReference  
            xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
            <wsse:Reference   
              URI="http://fabrikam123.com/SCTi"/>  
          </wsse:SecurityTokenReference>  
        </ds:KeyInfo>  
      </wsse:Signature>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:Register>  
      <wscoor:ProtocolIdentifier>...</wscoor:ProtocolIdentifier>  
      <wscoor:ParticipantProtocolService>  
        <a:Address>https://... </a:Address>  
      </wscoor:ParticipantProtocolService>  
    </wscoor:Register>  
  </s:Body>  
</s:Envelope>  
```  
  
#### <a name="register-response"></a>Register Response  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>  
      http://schemas.xmlsoap.org/ws/2004/10/wscoor/RegisterResponse  
    </a:Action>  
    <a:MessageID>urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088d</a:MessageID>  
    <a:RelatesTo>  
      urn:uuid:ed418b86-a75e-4aea-9d4e-a5d0cb5c088e        
    </a:RelatesTo>  
    <a:To>https://...</a:To>  
    <wsse:Security   
      s:mustUnderstand="1"   
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp>  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
    </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wscoor:RegisterResponse>  
      <wscoor:CoordinatorProtocolService>  
        <a:Address>https://...</a:Address>  
        <a:ReferenceParameters>  
          ...  
        </a:ReferenceParameters>  
      </wscoor:CoordinatorProtocolService>  
    </wscoor:RegisterResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="two-phase-commit-protocol-messages"></a>Zweiphasen-Commit-Protokollnachrichten  
 Die folgende Nachricht bezieht sich auf das Zweiphasen-Commit-Protokoll (2PC).  
  
#### <a name="commit"></a>Commit  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <a:Action>http://.../ws/2004/10/wsat/Commit</a:Action>  
    <a:To>https://...</a:To>  
    <wsse:Security   
      s:mustUnderstand="1"   
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"  
      xmlns:wssu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
      <wssu:Timestamp wssu:Id="_0" >  
        <wssu:Created>2005-12-15T23:36:13.827Z</wssu:Created>  
        <wssu:Expires>2005-12-15T23:41:13.827Z</wssu:Expires>  
      </wssu:Timestamp>  
   </wsse:Security>  
  </s:Header>  
  <s:Body xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
    <wsat:Commit />  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="application-messages"></a>Anwendungsnachrichten  
 Bei den folgenden Nachrichten handelt es sich um Anwendungsnachrichten.  
  
#### <a name="application-message-request"></a>Anwendungsnachrichtenanforderung  
  
```xml  
<s:Envelope>  
  <s:Header>  
<!-- Addressing headers, all signed-->  
    <wsse:Security s:mustUnderstand="1">  
      <wssu:Timestamp wssu:Id="timestamp">   
        <wssu:Created>2005-10-25T06:29:18.703Z</wssu:Created>  
        <wssu:Expires>2005-10-25T06:34:18.703Z</wssu:Expires>  
      </wssu:Timestamp>  
      <wsse:BinarySecurityToken   
          wssu:Id="IA_Certificate"   
          ValueType="...#X509v3"   
          EncodingType="...#Base64Binary">  
        <!-- IA certificate -->  
      </wsse:BinarySecurityToken>  
      <e:EncryptedKey Id="encrypted_key">  
            <!-- ephemeral key encrypted for PA certificate -->    
        <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
          <e:DataReference URI="#encrypted_body"/>  
          <e:DataReference URI="#encrypted_CCi"/>  
          <e:DataReference URI="#encrypted_issuedtokens"/>  
        </e:ReferenceList>  
      </e:EncryptedKey>  
      <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <!-- signature over Addressing headers, Timestamp, and Body -->  
      </Signature>  
    </wsse:Security>  
    <wsse11:EncryptedHeader >  
     <!-- encrypted wscoor:CoordinationContext header containing CCi -->  
    </wsse11:EncryptedHeader>  
    <wsse11:EncryptedHeader   
      <!-- encrypted wst:IssuedTokens header containing SCTi -->  
      <!-- wst:IssuedTokens header is taken verbatim from message #2 above, omitted for brevity -->  
    </wsse11:EncryptedHeader>  
  </s:Header>  
  <s:Body wssu:Id="body">  
    <!-- encrypted content of the Body element of the application message -->      
    <e:EncryptedData Id="encrypted_body"   
           Type="http://www.w3.org/2001/04/xmlenc#Content"   
           xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
...  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
```
