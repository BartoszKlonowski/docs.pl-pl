---
title: 'Zmiana istotna: interfejs API Obsoletions z niedomyślnymi identyfikatorami diagnostycznymi'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0 w podstawowych bibliotekach .NET, w których niektóre interfejsy API zostały oznaczone jako przestarzałe przy użyciu niestandardowego identyfikatora diagnostyki.
ms.date: 11/01/2020
ms.openlocfilehash: 9bd7ce18aed38955f9abc91e0c8b09e827c401d6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95761623"
---
# <a name="api-obsoletions-with-non-default-diagnostic-ids"></a><span data-ttu-id="3f069-103">Interfejs API Obsoletions z identyfikatorami diagnostycznymi innymi niż domyślne</span><span class="sxs-lookup"><span data-stu-id="3f069-103">API obsoletions with non-default diagnostic IDs</span></span>

<span data-ttu-id="3f069-104">Niektóre interfejsy API zostały oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="3f069-104">Some APIs have been marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="3f069-105">Ta twarda zmiana dotyczy interfejsów API, które zostały oznaczone jako przestarzałe *przy użyciu NIESTANDARDOWEGO identyfikatora diagnostyki*.</span><span class="sxs-lookup"><span data-stu-id="3f069-105">This breaking change is specific to APIs that have been marked as obsolete *with a custom diagnostic ID*.</span></span> <span data-ttu-id="3f069-106">Pominięcie domyślnego identyfikatora diagnostyki obsoletion, który jest [CS0618](../../../../csharp/language-reference/compiler-messages/cs0618.md) dla kompilatora języka C#, nie powoduje pomijania ostrzeżeń generowanych przez kompilator, gdy są używane te interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="3f069-106">Suppressing the default obsoletion diagnostic ID, which is [CS0618](../../../../csharp/language-reference/compiler-messages/cs0618.md) for the C# compiler, does not suppress the warnings that the compiler generates when these APIs are used.</span></span>

## <a name="change-description"></a><span data-ttu-id="3f069-107">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="3f069-107">Change description</span></span>

<span data-ttu-id="3f069-108">W poprzednich wersjach programu .NET te interfejsy API mogą być używane bez ostrzeżenia dotyczącego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="3f069-108">In previous .NET versions, these APIs can be used without any build warning.</span></span> <span data-ttu-id="3f069-109">W programie .NET 5,0 i jego nowszych wersjach korzystanie z tych interfejsów API powoduje wyświetlenie ostrzeżenia lub błędu w czasie kompilacji przy użyciu niestandardowego identyfikatora diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="3f069-109">In .NET 5.0 and later versions, use of these APIS produces a compile-time warning or error with a custom diagnostic ID.</span></span> <span data-ttu-id="3f069-110">Użycie niestandardowych identyfikatorów diagnostyki pozwala pominąć ostrzeżenia obsoletion indywidualnie zamiast zbiorczo pomijania wszystkich ostrzeżeń obsoletion.</span><span class="sxs-lookup"><span data-stu-id="3f069-110">The use of custom diagnostic IDs allows you to suppress the obsoletion warnings individually instead of blanket-suppressing all obsoletion warnings.</span></span>

<span data-ttu-id="3f069-111">Poniższa tabela zawiera listę niestandardowych identyfikatorów diagnostyki i odpowiadających im komunikatów ostrzegawczych dla przestarzałych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3f069-111">The following table lists the custom diagnostic IDs and their corresponding warning messages for obsoleted APIs.</span></span>

