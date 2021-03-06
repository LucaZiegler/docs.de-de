---
title: IMetaDataEmit::DefineParam-Methode
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineParam
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineParam
helpviewer_keywords:
- IMetaDataEmit::DefineParam method [.NET Framework metadata]
- DefineParam method [.NET Framework metadata]
ms.assetid: d86a3d14-4796-4909-9591-dfafe3de5ce4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5d49ac70aceb76f69711ea4bf514f69697ac156c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="imetadataemitdefineparam-method"></a>IMetaDataEmit::DefineParam-Methode
Erstellt eine Parameterdefinition mit der angegebenen Signatur für die Methode, die durch das angegebene Token verwiesen wird, und ruft ein Token für die Parameterdefinition.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT DefineParam (  
    [in]  mdMethodDef md,   
    [in]  ULONG       ulParamSeq,   
    [in]  LPCWSTR     szName,   
    [in]  DWORD       dwParamFlags,   
    [in]  DWORD       dwCPlusTypeFlag,   
    [in]  void const  *pValue,  
    [in]  ULONG       cchValue,   
    [out] mdParamDef  *ppd   
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `md`  
 [in] Das Token für die Methode, deren Parameter definiert wird.  
  
 `ulParamSeq`  
 [in] Die Sequenznummer des Parameters.  
  
 `szName`  
 [in] Der Name des Parameters im Unicode-Format.  
  
 `dwParamFlags`  
 [in] Flags für den Parameter. Dies ist eine Bitmaske der `CorParamAttr` Werte.  
  
 `dwCPlusTypeFlag`  
 [in] `ELEMENT_TYPE_` *\** für den konstanten Wert.  
  
 `pValue`  
 [in] Der Konstante Wert für den Parameter.  
  
 `cchValue`  
 [in] Die Größe in Unicode-Zeichen, d. h. der `pValue`.  
  
 `ppd`  
 [out] Die `mdParamDef` Token zugewiesen.  
  
## <a name="remarks"></a>Hinweise  
 Die Sequenzwerte `ulParamSeq` beginnen mit 1 für Parameter. Ein Wert zurückgegeben hat eine Sequenznummer 0.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cor.h  
  
 **Bibliothek:** als Ressource in MSCorEE.dll verwendet  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [IMetaDataEmit-Schnittstelle](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)  
 [IMetaDataEmit2-Schnittstelle](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
