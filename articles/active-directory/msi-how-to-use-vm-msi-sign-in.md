---
title: "Jak używać Azure VM zarządzane tożsamości usługi w celu logowania się"
description: "Krok po kroku instrukcje i przykłady dotyczące przy użyciu zarejestrować nazwę główną usługi Azure VM MSI dla skryptu klienta i zasobów dostępu."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: bryanla
ms.openlocfilehash: 2e4da8cd02a1d07a3225a0c1fda4c60928dba8a4
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-use-an-azure-vm-managed-service-identity-msi-for-sign-in"></a>Jak używać usługi Azure VM zarządzane usługi tożsamości (MSI) w celu logowania się 

[!INCLUDE [preview-notice](../../includes/active-directory-msi-preview-notice.md)]  
Ten artykuł zawiera przykłady skryptów środowiska PowerShell i interfejsu wiersza polecenia dla Zaloguj się przy użyciu nazwy głównej usługi MSI i wskazówki dotyczące ważnych kwestii, takich jak obsługa błędów.

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

Jeśli planujesz używać programu Azure PowerShell lub interfejsu wiersza polecenia Azure przykłady w tym artykule, należy zainstalować najnowszą wersję [programu Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) lub [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

> [!IMPORTANT]
> - Wszystkie przykładowy skrypt w tym artykule przyjęto założenie, że klient wiersza polecenia jest uruchomiona na maszynie wirtualnej włączone MSI. Funkcja maszyny Wirtualnej "Połącz" w portalu Azure, aby zdalnie nawiązać połączenia z maszyną Wirtualną. Aby uzyskać więcej informacji na temat włączania MSI w maszynie Wirtualnej, zobacz [skonfigurować maszyny Wirtualnej zarządzane usługi tożsamości (MSI) przy użyciu portalu Azure](msi-qs-configure-portal-windows-vm.md), lub jednego z artykułów variant (przy użyciu programu PowerShell, interfejsu wiersza polecenia, szablonu lub zestawu SDK platformy Azure). 
> - Aby zapobiec błędom podczas dostępu do zasobów, MSI maszyny Wirtualnej należy podać co najmniej odpowiedni zakres dostępu "Czytnika" (maszyny Wirtualnej lub nowszej) umożliwia operacji usługi Azure Resource Manager na maszynie Wirtualnej. Zobacz [przypisywanie dostępu zarządzane tożsamości usługi (MSI) do zasobów przy użyciu portalu Azure](msi-howto-assign-access-portal.md) szczegółowe informacje.

## <a name="overview"></a>Przegląd

Udostępnia MSI [nazwy głównej usługi](develop/active-directory-dev-glossary.md#service-principal-object), która jest [utworzony po włączeniu MSI](msi-overview.md#how-does-it-work) na maszynie Wirtualnej. Nazwy głównej usługi można uzyskać dostęp do zasobów platformy Azure i użyć jako tożsamości dla skryptu/polecenia-wiersza klientów w celu logowania się i dostęp do zasobów. Tradycyjnie Aby uzyskać dostęp do zabezpieczonych zasobów w ramach jego tożsamość, klient skryptu musi:  

   - zostać zarejestrowane i zgodę z usługą Azure AD jako aplikacja kliencka poufne/sieci web
   - Zaloguj się w ramach jego nazwy głównej usługi, za pomocą poświadczeń aplikacji, (które mogą osadzony w skrypcie)

MSI klient skrypt nie musi już zrobić, zgodnie z jego Zaloguj się w obszarze nazwy głównej usługi MSI. 

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Poniższy skrypt pokazuje, jak:

1. Zaloguj się do usługi Azure AD w obszarze nazwy głównej usługi MSI maszyny Wirtualnej  
2. Wywołanie usługi Azure Resource Manager i Pobierz identyfikator podmiotu zabezpieczeń usługi maszyny Wirtualnej Interfejs wiersza polecenia odpowiada on za zarządzanie tokenu użycia nabycia zostanie automatycznie. Pamiętaj zastąpić nazwę maszyny wirtualnej dla `<VM-NAME>`.  

   ```azurecli
   az login --msi
   
   spID=$(az resource list -n <VM-NAME> --query [*].identity.principalId --out tsv)
   echo The MSI service principal ID is $spID
   ```

## <a name="azure-powershell"></a>Azure PowerShell

Poniższy skrypt pokazuje, jak:

1. Należy uzyskać token dostępu MSI dla maszyny Wirtualnej.  
2. Użyj tokenu dostępu do logowania do usługi Azure AD w odpowiedniej nazwy głównej usługi MSI.   
3. Wywołanie polecenia cmdlet usługi Azure Resource Manager, aby uzyskać informacje dotyczące maszyny Wirtualnej. Zarządzanie tokenu użycie automatycznie zapewnia obsługę programu PowerShell.  

   ```azurepowershell
   # Get an access token for the MSI
   $response = Invoke-WebRequest -Uri http://localhost:50342/oauth2/token `
                                 -Method GET -Body @{resource="https://management.azure.com/"} -Headers @{Metadata="true"}
   $content =$response.Content | ConvertFrom-Json
   $access_token = $content.access_token
   echo "The MSI access token is $access_token"

   # Use the access token to sign in under the MSI service principal. -AccountID can be any string to identify the session.
   Login-AzureRmAccount -AccessToken $access_token -AccountId "MSI@50342"

   # Call Azure Resource Manager to get the service principal ID for the VM's MSI. 
   $vmInfoPs = Get-AzureRMVM -ResourceGroupName <RESOURCE-GROUP> -Name <VM-NAME>
   $spID = $vmInfoPs.Identity.PrincipalId
   echo "The MSI service principal ID is $spID"
   ```

## <a name="resource-ids-for-azure-services"></a>Identyfikatory zasobów dla usług Azure

Zobacz [uwierzytelniania pomocy technicznej usługi Azure AD z usług Azure](msi-overview.md#azure-services-that-support-azure-ad-authentication) listę zasobów, które obsługują usługi Azure AD i zostały przetestowane msi, a ich odpowiednich identyfikatorów zasobów.

## <a name="error-handling-guidance"></a>Wskazówki dotyczące obsługi błędów 

Odpowiedzi na następujące może wskazywać, że MSI maszyny Wirtualnej nie został prawidłowo skonfigurowany:

- Środowiska PowerShell: *Invoke WebRequest: nie można nawiązać połączenia z serwerem zdalnym*
- Interfejs wiersza polecenia: *MSI: nie można pobrać tokenu z "http://localhost:50342/oauth2/token" z powodu błędu programu "HTTPConnectionPool (host = 'localhost', port = 50342)* 

Jeśli zostanie wyświetlony jeden z tych błędów, wróć do maszyny Wirtualnej platformy Azure w ramach [portalu Azure](https://portal.azure.com) oraz:

- Przejdź do **konfiguracji** strony i upewnij się, "Tożsamość usługi zarządzanej" ma ustawioną wartość "Yes".
- Przejdź do **rozszerzenia** strony i upewnij się, z rozszerzeniem MSI pomyślnie wdrożone.

Jeśli jest albo nieprawidłowa, może być konieczne ponownie Wdróż ponownie MSI na zasobie oraz rozwiązywania problemów dotyczących niepowodzenia wdrożenia. Zobacz [skonfigurować maszyny Wirtualnej zarządzane usługi tożsamości (MSI) przy użyciu portalu Azure](msi-qs-configure-portal-windows-vm.md) Jeśli potrzebujesz pomocy w konfiguracji maszyny Wirtualnej.

## <a name="related-content"></a>Zawartość pokrewna

- Aby włączyć MSI w maszynie Wirtualnej platformy Azure, zobacz [skonfigurować maszyny Wirtualnej zarządzane usługi tożsamości (MSI) przy użyciu programu PowerShell](msi-qs-configure-powershell-windows-vm.md), lub [skonfigurować maszyny Wirtualnej zarządzane usługi tożsamości (MSI) przy użyciu wiersza polecenia platformy Azure](msi-qs-configure-cli-windows-vm.md)

W poniższej sekcji komentarzy umożliwia wyrazić swoją opinię i pomóc nam dostosować i kształtu zawartość.








