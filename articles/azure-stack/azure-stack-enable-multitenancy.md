---
title: "Włącz wielodostępność stosu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak obsługiwać wiele katalogów usługi Azure Active Directory w stosie Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: helaw
ms.openlocfilehash: a2cba85a553f20040d2fb118b35859b05870e361
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="enable-multi-tenancy-in-azure-stack"></a>Włącz wielodostępność stosu Azure

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Można skonfigurować stosu Azure do obsługi użytkowników z wieloma dzierżawcami usługi Azure Active Directory (Azure AD) do użycia usług Azure stosu. Na przykład rozważmy następujący scenariusz:

 - Jesteś administratorem usługi contoso.onmicrosoft.com, których zainstalowano Azure Stack.
 - Joanna jest administratorem katalogu fabrikam.onmicrosoft.com, w którym znajdują się użytkownicy gościa. 
 - Joanna przez firmy odbiera usługi IaaS i PaaS w firmie i wymaga umożliwić użytkownikom w katalogu gościa (fabrikam.onmicrosoft.com) Zaloguj się i korzystać z zasobów Azure stosu w contoso.onmicrosoft.com.

Ten przewodnik zawiera kroki wymagane w kontekście tego scenariusza, aby skonfigurować wielodostępność stosu Azure.  W tym scenariuszu należy i Joanna należy wykonać kroki, aby umożliwić użytkownikom z firmy Fabrikam zalogować się i korzystać z usług Azure stosu wdrożenia w firmie Contoso.  

## <a name="before-you-begin"></a>Przed rozpoczęciem
Istnieje kilka wstępnie wymaganych elementów do uwzględnienia przed skonfigurowaniem wielodostępność stosu Azure:
  
 - Możesz i Joanna musi koordynować czynności administracyjne w katalogu Azure stosu jest zainstalowana w (Contoso) i katalog gościa (Fabrikam).  
 - Upewnij się, że znasz [zainstalowane](azure-stack-powershell-install.md) i [skonfigurowane](azure-stack-powershell-configure-admin.md) programu PowerShell dla usługi Azure stosu.
 - [Pobierz narzędzia stosu Azure](azure-stack-powershell-download.md)i zaimportuj moduły Connect i tożsamości:

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - Joanna będzie wymagać [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) dostęp do usługi Azure stosu. 

## <a name="configure-azure-stack-directory"></a>Skonfiguruj katalog Azure stosu
W tej sekcji skonfigurujesz stosu Azure umożliwia logowania z firmy Fabrikam usługi Azure AD directory dzierżawcami.

### <a name="onboard-guest-directory-tenant"></a>Gość dołączyć katalogu dzierżawcy
Następny, dołączyć dzierżawy katalogu gościa (Fabrikam) Azure stosu.  Ten krok obejmuje skonfigurowanie usługi Azure Resource Manager może akceptować użytkowników i nazwy główne usług dzierżawy usługi directory gościa.

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace the value below with the Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a>Skonfiguruj katalog gościa
Po wykonaniu kroków w katalogu Azure stosu Joanna musi dostarczyć zgodę na dostęp do katalogu gościa stos Azure i zarejestruj stosu Azure z katalogu gościa. 

### <a name="registering-azure-stack-with-the-guest-directory"></a>Rejestrowanie Azure stosu w katalogu gościa
Gdy administrator katalogu gościa udostępnił zgody na stos Azure na dostęp do katalogu w firmie Fabrikam, muszą zarejestrować stosu Azure z dzierżawcą katalogu firmy.

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName `
 -Verbose 
````
## <a name="direct-users-to-sign-in"></a>Bezpośrednie użytkownikom na logowanie
Teraz, możesz i Joanna zostały wykonane kroki do katalogu dołączyć Joanna, Joanna przekierować użytkowników Fabrikam do logowania.  Firma Fabrikam (to znaczy, że użytkownicy z sufiksem fabrikam.onmicrosoft.com) logowania, przechodząc na stronę https://portal.local.azurestack.external.  

Joanna kieruje żadnego [obce podmioty](../active-directory/active-directory-understanding-resource-access.md) w katalogu firmy Fabrikam (to znaczy użytkowników w katalogu firmy Fabrikam bez sufiks fabrikam.onmicrosoft.com) zalogowanie się przy użyciu https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Jeśli nie należy używać tego adresu URL, są wysyłane do ich domyślny katalog (Fabrikam) i komunikat o błędzie z informacją, że nie zgodził ich administratora.

## <a name="next-steps"></a>Następne kroki

- [Zarządzanie dostawcami delegowanego](azure-stack-delegated-provider.md)
- [Kluczowe założenia Azure stosu](azure-stack-key-features.md)
