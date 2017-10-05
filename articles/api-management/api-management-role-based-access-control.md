---
title: "Jak używać kontroli dostępu opartej na rolach w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użyć wbudowanych ról i tworzyć role niestandardowe w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: fa757a591d788f52d759bc24accedd3c55149ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-role-based-access-control-in-azure-api-management"></a>Jak używać kontroli dostępu opartej na rolach w usłudze Azure API Management
Zarządzanie interfejsami API Azure polega na kontroli dostępu based (RBAC) umożliwia precyzyjne zarządzanie dostępem dla usługi interfejsu API zarządzania i jednostek (np. interfejsów API, zasady). Ten artykuł zawiera przegląd ról wbudowanych i niestandardowych w usłudze API Management. Aby uzyskać więcej informacji na temat zarządzania dostępem w portalu Azure, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Wbudowane role
Zarządzanie interfejsami API obecnie zawiera wbudowane role 3 i doda 2 jedną rolę w najbliższej przyszłości. W innych zakresach, łącznie z subskrypcji, grupy zasobów, a poszczególne wystąpienia interfejsu API zarządzania można przypisać tych ról. Na przykład jeśli rola "Azure API Management usługi czytnika" jest przypisana do użytkownika na poziomie grupy zasobów, użytkownik ma dostęp do odczytu do wszystkich wystąpień usługi API Management znajdującej się w grupie zasobów. 

Poniższa tabela zawiera krótkie opisy wbudowane role. Można przypisać te role przy użyciu portalu Azure lub innych narzędzi, w tym na platformie Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [interfejsu wiersza polecenia](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), i [interfejsu API REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Aby uzyskać szczegółowe informacje dotyczące sposobu przypisywania ról wbudowanych, zobacz [zarządzanie dostępem do zasobów subskrypcji platformy Azure za pomocą przypisań ról](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rola          | Dostęp do odczytu<sup>[1]</sup> | Dostęp do zapisu<sup>[2]</sup> | Tworzenie usług, usuwanie, skalowanie sieci VPN i Konfiguracja domeny niestandardowej | Dostęp do portalu Publsiher starszej wersji | Opis
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API Management usługi współautora | ✓ | ✓ | ✓ | ✓ | Użytkownika nadrzędnego. Ma pełny dostęp CRUD do usługi API Management i jednostek (np. interfejsów API, zasady). Ma dostęp do portalu starszych wydawcy. |
| Czytnik usługi zarządzania interfejsu API platformy Azure | ✓ | | || Ma dostęp tylko do odczytu do usługi API Management i jednostek. |
| Operator usługi zarządzania interfejsu API platformy Azure | ✓ | | ✓ | | Można zarządzać usługi API Management, ale nie jednostek.|
| Edytor usługi zarządzania w usłudze Azure interfejsu API<sup>*</sup> | ✓ | ✓ | |  | Można zarządzać zarządzanie interfejsami API jednostek, ale nie usług.|
| Azure API Management Content Manager<sup>*</sup> | ✓ | | | ✓ | Można zarządzać portalu dla deweloperów. Dostęp tylko do odczytu do usługi i jednostek.|

<sup>[1] dostęp do odczytu do usługi API Management i jednostek (np. interfejsów API, zasad)</sup>

<sup>[2] do zapisu usługi interfejsu API zarządzania i jednostkami, z wyjątkiem następujących opeartions: 1) wystąpienia tworzenie, usuwanie i skalowanie Konfigurowanie nazwy domeny niestandardowe 3) konfiguracji sieci VPN 2)</sup>

<sup>\*Edytor usługi roli będą dostępne po możemy migracji wszystkich admin interfejsu użytkownika z istniejącego portalu wydawcy do portalu Azure. Rola menedżera zawartości będą dostępne po portalu wydawcy został zrefaktoryzowany obejmowało tylko funkcje związane z zarządzaniem portalu dla deweloperów.</sup>  


## <a name="custom-roles"></a>Role niestandardowe
Jeśli żadna z wbudowanych ról nie spełnia określonych potrzeb, można tworzyć role niestandardowe do zapewnienia bardziej szczegółowe zarządzanie dostępem dla interfejsu API zarządzania jednostek. Na przykład można utworzyć niestandardową rolę, który ma dostęp tylko do odczytu do usługi API Management, ale ma zapisu dostęp tylko do jednego interfejsu API. Aby uzyskać więcej informacji o niestandardowych rolach, zobacz [role niestandardowe w Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Po utworzeniu niestandardowej roli zabezpieczeń, łatwiej rozpocząć od jednego z wbudowanych ról. Edytuj atrybuty dodawanie działań, NotActions lub AssignableScopes, a następnie zapisz zmiany jako nową rolę. W poniższym przykładzie rozpoczyna się od roli "Czytnika usługi Managment interfejsu API platformy Azure" i tworzy niestandardowej roli zabezpieczeń o nazwie "Kalkulator Edytor interfejsu API". Tworzona rola niestandardowa można przypisać tylko do określonego interfejsu API w związku z tym będzie ma dostęp tylko do tego interfejsu API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access to Contoso APIM instance and write access to the Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of the user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Obejrzyj film wideo

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o opartej na rolach kontroli dostępu na platformie Azure
  * [Wprowadzenie do zarządzania dostępem w witrynie Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Zarządzanie dostępem do zasobów subskrypcji platformy Azure za pomocą przypisań ról](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Role niestandardowe w Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
