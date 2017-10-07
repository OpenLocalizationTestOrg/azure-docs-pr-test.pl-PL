---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Utwórz prywatne rejestru kontenera Docker przy użyciu hello Azure PowerShell
Używanie poleceń w [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate rejestru kontenera i zarządzać jego ustawienia z komputera z systemem Windows. Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md), hello [interfejsu wiersza polecenia Azure](container-registry-get-started-azure-cli.md), lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Tło i pojęcia dla [hello — omówienie](container-registry-intro.md)
* Aby uzyskać pełną listę obsługiwanych poleceń cmdlet, zobacz [poleceń cmdlet do zarządzania Azure kontenera rejestru](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Wymagania wstępne
* **Program Azure PowerShell**: tooinstall i rozpocząć pracę z programem Azure PowerShell, zobacz hello [instrukcje dotyczące instalacji](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Zaloguj się za tooyour subskrypcji platformy Azure, uruchamiając `Login-AzureRMAccount`. Aby uzyskać więcej informacji, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów. Upewnij się, że grupa zasobów hello znajduje się w lokalizacji hello usługa Rejestr kontenera [dostępne](https://azure.microsoft.com/regions/services/). toocreate grupę zasobów, przy użyciu programu Azure PowerShell, zobacz [hello w programie PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Konto magazynu** (opcjonalnie): Utwórz standardowy Azure [konta magazynu](../storage/common/storage-introduction.md) tooback hello kontener klucza rejestru hello tej samej lokalizacji. Jeśli nie określisz konta magazynu podczas tworzenia rejestru z `New-AzureRMContainerRegistry`, hello polecenie tworzy go dla Ciebie. toocreate magazynu konta za pomocą programu PowerShell, zobacz [hello w programie PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Usługa Premium Storage nie jest obecnie obsługiwana.
* **Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru przy użyciu programu PowerShell, domyślnie go nie ustawiono dostępu. W zależności od potrzeb możesz przypisać istniejący Rejestr tooa główną usługi Azure Active Directory lub Utwórz i Przypisz nowy. Alternatywnie można włączyć rejestru hello konta administratora. Zobacz hello sekcje w dalszej części tego artykułu. Aby uzyskać więcej informacji na temat dostępu do rejestru, zobacz [Uwierzytelnij z rejestru kontenera hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów
Uruchom hello `New-AzureRMContainerRegistry` toocreate polecenia rejestru kontenera.

> [!TIP]
> Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry. Nazwa rejestru Hello w przykładach hello jest `MyRegistry`, ale podstawić własną unikatową nazwę.
>
>

Witaj następujące polecenia używa hello minimalnego parametry toocreate kontenera rejestru `MyRegistry` w grupie zasobów hello `MyResourceGroup` w hello lokalizacji południowo-środkowe stany:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* Parametr `-StorageAccountName` jest opcjonalny. Jeśli nie jest określony, konto magazynu jest tworzony z nazwą składającą się z nazwy rejestru hello i sygnaturę czasową w hello określonej grupy zasobów.

## <a name="assign-a-service-principal"></a>Przypisywanie nazwy głównej usługi
Użyj tooassign poleceń programu PowerShell usługi Azure Active Directory [nazwy głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa rejestru. Witaj nazwy głównej usługi w tych przykładach przypisany hello właściciela roli, ale można przypisać [innych ról](../active-directory/role-based-access-control-configure.md) Jeśli chcesz.

### <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi
W hello następujące polecenia utworzono nową główną nazwę usługi. Określ silne hasło z hello `-Password` parametru.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Przypisanie nazwy głównej usługi nowego lub istniejącego
Można przypisać nowej lub istniejącej rejestr tooa główną usługi. tooassign jej właściciela roli dostępu toohello rejestru, uruchom polecenie toohello podobne, poniższy przykład:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Zaloguj się w rejestrze toohello hello nazwy głównej usługi
Po przypisaniu rejestr toohello główna usługi hello, musisz zalogować się przy użyciu hello następujące polecenie:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Zarządzanie poświadczeniami administratora
Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone. Witaj poniższe przykłady przedstawiają poleceń programu PowerShell poświadczenia administratora hello toomanage rejestru kontenera.

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
* [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
