---
ms.openlocfilehash: 9fd4e570d9476f5ac4c310759113d72b354a3060
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606303"
---
### <a name="tls-1x-by-default-passes-the-sch_send_aux_record-flag-to-the-underlying-schannel-api"></a><span data-ttu-id="db748-101">Protokół TLS 1. x domyślnie przekazuje flagę SCH_SEND_AUX_RECORD do źródłowego interfejsu API SCHANNEL</span><span class="sxs-lookup"><span data-stu-id="db748-101">TLS 1.x by default passes the SCH_SEND_AUX_RECORD flag to the underlying SCHANNEL API</span></span>

#### <a name="details"></a><span data-ttu-id="db748-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="db748-102">Details</span></span>

<span data-ttu-id="db748-103">W przypadku korzystania z protokołu TLS 1. x .NET Framework opiera się na źródłowym interfejsie API SCHANNEL systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="db748-103">When using TLS 1.x, the .NET Framework relies on the underlying Windows SCHANNEL API.</span></span> <span data-ttu-id="db748-104">Począwszy od .NET Framework 4,6, flaga [SCH_SEND_AUX_RECORD](/windows/win32/api/schannel/ns-schannel-schannel_cred) jest domyślnie przenoszona do kanału Schannel.</span><span class="sxs-lookup"><span data-stu-id="db748-104">Starting with .NET Framework 4.6, the [SCH_SEND_AUX_RECORD](/windows/win32/api/schannel/ns-schannel-schannel_cred) flag is passed by default to SCHANNEL.</span></span> <span data-ttu-id="db748-105">Powoduje to, że SCHANNEL dzieli dane tak, aby były szyfrowane do dwóch oddzielnych rekordów, pierwszy jako jeden bajt, a drugi jako <em>n</em>-1 b. W rzadkich przypadkach powoduje to przerwanie komunikacji między klientami a istniejącymi serwerami, które zakładają, że dane znajdują się w pojedynczym rekordzie.</span><span class="sxs-lookup"><span data-stu-id="db748-105">This causes SCHANNEL to split data to be encrypted into two separate records, the first as a single byte and the second as <em>n</em>-1 bytes.In rare cases, this breaks communication between clients and existing servers that make the assumption that the data resides in a single record.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="db748-106">Sugestia</span><span class="sxs-lookup"><span data-stu-id="db748-106">Suggestion</span></span>

<span data-ttu-id="db748-107">Jeśli ta zmiana powoduje przerwanie komunikacji z istniejącym serwerem, można wyłączyć wysyłanie flagi [SCH_SEND_AUX_RECORD](/windows/win32/api/schannel/ns-schannel-schannel_cred) i przywrócić poprzednie zachowanie niedzielenia danych na oddzielne rekordy, dodając następujący przełącznik do [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu w [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sekcji pliku konfiguracyjnego aplikacji:</span><span class="sxs-lookup"><span data-stu-id="db748-107">If this change breaks communication with an existing server, you can disable sending the [SCH_SEND_AUX_RECORD](/windows/win32/api/schannel/ns-schannel-schannel_cred) flag and restore the previous behavior of not splitting data into separate records by adding the following switch to the [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element in the [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) section of your app configuration file:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchSendAuxRecord=true" />
</runtime>
```

> [!IMPORTANT]
> <span data-ttu-id="db748-108">To ustawienie jest dostępne wyłącznie w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="db748-108">This setting is provided for backward compatibility only.</span></span> <span data-ttu-id="db748-109">Jego użycie nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="db748-109">Its use is otherwise not recommended.</span></span>

| <span data-ttu-id="db748-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="db748-110">Name</span></span>    | <span data-ttu-id="db748-111">Wartość</span><span class="sxs-lookup"><span data-stu-id="db748-111">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="db748-112">Zakres</span><span class="sxs-lookup"><span data-stu-id="db748-112">Scope</span></span>   | <span data-ttu-id="db748-113">Edge</span><span class="sxs-lookup"><span data-stu-id="db748-113">Edge</span></span>        |
| <span data-ttu-id="db748-114">Wersja</span><span class="sxs-lookup"><span data-stu-id="db748-114">Version</span></span> | <span data-ttu-id="db748-115">4,6</span><span class="sxs-lookup"><span data-stu-id="db748-115">4.6</span></span>         |
| <span data-ttu-id="db748-116">Typ</span><span class="sxs-lookup"><span data-stu-id="db748-116">Type</span></span>    | <span data-ttu-id="db748-117">Przekierowanie</span><span class="sxs-lookup"><span data-stu-id="db748-117">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="db748-118">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="db748-118">Affected APIs</span></span>

- <xref:System.Net.Security.SslStream?displayProperty=nameWithType>
- <xref:System.Net.ServicePointManager?displayProperty=nameWithType>
- <xref:System.Net.Http.HttpClient?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>
- <xref:System.Net.FtpWebRequest?displayProperty=nameWithType>
