---
title: IMetaDataDispenserEx::SetOption — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.SetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::SetOption
helpviewer_keywords:
- IMetaDataDispenserEx::SetOption method [.NET Framework metadata]
- SetOption method [.NET Framework metadata]
ms.assetid: 9f1c7ccd-7fb2-41d8-aa00-24b823376527
topic_type:
- apiref
ms.openlocfilehash: 4216658eb562c5c57b75c3c257cd8e53a7a34221
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95700590"
---
# <a name="imetadatadispenserexsetoption-method"></a>IMetaDataDispenserEx::SetOption — Metoda

Ustawia określoną opcję na daną wartość dla bieżącego zakresu metadanych. Opcja określa, jak są obsługiwane wywołania bieżącego zakresu metadanych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetOption (  
    [in] REFGUID optionId,
    [in] const VARIANT *pValue  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `optionId`  
 podczas Wskaźnik do identyfikatora GUID, który określa opcję, która ma zostać ustawiona.  
  
 `pValue`  
 podczas Wartość, która ma zostać użyta do ustawienia opcji. Typ tej wartości musi być wariantem typu określonej opcji.  
  
## <a name="remarks"></a>Uwagi  

 Poniższa tabela zawiera listę dostępnych identyfikatorów GUID, `optionId` do których może wskazywać parametr oraz odpowiednie prawidłowe wartości `pValue` parametru.  
  
|GUID|Opis|`pValue` Konstruktora|  
|----------|-----------------|------------------------|  
|MetaDataCheckDuplicatesFor|Kontroluje, które elementy są sprawdzane pod kątem duplikatów. Za każdym razem, gdy wywoływana jest metoda [IMetaDataEmit](imetadataemit-interface.md) , która tworzy nowy element, można polecić metodę, aby sprawdzić, czy element już istnieje w bieżącym zakresie. Na przykład można sprawdzić obecność `mdMethodDef` elementów. w tym przypadku, gdy wywołasz [IMetaDataEmit::D efinemethod](imetadataemit-definemethod-method.md), sprawdzimy, czy metoda jeszcze nie istnieje w bieżącym zakresie. Ten test korzysta z klucza, który jednoznacznie identyfikuje daną metodę: Parent Type, Name i Signature.|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorCheckDuplicatesFor —](corcheckduplicatesfor-enumeration.md) .|  
|MetaDataRefToDefCheck|Kontroluje, które elementy, do których istnieją odwołania, są konwertowane na definicje. Domyślnie aparat metadanych optymalizuje kod przez przekonwertowanie elementu, do którego się odwołuje, jeśli element, do którego się odwoływano, jest zdefiniowany w bieżącym zakresie.|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorRefToDefCheck —](correftodefcheck-enumeration.md) .|  
|MetaDataNotificationForTokenMovement|Określa, które ponowne mapowania tokenu występują podczas scalania metadanych generują wywołania zwrotne. Użyj metody [IMetaDataEmit:: SetHandle](imetadataemit-sethandler-method.md) , aby nawiązać Interfejs [IMapToken](imaptoken-interface.md) .|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorNotificationForTokenMovement —](cornotificationfortokenmovement-enumeration.md) .|  
|MetaDataSetENC|Steruje zachowaniem funkcji Edit-and-Continue (ENC). Można ustawić tylko jeden tryb zachowania w danym momencie.|Musi być VARIANT typu UI4 i musi zawierać wartość wyliczenia [CorSetENC —](corsetenc-enumeration.md) . Wartość nie jest maską bitów.|  
|MetaDataErrorIfEmitOutOfOrder|Kontroluje, które emitowane błędy generują wywołania zwrotne. Emitowanie metadanych poza kolejnością nie jest krytyczne; Jednak w przypadku emisji metadanych w kolejności, w której jest preferowany aparat metadanych, metadane są bardziej kompaktowe i dlatego mogą być bardziej efektywnie przeszukiwane. Użyj `IMetaDataEmit::SetHandler` metody, aby nawiązać Interfejs [IMetaDataError](imetadataerror-interface.md) .|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorErrorIfEmitOutOfOrder —](corerrorifemitoutoforder-enumeration.md) .|  
|MetaDataImportOption|Kontroluje typy elementów, które zostały usunięte podczas ENC, są pobierane przez moduł wyliczający.|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorImportOptions — Enumeration](corimportoptions-enumeration.md) .|  
|MetaDataThreadSafetyOptions|Określa, czy aparat metadanych uzyskuje blokady czytnika/składnika zapisywania, zapewniając w ten sposób bezpieczeństwo wątków. Domyślnie silnik zakłada, że dostęp jest jednowątkowy przez obiekt wywołujący, więc nie są pobierane żadne blokady. Klienci są odpowiedzialni za zachowanie poprawnej synchronizacji wątków podczas korzystania z interfejsu API metadanych.|Musi być VARIANT typu UI4 i musi zawierać wartość wyliczenia [CorThreadSafetyOptions —](corthreadsafetyoptions-enumeration.md) . Wartość nie jest maską bitów.|  
|MetaDataGenerateTCEAdapters|Określa, czy importer biblioteki typów powinien generować karty z ściśle połączonymi zdarzeniami (TCE) dla kontenerów punktów połączenia COM.|Musi być wariantem typu BOOL. Jeśli `pValue` jest ustawiona na `true` , importer biblioteki typów GENERUJE karty tce.|  
|MetaDataTypeLibImportNamespace|Określa niedomyślną przestrzeń nazw dla importowanej biblioteki typów.|Musi mieć wartość null lub być wariantem typu BSTR. Jeśli `pValue` jest wartością null, bieżąca przestrzeń nazw jest ustawiona na wartość null; w przeciwnym razie bieżąca przestrzeń nazw jest ustawiona na ciąg, który jest przechowywany w typie BSTR wariantu.|  
|MetaDataLinkerOptions|Określa, czy konsolidator powinien generować zestaw lub .NET Framework plik modułu.|Musi być wariantem typu UI4 i musi zawierać kombinację wartości wyliczenia [CorLinkerOptions —](corlinkeroptions-enumeration.md) .|  
|MetaDataRuntimeVersion|Określa wersję środowiska uruchomieniowego języka wspólnego, dla którego został skompilowany obraz. Wersja jest przechowywana jako ciąg, na przykład "v 1.0.3705".|Musi być wartością null, wartością VT_EMPTY lub wariantem typu BSTR. Jeśli `pValue` ma wartość null, wersja środowiska uruchomieniowego jest ustawiona na wartość null. Jeśli `pValue` VT_EMPTY, wersja jest ustawiona na wartość domyślną, która jest rysowana z wersji Mscorwks.dll, w której jest uruchomiony kod metadanych. W przeciwnym razie wersja środowiska uruchomieniowego jest ustawiona na ciąg, który jest przechowywany w typie BSTR wariantu.|  
|MetaDataMergerOptions|Określa opcje scalania metadanych.|Musi być wariantem typu UI4 i musi zawierać kombinację wartości `MergeFlags` wyliczenia, która jest opisana w pliku corhdr. h.|  
|MetaDataPreserveLocalRefs|Wyłącza Optymalizowanie lokalnych odwołań do definicji.|Musi zawierać kombinację wartości wyliczenia [CorLocalRefPreservation —](corlocalrefpreservation-enumeration.md) .|  
  
## <a name="requirements"></a>Wymagania  

 **Platforma:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Używane jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataDispenserEx — Interfejs](imetadatadispenserex-interface.md)
- [IMetaDataDispenser — Interfejs](imetadatadispenser-interface.md)
