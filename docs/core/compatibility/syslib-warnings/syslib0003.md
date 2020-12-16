---
title: Ostrzeżenie SYSLIB0003
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0003 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 9ef394408c108859abccda504f70694e5b345677
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596591"
---
# <a name="syslib0003-code-access-security-is-not-supported"></a><span data-ttu-id="fe7c6-103">SYSLIB0003: zabezpieczenia dostępu kodu nie są obsługiwane</span><span class="sxs-lookup"><span data-stu-id="fe7c6-103">SYSLIB0003: Code access security is not supported</span></span>

<span data-ttu-id="fe7c6-104">[Zabezpieczenia dostępu kodu (CAS)](../../../framework/data/adonet/code-access-security.md) to nieobsługiwana, Starsza technologia.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-104">[Code access security (CAS)](../../../framework/data/adonet/code-access-security.md) is an unsupported, legacy technology.</span></span> <span data-ttu-id="fe7c6-105">Infrastruktura umożliwiająca obsługę urzędów certyfikacji, która istnieje tylko w .NET Framework 2. x-4. x, jest przestarzała i nie otrzymuje poprawek do obsługi lub zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-105">The infrastructure to enable CAS, which exists only in .NET Framework 2.x - 4.x, is deprecated and not receiving servicing or security fixes.</span></span>

