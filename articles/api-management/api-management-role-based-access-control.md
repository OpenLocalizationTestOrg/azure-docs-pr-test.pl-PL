---
title: "tooUse aaaHow opartej na rolach kontroli dostępu w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello wbudowane role i tworzyć role niestandardowe w usłudze Azure API Management"
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
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Sposób tooUse, kontroli dostępu opartej na rolach, w usłudze Azure API Management
Zarządzanie interfejsami API Azure zależy od based kontroli dostępu (RBAC) tooenable precyzyjne zarządzanie dostępem dla usługi interfejsu API zarządzania i jednostek (np. interfejsów API, zasady). W tym artykule przedstawiono omówienie hello ról wbudowanych i niestandardowych w usłudze API Management. Aby uzyskać więcej informacji na temat zarządzania dostępem w portalu Azure hello zobacz [wprowadzenie do zarządzania dostępem w hello portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Wbudowane role
Zarządzanie interfejsami API obecnie zawiera wbudowane role 3 i doda 2 jedną rolę w hello Najbliższa przyszłość. W innych zakresach, łącznie z subskrypcji, grupy zasobów, a poszczególne wystąpienia interfejsu API zarządzania można przypisać tych ról. Na przykład jeśli tooan użytkownika na poziomie grupy zasobów hello przypisano rolę "Azure API Management usługi czytnika" hello, następnie hello użytkownika będzie miał dostęp do odczytu tooall zarządzanie interfejsami API wystąpień wewnątrz hello grupy zasobów. 

Witaj Poniższa tabela zawiera krótkie opisy hello wbudowane role. Można przypisać te role przy użyciu portalu Azure hello lub innych narzędzi, w tym na platformie Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [interfejsu wiersza polecenia](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), i [interfejsu API REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Aby uzyskać szczegółowe informacje o tym, jak tooassign wbudowanych ról, zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rola          | Dostęp do odczytu<sup>[1]</sup> | Dostęp do zapisu<sup>[2]</sup> | Tworzenie usług, usuwanie, skalowanie sieci VPN i Konfiguracja domeny niestandardowej | Dostęp do portalu Publsiher toolegacy | Opis
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API Management usługi współautora | ✓ | ✓ | ✓ | ✓ | Użytkownika nadrzędnego. Ma pełne usługi zarządzania tooAPI dostępu CRUD i jednostek (np. interfejsów API, zasady). Ma dostęp toohello wydawcy starszej wersji portalu. |
| Czytnik usługi zarządzania interfejsu API platformy Azure | ✓ | | || Ma dostęp tylko do odczytu tooAPI zarządzania usługami i jednostek. |
| Operator usługi zarządzania interfejsu API platformy Azure | ✓ | | ✓ | | Można zarządzać usługi API Management, ale nie jednostek.|
| Edytor usługi zarządzania w usłudze Azure interfejsu API<sup>*</sup> | ✓ | ✓ | |  | Można zarządzać zarządzanie interfejsami API jednostek, ale nie usług.|
| Azure API Management Content Manager<sup>*</sup> | ✓ | | | ✓ | Można zarządzać portalu dla deweloperów. Tooservices dostęp tylko do odczytu i jednostek.|

<sup>[1] usługi zarządzania tooAPI dostęp do odczytu i jednostek (np. interfejsów API, zasad)</sup>

<sup>Usługi zarządzania tooAPI [2] do zapisu i jednostek, z wyjątkiem następujących opeartions: 1) wystąpienia tworzenie, usuwanie i skalowanie Konfigurowanie nazwy domeny niestandardowe 3) konfiguracji sieci VPN 2)</sup>

<sup>\*Witaj Edytor usługi roli będą dostępne po możemy migracji wszystkich admin interfejsu użytkownika z hello istniejących wydawcy portalu toohello portalu Azure. Witaj rolę menedżera zawartości będzie dostępna po portalu wydawcy hello został zrefaktoryzowany tooonly zawiera funkcje pokrewne toomanaging hello developer portal.</sup>  


## <a name="custom-roles"></a>Role niestandardowe
Jeśli żadna hello wbudowanych ról nie spełnia określonych potrzeb, role niestandardowe można tworzyć tooprovide bardziej szczegółowe zarządzanie dostępem do usługi API Management jednostek. Na przykład można utworzyć niestandardową rolę, której ma dostęp tylko do odczytu tooan usługi API Management, ale tylko ma interfejsu API tooone dostęp do zapisu. Zobacz szczegółowe informacje o niestandardowych rolach toolearn [role niestandardowe w Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Po utworzeniu niestandardowej roli zabezpieczeń jest łatwiejsze toostart z jedną z wbudowanych ról hello. Edytuj hello atrybuty tooadd hello akcje, NotActions lub AssignableScopes, a następnie zapisz zmiany hello jako nową rolę. Witaj poniższy przykład rozpoczyna się od roli "Czytnika usługi Managment interfejsu API platformy Azure" hello i tworzy niestandardowej roli zabezpieczeń o nazwie "Kalkulator Edytor interfejsu API". Hello niestandardowej roli zabezpieczeń można przypisać tylko tooa interfejsu API w związku z tym spowoduje tylko ma API toothat dostępu. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Obejrzyj film wideo

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o opartej na rolach kontroli dostępu na platformie Azure
  * [Wprowadzenie do zarządzania dostępem w hello portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Role niestandardowe w Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
