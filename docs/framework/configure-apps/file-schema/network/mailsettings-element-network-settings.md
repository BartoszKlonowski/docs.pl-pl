---
title: <mailSettings>, element (ustawienia sieci)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: 4e8bf23ce39edadf80f019315c690b597b3d7361
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089232"
---
# <a name="mailsettings-element-network-settings"></a><span data-ttu-id="83ddf-102">\<mailSettings>, element (ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="83ddf-102">\<mailSettings> Element (Network Settings)</span></span>
<span data-ttu-id="83ddf-103">Konfiguruje opcje wysyłania poczty.</span><span class="sxs-lookup"><span data-stu-id="83ddf-103">Configures mail sending options.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a><span data-ttu-id="83ddf-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="83ddf-104">Syntax</span></span>  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="83ddf-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="83ddf-105">Attributes and Elements</span></span>  
 <span data-ttu-id="83ddf-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="83ddf-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="83ddf-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="83ddf-107">Attributes</span></span>  
 <span data-ttu-id="83ddf-108">Brak.</span><span class="sxs-lookup"><span data-stu-id="83ddf-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="83ddf-109">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="83ddf-109">Child Elements</span></span>  
  
|<span data-ttu-id="83ddf-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="83ddf-110">Attribute</span></span>|<span data-ttu-id="83ddf-111">Opis</span><span class="sxs-lookup"><span data-stu-id="83ddf-111">Description</span></span>|  
|---------------|-----------------|  
|[<span data-ttu-id="83ddf-112">\<smtp>— Element (Ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="83ddf-112">\<smtp> Element (Network Settings)</span></span>](smtp-element-network-settings.md)|<span data-ttu-id="83ddf-113">Konfiguruje opcje protokołu Simple Mail Transport.</span><span class="sxs-lookup"><span data-stu-id="83ddf-113">Configures Simple Mail Transport Protocol options.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="83ddf-114">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="83ddf-114">Parent Elements</span></span>  
  
|<span data-ttu-id="83ddf-115">**Postaci**</span><span class="sxs-lookup"><span data-stu-id="83ddf-115">**Element**</span></span>|<span data-ttu-id="83ddf-116">**Opis**</span><span class="sxs-lookup"><span data-stu-id="83ddf-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="83ddf-117">\<system.Net>— Element (Ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="83ddf-117">\<system.Net> Element (Network Settings)</span></span>](system-net-element-network-settings.md)|<span data-ttu-id="83ddf-118">Zawiera ustawienia, które określają, w jaki sposób .NET Framework nawiązuje połączenie z siecią.</span><span class="sxs-lookup"><span data-stu-id="83ddf-118">Contains settings that specify how the .NET Framework connects to the network.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="83ddf-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="83ddf-119">Example</span></span>  
 <span data-ttu-id="83ddf-120">W poniższym przykładzie określono odpowiednie parametry SMTP do wysyłania wiadomości e-mail przy użyciu domyślnych poświadczeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="83ddf-120">The following example specifies the appropriate SMTP parameters to send email using the default network credentials.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="83ddf-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="83ddf-121">See also</span></span>

- <xref:System.Net.Mail.SmtpClient>
- [<span data-ttu-id="83ddf-122">Schemat ustawień sieci</span><span class="sxs-lookup"><span data-stu-id="83ddf-122">Network Settings Schema</span></span>](index.md)
