---
title: Schemat ustawień kryptografii
ms.date: 03/30/2017
helpviewer_keywords:
- configuration schema [.NET Framework], cryptography
- elements [.NET Framework], cryptography
- schema configuration settings
- cryptography, settings schema
- cryptography, mapping algorithm names
- configuration sections [.NET Framework]
- configuration settings [.NET Framework], cryptography
ms.assetid: 1f55050a-b2a3-4868-a3c0-da20826150f3
ms.openlocfilehash: 0215851f83a13ee48547144f08c5c693ec2d90bf
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91149533"
---
# <a name="cryptography-settings-schema"></a>Schemat ustawień kryptografii

Schemat ustawień kryptografii zawiera elementy, które określają sposób mapowania przyjaznych nazw algorytmów na klasy implementujące algorytmy kryptografii.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<mscorlib>**](mscorlib-element-for-cryptography-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptographySettings>**](cryptographysettings-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptoNameMapping>**](cryptonamemapping-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptoClasses>**](cryptoclasses-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptoClass>**](cryptoclass-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<nameEntry>**](nameentry-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<oidMap>**](oidmap-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<oidEntry>**](oidentry-element.md)

|Element|Opis|  
|-------------|-----------------|  
|[**\<cryptoClasses**>](cryptoclasses-element.md)|Zawiera listę klas kryptograficznych, które mają mapowanie do przyjaznej nazwy w **\<nameEntry>** elemencie.|  
|[**\<cryptoClass**>](cryptoclass-element.md)|Zawiera klasę kryptografii, która ma mapowanie do przyjaznej nazwy w **\<nameEntry>** elemencie.|  
|[**\<cryptographySettings**>](cryptographysettings-element.md)|Zawiera ustawienia kryptografii.|  
|[**\<cryptoNameMapping**>](cryptonamemapping-element.md)|Zawiera mapowania klas do przyjaznych nazw.|  
|[**\<mscorlib>** element dla ustawień kryptografii](mscorlib-element-for-cryptography-settings.md)|Zawiera **\<cryptographySettings>** element.|  
|[**\<nameEntry>**](nameentry-element.md)|Mapuje nazwę klasy na przyjazną nazwę algorytmu, która pozwala jednej klasie mieć wiele przyjaznych nazw.|  
|[**\<oidEntry>**](oidentry-element.md)|Mapuje identyfikator obiektu ASN. 1 (OID) na przyjazną nazwę.|  
|[**\<oidMap>**](oidmap-element.md)|Zawiera mapowania identyfikatorów OID ASN. 1 do klas.|  
  
## <a name="see-also"></a>Zobacz też

- [Schemat pliku konfiguracji](../index.md)
- [Usługi kryptograficzne](../../../../standard/security/cryptographic-services.md)