| <span data-ttu-id="3f069-112">Identyfikator diagnostyki</span><span class="sxs-lookup"><span data-stu-id="3f069-112">Diagnostic ID</span></span> | <span data-ttu-id="3f069-113">Opis</span><span class="sxs-lookup"><span data-stu-id="3f069-113">Description</span></span> | <span data-ttu-id="3f069-114">Ważność</span><span class="sxs-lookup"><span data-stu-id="3f069-114">Severity</span></span> |
| - | - |
| `SYSLIB0001` | <span data-ttu-id="3f069-115">Kodowanie UTF-7 jest niezabezpieczone i nie powinno być używane.</span><span class="sxs-lookup"><span data-stu-id="3f069-115">The UTF-7 encoding is insecure and should not be used.</span></span> <span data-ttu-id="3f069-116">Zamiast tego należy rozważyć użycie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="3f069-116">Consider using UTF-8 instead.</span></span> | <span data-ttu-id="3f069-117">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-117">Warning</span></span> |
| `SYSLIB0002` | <span data-ttu-id="3f069-118"><xref:System.Security.Permissions.PrincipalPermissionAttribute> nie jest uznawany przez środowisko uruchomieniowe i nie może być używany.</span><span class="sxs-lookup"><span data-stu-id="3f069-118"><xref:System.Security.Permissions.PrincipalPermissionAttribute> is not honored by the runtime and must not be used.</span></span> | <span data-ttu-id="3f069-119">Błąd</span><span class="sxs-lookup"><span data-stu-id="3f069-119">Error</span></span> |
| `SYSLIB0003` | <span data-ttu-id="3f069-120">Zabezpieczenia dostępu kodu (CAS) nie są obsługiwane ani honorowane przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="3f069-120">Code access security (CAS) is not supported or honored by the runtime.</span></span> | <span data-ttu-id="3f069-121">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-121">Warning</span></span> |
| `SYSLIB0004` | <span data-ttu-id="3f069-122">Funkcja ograniczonego regionu wykonywania (CER) nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3f069-122">The constrained execution region (CER) feature is not supported.</span></span> | <span data-ttu-id="3f069-123">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-123">Warning</span></span> |
| `SYSLIB0005` | <span data-ttu-id="3f069-124">Globalna pamięć podręczna zestawów (GAC) nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3f069-124">The global assembly cache (GAC) is not supported.</span></span> | <span data-ttu-id="3f069-125">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-125">Warning</span></span> |
| `SYSLIB0006` | <span data-ttu-id="3f069-126"><xref:System.Threading.Thread.Abort?displayProperty=nameWithType> nie jest obsługiwane i zgłasza <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="3f069-126"><xref:System.Threading.Thread.Abort?displayProperty=nameWithType> is not supported and throws <xref:System.PlatformNotSupportedException>.</span></span> | <span data-ttu-id="3f069-127">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-127">Warning</span></span> |
| `SYSLIB0007` | <span data-ttu-id="3f069-128">Domyślna implementacja tego algorytmu kryptografii nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3f069-128">The default implementation of this cryptography algorithm is not supported.</span></span> | <span data-ttu-id="3f069-129">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-129">Warning</span></span> |
| `SYSLIB0008` | <span data-ttu-id="3f069-130"><xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator>Interfejs API nie jest obsługiwany i zgłasza <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="3f069-130">The <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator> API is not supported and throws <xref:System.PlatformNotSupportedException>.</span></span> | <span data-ttu-id="3f069-131">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-131">Warning</span></span> |
| `SYSLIB0009` | <span data-ttu-id="3f069-132"><xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType>Metody i <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> nie są obsługiwane i throw <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="3f069-132">The <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType> and <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> methods are not supported and throw <xref:System.PlatformNotSupportedException>.</span></span> | <span data-ttu-id="3f069-133">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-133">Warning</span></span> |
| `SYSLIB0010`| <span data-ttu-id="3f069-134">Niektóre interfejsy API komunikacji zdalnej nie są obsługiwane i throw <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="3f069-134">Some remoting APIs are not supported and throw <xref:System.PlatformNotSupportedException>.</span></span> | <span data-ttu-id="3f069-135">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-135">Warning</span></span> |
| `SYSLIB0011` | <span data-ttu-id="3f069-136"><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> Serializacja jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="3f069-136"><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> serialization is obsolete and should not be used.</span></span> | <span data-ttu-id="3f069-137">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-137">Warning</span></span> |
| `SYSLIB0012` | <span data-ttu-id="3f069-138"><xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> i <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> są dołączone tylko do .NET Framework zgodności.</span><span class="sxs-lookup"><span data-stu-id="3f069-138"><xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> and <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> are only included for .NET Framework compatibility.</span></span> <span data-ttu-id="3f069-139">Zamiast tego użyj polecenia cmdlet <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="3f069-139">Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> instead.</span></span> | <span data-ttu-id="3f069-140">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="3f069-140">Warning</span></span> |