<span data-ttu-id="fe7c6-106">W związku z tym większość typów związanych z zabezpieczeniami dostępu kodu (CAS) w programie .NET jest przestarzałych, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-106">As a result, most code access security (CAS)-related types in .NET are obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="fe7c6-107">Obejmuje to atrybuty CAS, takie jak <xref:System.Security.Permissions.SecurityPermissionAttribute> obiekty uprawnień urzędów certyfikacji, takie <xref:System.Net.SocketPermission> jak <xref:System.Security.Policy.EvidenceBase> Typy pochodne i inne pomocnicze interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-107">This includes CAS attributes, such as <xref:System.Security.Permissions.SecurityPermissionAttribute>, CAS permission objects, such as <xref:System.Net.SocketPermission>, <xref:System.Security.Policy.EvidenceBase>-derived types, and other supporting APIs.</span></span> <span data-ttu-id="fe7c6-108">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0003` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-108">Using these APIs generates warning `SYSLIB0003` at compile time.</span></span>

<span data-ttu-id="fe7c6-109">Kompletna lista przestarzałych interfejsów API urzędów certyfikacji jest następująca:</span><span class="sxs-lookup"><span data-stu-id="fe7c6-109">The complete list of obsolete CAS APIs is as follows:</span></span>

- <xref:System.AppDomain.PermissionSet?displayProperty=fullName>
- <xref:System.Configuration.ConfigurationPermission?displayProperty=fullName>
- <xref:System.Configuration.ConfigurationPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.Common.DBDataPermission?displayProperty=fullName>
- <xref:System.Data.Common.DBDataPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.Odbc.OdbcPermission?displayProperty=fullName>
- <xref:System.Data.Odbc.OdbcPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.OleDb.OleDbPermission?displayProperty=fullName>
- <xref:System.Data.OleDb.OleDbPermissionAttribute?displayProperty=fullName>
- <xref:System.Data.OracleClient.OraclePermission?displayProperty=fullName>
- <xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName>
- <xref:System.Data.SqlClient.SqlClientPermission?displayProperty=fullName>
- <xref:System.Data.SqlClient.SqlClientPermissionAttribute?displayProperty=fullName>
- <xref:System.Diagnostics.EventLogPermission?displayProperty=fullName>
- <xref:System.Diagnostics.EventLogPermissionAttribute?displayProperty=fullName>
- <xref:System.Diagnostics.PerformanceCounterPermission?displayProperty=fullName>
- <xref:System.Diagnostics.PerformanceCounterPermissionAttribute?displayProperty=fullName>
- <xref:System.DirectoryServices.DirectoryServicesPermission?displayProperty=fullName>
- <xref:System.DirectoryServices.DirectoryServicesPermissionAttribute?displayProperty=fullName>
- <xref:System.Drawing.Printing.PrintingPermission?displayProperty=fullName>
- <xref:System.Drawing.Printing.PrintingPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.DnsPermission?displayProperty=fullName>
- <xref:System.Net.DnsPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.Mail.SmtpPermission?displayProperty=fullName>
- <xref:System.Net.Mail.SmtpPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.NetworkInformation.NetworkInformationPermission?displayProperty=fullName>
- <xref:System.Net.NetworkInformation.NetworkInformationPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.Collaboration.PeerCollaborationPermission?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.Collaboration.PeerCollaborationPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.PnrpPermission?displayProperty=fullName>
- <xref:System.Net.PeerToPeer.PnrpPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.SocketPermission?displayProperty=fullName>
- <xref:System.Net.SocketPermissionAttribute?displayProperty=fullName>
- <xref:System.Net.WebPermission?displayProperty=fullName>
- <xref:System.Net.WebPermissionAttribute?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.AllowReversePInvokeCallsAttribute?displayProperty=fullName>
- <xref:System.Security.CodeAccessPermission?displayProperty=fullName>
- <xref:System.Security.HostProtectionException?displayProperty=fullName>
- <xref:System.Security.IPermission?displayProperty=fullName>
- <xref:System.Security.IStackWalk?displayProperty=fullName>
- <xref:System.Security.NamedPermissionSet?displayProperty=fullName>
- <xref:System.Security.PermissionSet?displayProperty=fullName>
- <xref:System.Security.Permissions.CodeAccessSecurityAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.DataProtectionPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.DataProtectionPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.DataProtectionPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.EnvironmentPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.FileDialogPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.FileIOPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.GacIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.GacIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.HostProtectionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.HostProtectionResource?displayProperty=fullName>
- <xref:System.Security.Permissions.IUnrestrictedPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageContainment?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageFilePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStorageFilePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStoragePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.IsolatedStoragePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntry?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntryCollection?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAccessEntryEnumerator?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.KeyContainerPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionAudio?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionImage?displayProperty=fullName>
- <xref:System.Security.Permissions.MediaPermissionVideo?displayProperty=fullName>
- <xref:System.Security.Permissions.PermissionSetAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.PermissionState?displayProperty=fullName>
- <xref:System.Security.Permissions.PrincipalPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.PublisherIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.PublisherIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermissionAccess?displayProperty=fullName>
- <xref:System.Security.Permissions.RegistryPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.ResourcePermissionBase?displayProperty=fullName>
- <xref:System.Security.Permissions.ResourcePermissionBaseEntry?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.SecurityPermissionFlag?displayProperty=fullName>
- <xref:System.Security.Permissions.SiteIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.SiteIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermission?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StorePermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNameIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.StrongNamePublicKeyBlob?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.TypeDescriptorPermissionFlags?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionClipboard?displayProperty=fullName>
- <xref:System.Security.Permissions.UIPermissionWindow?displayProperty=fullName>
- <xref:System.Security.Permissions.UrlIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.UrlIdentityPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermissionAttribute?displayProperty=fullName>
- <xref:System.Security.Permissions.WebBrowserPermissionLevel?displayProperty=fullName>
- <xref:System.Security.Permissions.ZoneIdentityPermission?displayProperty=fullName>
- <xref:System.Security.Permissions.ZoneIdentityPermissionAttribute?displayProperty=fullName>
- [<span data-ttu-id="fe7c6-110">System. Security. Policy. ApplicationTrust. ApplicationTrust (PermissionSet, IEnumerable \<StrongName> )</span><span class="sxs-lookup"><span data-stu-id="fe7c6-110">System.Security.Policy.ApplicationTrust.ApplicationTrust(PermissionSet, IEnumerable\<StrongName>)</span></span>](/dotnet/api/system.security.policy.applicationtrust.-ctor#System_Security_Policy_ApplicationTrust__ctor_System_Security_PermissionSet_System_Collections_Generic_IEnumerable_System_Security_Policy_StrongName__)
- <xref:System.Security.Policy.ApplicationTrust.FullTrustAssemblies?displayProperty=fullName>
- <xref:System.Security.Policy.FileCodeGroup?displayProperty=fullName>
- <xref:System.Security.Policy.GacInstalled?displayProperty=fullName>
- <xref:System.Security.Policy.IIdentityPermissionFactory?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.AddNamedPermissionSet(System.Security.NamedPermissionSet)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.ChangeNamedPermissionSet(System.String,System.Security.PermissionSet)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.GetNamedPermissionSet(System.String)?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyLevel.RemoveNamedPermissionSet%2A?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyStatement.PermissionSet?displayProperty=fullName>
- <xref:System.Security.Policy.PolicyStatement.%23ctor%2A?displayProperty=fullName>
- <xref:System.Security.Policy.Publisher?displayProperty=fullName>
- <xref:System.Security.Policy.Site?displayProperty=fullName>
- <xref:System.Security.Policy.StrongName?displayProperty=fullName>
- <xref:System.Security.Policy.StrongNameMembershipCondition?displayProperty=fullName>
- <xref:System.Security.Policy.Url?displayProperty=fullName>
- <xref:System.Security.Policy.Zone?displayProperty=fullName>
- <xref:System.Security.SecurityManager?displayProperty=fullName>
- <xref:System.ServiceProcess.ServiceControllerPermission?displayProperty=fullName>
- <xref:System.ServiceProcess.ServiceControllerPermissionAttribute?displayProperty=fullName>
- <xref:System.Transactions.DistributedTransactionPermission?displayProperty=fullName>
- <xref:System.Transactions.DistributedTransactionPermissionAttribute?displayProperty=fullName>
- <xref:System.Web.AspNetHostingPermission?displayProperty=fullName>
- <xref:System.Web.AspNetHostingPermissionAttribute?displayProperty=fullName>
- <xref:System.Xaml.Permissions.XamlLoadPermission?displayProperty=fullName>

## <a name="workarounds"></a><span data-ttu-id="fe7c6-111">Obejścia</span><span class="sxs-lookup"><span data-stu-id="fe7c6-111">Workarounds</span></span>

- <span data-ttu-id="fe7c6-112">W przypadku potwierdzenia uprawnień zabezpieczeń Usuń atrybut lub wywołanie, które potwierdza uprawnienie.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-112">If you're asserting any security permission, remove the attribute or call that asserts the permission.</span></span>

  ```csharp
  // REMOVE the attribute below.
  [SecurityPermission(SecurityAction.Assert, ControlThread = true)]
  public void DoSomething()
  {
  }
  public void DoAssert()
  {
      // REMOVE the line below.
      new SecurityPermission(SecurityPermissionFlag.ControlThread).Assert();
  }
  ```

- <span data-ttu-id="fe7c6-113">Jeśli masz odmowę lub ograniczenie (za pośrednictwem `PermitOnly` ) dowolnych uprawnień, skontaktuj się z doradcą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-113">If you're denying or restricting (via `PermitOnly`) any permission, contact your security advisor.</span></span> <span data-ttu-id="fe7c6-114">Ponieważ atrybuty urzędów certyfikacji nie są uznawane przez środowisko uruchomieniowe programu .NET 5.0 +, aplikacja może mieć otwór bezpieczeństwa, jeśli nie opiera się on na infrastrukturze CAS w celu ograniczenia dostępu do tych metod.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-114">Because CAS attributes are not honored by the .NET 5.0+ runtime, your application could have a security hole if it incorrectly relies on the CAS infrastructure to restrict access to these methods.</span></span>

  ```csharp
  // REVIEW the attribute below; could indicate security vulnerability.
  [SecurityPermission(SecurityAction.Deny, ControlThread = true)]
  public void DoSomething()
  {
  }
  public void DoPermitOnly()
  {
      // REVIEW the line below; could indicate security vulnerability.
      new SecurityPermission(SecurityPermissionFlag.ControlThread).PermitOnly();
  }
  ```

- <span data-ttu-id="fe7c6-115">Jeśli masz jakieś uprawnienia (z wyjątkiem <xref:System.Security.Permissions.PrincipalPermission> ), Usuń żądanie.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-115">If you're demanding any permission (except <xref:System.Security.Permissions.PrincipalPermission>), remove the demand.</span></span> <span data-ttu-id="fe7c6-116">Wszystkie wymagania zakończą się pomyślnie w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="fe7c6-116">All demands will succeed at run time.</span></span>

  ```csharp
  // REMOVE the attribute below; it will always succeed.
  [SecurityPermission(SecurityAction.Demand, ControlThread = true)]
  public void DoSomething()
  {
  }
  public void DoDemand()
  {
      // REMOVE the line below; it will always succeed.
      new SecurityPermission(SecurityPermissionFlag.ControlThread).Demand();
  }
  ```

- <span data-ttu-id="fe7c6-117">Jeśli masz wymaganie <xref:System.Security.Permissions.PrincipalPermission> , zapoznaj się z tematem wskazówki dotyczące [SYSLIB0002: PrincipalPermissionAttribute jest przestarzałe](syslib0002.md#workarounds).</span><span class="sxs-lookup"><span data-stu-id="fe7c6-117">If you're demanding <xref:System.Security.Permissions.PrincipalPermission>, consult the guidance for [SYSLIB0002: PrincipalPermissionAttribute is obsolete](syslib0002.md#workarounds).</span></span> <span data-ttu-id="fe7c6-118">Te wskazówki dotyczą zarówno programu <xref:System.Security.Permissions.PrincipalPermission> , jak i <xref:System.Security.Permissions.PrincipalPermissionAttribute> .</span><span class="sxs-lookup"><span data-stu-id="fe7c6-118">That guidance applies for both <xref:System.Security.Permissions.PrincipalPermission> and <xref:System.Security.Permissions.PrincipalPermissionAttribute>.</span></span>

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="fe7c6-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="fe7c6-119">See also</span></span>

- [<span data-ttu-id="fe7c6-120">SYSLIB0002: PrincipalPermissionAttribute jest przestarzała</span><span class="sxs-lookup"><span data-stu-id="fe7c6-120">SYSLIB0002: PrincipalPermissionAttribute is obsolete</span></span>](syslib0002.md)
