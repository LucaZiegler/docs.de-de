---
title: IMetaDataImport::EnumMethodSemantics-Methode
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMethodSemantics
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMethodSemantics
helpviewer_keywords:
- EnumMethodSemantics method [.NET Framework metadata]
- IMetaDataImport::EnumMethodSemantics method [.NET Framework metadata]
ms.assetid: e7e3c630-9691-46d6-94df-b5593a7bb08a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 00a28e0f7ab03af8d5f2fc0dda5274f9aaa4dca2
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="imetadataimportenummethodsemantics-method"></a>IMetaDataImport::EnumMethodSemantics-Methode
Zählt die Eigenschaften und die Eigenschaftenänderungsereignisse auf, auf die sich die angegebene Methode bezieht.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT EnumMethodSemantics (  
   [in, out] HCORENUM    *phEnum,  
   [in]  mdMethodDef     mb,   
   [out] mdToken         rEventProp[],  
   [in]  ULONG           cMax,  
   [out] ULONG           *pcEventProp  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `phEnum`  
 [in, out] Ein Zeiger auf den Enumerator. Dies muss für den ersten Aufruf dieser Methode NULL sein.  
  
 `mb`  
 [in] Ein MethodDef-Token, das den Bereich der Enumeration einschränkt.  
  
 `rEventProp`  
 [out] Das Array zum Speichern von Ereignissen oder Eigenschaften verwendet.  
  
 `cMax`  
 [in] Die maximale Größe des `rEventProp`-Arrays.  
  
 `pcEventProp`  
 [out] Die Anzahl von Ereignissen oder Eigenschaften, die im zurückgegebenen `rEventProp`.  
  
## <a name="return-value"></a>Rückgabewert  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|`S_OK`|`EnumMethodSemantics` wurde erfolgreich zurückgegeben.|  
|`S_FALSE`|Es sind keine Ereignisse oder Eigenschaften aufgelistet werden. In diesem Fall `pcEventProp` 0 (null).|  
  
## <a name="remarks"></a>Hinweise  
 Viele Typen der common Language Runtime definieren *Eigenschaft* `Changed` Ereignisse und `On` *Eigenschaft* `Changed` Methoden, die sich auf ihre Eigenschaften. Z. B. die <xref:System.Windows.Forms.Control?displayProperty=nameWithType> Typ definiert einen <xref:System.Windows.Forms.Control.Font%2A> -Eigenschaft, ein <xref:System.Windows.Forms.Control.FontChanged> -Ereignis und eine <xref:System.Windows.Forms.Control.OnFontChanged%2A> Methode. Die Set-Zugriffsmethode, der die <xref:System.Windows.Forms.Control.Font%2A> Eigenschaftenaufrufe <xref:System.Windows.Forms.Control.OnFontChanged%2A> -Methode, die wiederum löst die <xref:System.Windows.Forms.Control.FontChanged> Ereignis. Rufen `EnumMethodSemantics` mithilfe von MethodDef für <xref:System.Windows.Forms.Control.OnFontChanged%2A> abzurufenden Verweise auf die <xref:System.Windows.Forms.Control.Font%2A> Eigenschaft und die <xref:System.Windows.Forms.Control.FontChanged> Ereignis.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cor.h  
  
 **Bibliothek:** als Ressource in MsCorEE.dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [IMetaDataImport-Schnittstelle](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [IMetaDataImport2-Schnittstelle](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
