---
title: Repozytoria rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak używać repozytoria rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a>Utwórz prywatne rejestru kontenera Docker przy użyciu programu Azure PowerShell
Używanie poleceń w [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) Tworzenie rejestru kontenera i zarządzanie nimi jego ustawienia z komputera z systemem Windows. Można również tworzyć i zarządzać przy użyciu rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md), [interfejsu wiersza polecenia Azure](container-registry-get-started-azure-cli.md), lub programowo z rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Podstawy oraz pojęcia zostały przedstawione w części [ — omówienie](container-registry-intro.md)
* Aby uzyskać pełną listę obsługiwanych poleceń cmdlet, zobacz [poleceń cmdlet do zarządzania Azure kontenera rejestru](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Wymagania wstępne
* **Program Azure PowerShell**: Aby zainstalować i rozpocząć pracę z programem Azure PowerShell, zobacz [instrukcje dotyczące instalacji](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Zaloguj się do subskrypcji platformy Azure, uruchamiając polecenie `Login-AzureRMAccount`. Aby uzyskać więcej informacji, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów. Upewnij się, że grupa zasobów znajduje się w lokalizacji, w której usługa Container Registry jest [dostępna](https://azure.microsoft.com/regions/services/). Aby utworzyć grupę zasobów, przy użyciu programu Azure PowerShell, zobacz [dokumentacji programu PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Konto magazynu** (opcjonalnie): utwórz standardowe [konto magazynu](../storage/common/storage-introduction.md) platformy Azure, aby obsługiwać rejestr kontenerów w tej samej lokalizacji. Jeśli nie określisz konta magazynu podczas tworzenia rejestru przy użyciu polecenia `New-AzureRMContainerRegistry`, polecenie spowoduje utworzenie go dla Ciebie. Aby utworzyć konto magazynu przy użyciu programu PowerShell, zobacz [dokumentacji programu PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Usługa Premium Storage nie jest obecnie obsługiwana.
* **Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru przy użyciu programu PowerShell, domyślnie go nie ustawiono dostępu. W zależności od potrzeb można przypisać istniejącej nazwy głównej usługi Azure Active Directory do rejestru lub Utwórz i przypisz nowe. Alternatywnie można włączyć konta administratora w rejestrze. Zobacz sekcje w dalszej części tego artykułu. Więcej informacji dotyczących dostępu do rejestru znajduje się w temacie [Authenticate with a container registry](container-registry-authentication.md) (Uwierzytelnianie za pomocą rejestru kontenera).

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów
Uruchom polecenie `New-AzureRMContainerRegistry`, aby utworzyć rejestr kontenera.

> [!TIP]
> Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry. W przykładach nazwa rejestru to `MyRegistry`, ale możesz ją zastąpić własną, unikatową nazwą.
>
>

Następujące polecenie używa minimalnej liczby parametrów do utworzenia kontenera rejestru `MyRegistry` w grupie zasobów `MyResourceGroup` w lokalizacji Południowo-środkowe stany USA:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* Parametr `-StorageAccountName` jest opcjonalny. Jeśli nie określono inaczej, nazwa konta magazynu utworzonego we wskazanej grupie zasobów składa się z nazwy rejestru i sygnatury czasowej.

## <a name="assign-a-service-principal"></a>Przypisywanie nazwy głównej usługi
Przypisz usługi Azure Active Directory za pomocą poleceń programu PowerShell [nazwy głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md) rejestru. W tych przykładach do nazwy głównej usługi przypisano rolę Właściciel, ale możesz przypisywać [inne role](../active-directory/role-based-access-control-configure.md).

### <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi
W poniższym poleceniu utworzono nową główną nazwę usługi. Określ silne hasło przy użyciu parametru `-Password`.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Przypisanie nazwy głównej usługi nowego lub istniejącego
Nowej lub istniejącej nazwy głównej usługi można przypisać do rejestru. Aby przypisać właściciela roli dostępu do rejestru, uruchom polecenie podobne do poniższego przykładu:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a>Zaloguj się w rejestrze z nazwy głównej usługi
Po przypisaniu nazwy głównej usługi w rejestrze, należy zalogować się przy użyciu następującego polecenia:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Zarządzanie poświadczeniami administratora
Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone. Poniżej przedstawiono polecenia programu PowerShell do zarządzania poświadczeń administratora dla kontenera rejestru.

### <a name="obtain-admin-user-credentials"></a>Uzyskiwanie poświadczeń użytkownika administratora
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Włączanie użytkownika administratora dla istniejącego rejestru
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Wyłączanie użytkownika administratora dla istniejącego rejestru
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Następne kroki
* [Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md) (Wypychanie pierwszego obrazu za pomocą interfejsu wiersza polecenia platformy Docker)