## <a name="version-introduced"></a><span data-ttu-id="3f069-141">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="3f069-141">Version introduced</span></span>

<span data-ttu-id="3f069-142">.NET 5,0</span><span class="sxs-lookup"><span data-stu-id="3f069-142">.NET 5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="3f069-143">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="3f069-143">Recommended action</span></span>

- <span data-ttu-id="3f069-144">Postępuj zgodnie ze szczegółowymi wskazówkami podanymi dla każdego identyfikatora diagnostyki przy użyciu linku adresu URL podanego w ostrzeżeniu.</span><span class="sxs-lookup"><span data-stu-id="3f069-144">Follow the specific guidance provided for the each diagnostic ID using the URL link provided on the warning.</span></span>

- <span data-ttu-id="3f069-145">Nie można pominąć ostrzeżeń ani błędów dla tych Obsoletions przy użyciu standardowego identyfikatora diagnostyki dla przestarzałych typów lub członków; Użyj `SYSLIBxxxx` zamiast tego wartości NIESTANDARDOWEGO identyfikatora diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="3f069-145">Warnings or errors for these obsoletions can't be suppressed using the standard diagnostic ID for obsolete types or members; use the custom `SYSLIBxxxx` diagnostic ID value instead.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="3f069-146">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="3f069-146">Affected APIs</span></span>

### <a name="syslib0001"></a><span data-ttu-id="3f069-147">SYSLIB0001</span><span class="sxs-lookup"><span data-stu-id="3f069-147">SYSLIB0001</span></span>

- <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType>
- <xref:System.Text.UTF7Encoding.%23ctor%2A>

### <a name="syslib0002"></a><span data-ttu-id="3f069-148">SYSLIB0002</span><span class="sxs-lookup"><span data-stu-id="3f069-148">SYSLIB0002</span></span>

- <xref:System.Security.Permissions.PrincipalPermissionAttribute.%23ctor(System.Security.Permissions.SecurityAction)>

### <a name="syslib0003"></a><span data-ttu-id="3f069-149">SYSLIB0003</span><span class="sxs-lookup"><span data-stu-id="3f069-149">SYSLIB0003</span></span>

<span data-ttu-id="3f069-150">Klasy w `System.Security.Permissions` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="3f069-150">Classes in the `System.Security.Permissions` namespace:</span></span>

- <xref:System.Security.Permissions.CodeAccessSecurityAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.DataProtectionPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.DataProtectionPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.GacIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.GacIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.HostProtectionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageFilePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageFilePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStoragePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStoragePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntry?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntryCollection?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntryEnumerator?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.PermissionSetAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.PrincipalPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.PublisherIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.PublisherIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ResourcePermissionBase?displayProperty=fullName>
- <xref:System.Security.Permissions.ResourcePermissionBaseEntry?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.SiteIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.SiteIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNameIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNamePublicKeyBlob?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.UrlIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.UrlIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ZoneIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.ZoneIdentityPermissionAttribute?displayProperty=fullName>

<span data-ttu-id="3f069-151">Klasy, które pochodzą z `CodeAccessSecurityAttribute` :</span><span class="sxs-lookup"><span data-stu-id="3f069-151">Classes that derive from `CodeAccessSecurityAttribute`:</span></span>

- <xref:System.Configuration.ConfigurationPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.Common.DBDataPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.Odbc.OdbcPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.OleDb.OleDbPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName>
- <xref:System.Data.SqlClient.SqlClientPermissionAttribute?displayProperty=fullName>
- <xref:System.Diagnostics.EventLogPermissionAttribute?displayProperty=fullName>
- <xref:System.Diagnostics.PerformanceCounterPermissionAttribute?displayProperty=fullName>
- <xref:System.DirectoryServices.DirectoryServicesPermissionAttribute?displayProperty=fullName>
- <xref:System.Drawing.Printing.PrintingPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.DnsPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.SocketPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.WebPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.Mail.SmtpPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.NetworkInformation.NetworkInformationPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.PnrpPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.Collaboration.PeerCollaborationPermissionAttribute?displayProperty=fullName>
- <xref:System.ServiceProcess.ServiceControllerPermissionAttribute?displayProperty=fullName>
- <xref:System.Transactions.DistributedTransactionPermissionAttribute?displayProperty=fullName>
- <xref:System.Web.AspNetHostingPermissionAttribute?displayProperty=fullName>

<span data-ttu-id="3f069-152">Interfejsów</span><span class="sxs-lookup"><span data-stu-id="3f069-152">Interfaces:</span></span>

- <xref:System.Security.Permissions.IUnrestrictedPermission?displayProperty=fullName>
- <xref:System.Security.IPermission?displayProperty=fullName>
- <xref:System.Security.IStackWalk?displayProperty=fullName>
- <xref:System.Security.Policy.IIdentityPermissionFactory?displayProperty=fullName>

<span data-ttu-id="3f069-153">Klasy, które implementują `IStackWalk` :</span><span class="sxs-lookup"><span data-stu-id="3f069-153">Classes that implement `IStackWalk`:</span></span>

- <xref:System.Security.NamedPermissionSet?displayProperty=fullName>
- <xref:System.Security.PermissionSet?displayProperty=fullName>

<span data-ttu-id="3f069-154">Klasy, które implementują `IPermission` :</span><span class="sxs-lookup"><span data-stu-id="3f069-154">Classes that implement `IPermission`:</span></span>

- <xref:System.Security.CodeAccessPermission?displayProperty=fullName>

<span data-ttu-id="3f069-155">Klasy, które pochodzą z `CodeAccessPermission` :</span><span class="sxs-lookup"><span data-stu-id="3f069-155">Classes that derive from `CodeAccessPermission`:</span></span>

- <xref:System.Configuration.ConfigurationPermission?displayProperty=fullName>
- <xref:System.Data.Common.DBDataPermission?displayProperty=fullName>
- <xref:System.Data.Odbc.OdbcPermission?displayProperty=fullName>
- <xref:System.Data.OleDb.OleDbPermission?displayProperty=fullName>
- <xref:System.Data.SqlClient.SqlClientPermission?displayProperty=fullName>
- <xref:System.Data.OracleClient.OraclePermission?displayProperty=fullName>
- <xref:System.Drawing.Printing.PrintingPermission?displayProperty=fullName>
- <xref:System.Net.DnsPermission?displayProperty=fullName>
- <xref:System.Net.SocketPermission?displayProperty=fullName>
- <xref:System.Net.WebPermission?displayProperty=fullName>
- <xref:System.Net.Mail.SmtpPermission?displayProperty=fullName>
- <xref:System.Net.NetworkInformation.NetworkInformationPermission?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.PnrpPermission?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.Collaboration.PeerCollaborationPermission?displayProperty=fullName>
- <xref:System.Transactions.DistributedTransactionPermission?displayProperty=fullName>
- <xref:System.Web.AspNetHostingPermission?displayProperty=fullName>
- <xref:System.Xaml.Permissions.XamlLoadPermission?displayProperty=fullName>

<span data-ttu-id="3f069-156">Klasy, które pochodzą z `ResourcePermissionBase` :</span><span class="sxs-lookup"><span data-stu-id="3f069-156">Classes that derive from `ResourcePermissionBase`:</span></span>

- <xref:System.Diagnostics.EventLogPermission?displayProperty=fullName>
- <xref:System.Diagnostics.PerformanceCounterPermission?displayProperty=fullName>
- <xref:System.DirectoryServices.DirectoryServicesPermission?displayProperty=fullName>
- <xref:System.ServiceProcess.ServiceControllerPermission?displayProperty=fullName>

<span data-ttu-id="3f069-157">Wyliczenia w `System.Security.Permissions` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="3f069-157">Enums in the `System.Security.Permissions` namespace:</span></span>

- <xref:System.Security.Permissions.DataProtectionPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.HostProtectionResource?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageContainment?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionAudio?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionImage?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionVideo?displayProperty=fullName>
- <xref:System.Security.Permissions.PermissionState?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermissionFlag?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionClipboard?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionWindow?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermissionLevel?displayProperty=fullName>

<span data-ttu-id="3f069-158">Klasy i składowe, które są zależne od typów zabezpieczeń dostępu kodu:</span><span class="sxs-lookup"><span data-stu-id="3f069-158">Classes and members that depend on code access security types:</span></span>

- <xref:System.AppDomain.PermissionSet?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.AllowReversePInvokeCallsAttribute?displayProperty=fullName>
- <xref:System.Security.HostProtectionException?displayProperty=fullName>
- <xref:System.Security.Policy.FileCodeGroup?displayProperty=fullName>
- <xref:System.Security.Policy.StrongName?displayProperty=fullName>
- <xref:System.Security.Policy.StrongNameMembershipCondition?displayProperty=fullName>
- [<span data-ttu-id="3f069-159">System. Security. Policy. ApplicationTrust. ApplicationTrust (PermissionSet, IEnumerable \<StrongName> )</span><span class="sxs-lookup"><span data-stu-id="3f069-159">System.Security.Policy.ApplicationTrust.ApplicationTrust(PermissionSet, IEnumerable\<StrongName>)</span></span>](/dotnet/api/system.security.policy.applicationtrust.-ctor#System_Security_Policy_ApplicationTrust__ctor_System_Security_PermissionSet_System_Collections_Generic_IEnumerable_System_Security_Policy_StrongName__)
- <xref:System.Security.Policy.ApplicationTrust.FullTrustAssemblies?displayProperty=fullName>
- <xref:System.Security.Policy.GacInstalled?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyStatement.%23ctor%2A?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.AddNamedPermissionSet(System.Security.NamedPermissionSet)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.ChangeNamedPermissionSet(System.String,System.Security.PermissionSet)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.GetNamedPermissionSet(System.String)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.RemoveNamedPermissionSet(System.String)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.RemoveNamedPermissionSet(System.Security.NamedPermissionSet)?displayProperty=nameWithType>
- <xref:System.Security.Policy.PolicyStatement.PermissionSet?displayProperty=fullName>
- <xref:System.Security.Policy.Publisher?displayProperty=fullName>
- <xref:System.Security.Policy.Site?displayProperty=fullName>
- <xref:System.Security.Policy.Url?displayProperty=fullName>
- <xref:System.Security.Policy.Zone?displayProperty=fullName>
- <xref:System.Security.SecurityManager?displayProperty=fullName>

### <a name="syslib0004"></a><span data-ttu-id="3f069-160">SYSLIB0004</span><span class="sxs-lookup"><span data-stu-id="3f069-160">SYSLIB0004</span></span>

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(System.Runtime.CompilerServices.RuntimeHelpers.TryCode,System.Runtime.CompilerServices.RuntimeHelpers.CleanupCode,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegionsNoOP?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareContractedDelegate(System.Delegate)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ProbeForSufficientStack?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Cer?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Consistency?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute?displayProperty=nameWithType>

### <a name="syslib0005"></a><span data-ttu-id="3f069-161">SYSLIB0005</span><span class="sxs-lookup"><span data-stu-id="3f069-161">SYSLIB0005</span></span>

- <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=nameWithType>

### <a name="syslib0006"></a><span data-ttu-id="3f069-162">SYSLIB0006</span><span class="sxs-lookup"><span data-stu-id="3f069-162">SYSLIB0006</span></span>

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

### <a name="syslib0007"></a><span data-ttu-id="3f069-163">SYSLIB0007</span><span class="sxs-lookup"><span data-stu-id="3f069-163">SYSLIB0007</span></span>

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

### <a name="syslib0008"></a><span data-ttu-id="3f069-164">SYSLIB0008</span><span class="sxs-lookup"><span data-stu-id="3f069-164">SYSLIB0008</span></span>

- <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType>

### <a name="syslib0009"></a><span data-ttu-id="3f069-165">SYSLIB0009</span><span class="sxs-lookup"><span data-stu-id="3f069-165">SYSLIB0009</span></span>

- <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType>
- <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType>

### <a name="syslib0010"></a><span data-ttu-id="3f069-166">SYSLIB0010</span><span class="sxs-lookup"><span data-stu-id="3f069-166">SYSLIB0010</span></span>

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType>

### <a name="syslib0011"></a><span data-ttu-id="3f069-167">SYSLIB0011</span><span class="sxs-lookup"><span data-stu-id="3f069-167">SYSLIB0011</span></span>

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

### <a name="syslib0012"></a><span data-ttu-id="3f069-168">SYSLIB0012</span><span class="sxs-lookup"><span data-stu-id="3f069-168">SYSLIB0012</span></span>

- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType>
