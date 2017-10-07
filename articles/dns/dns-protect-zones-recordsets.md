---
title: aaaProtecting strefy DNS i rekordy | Dokumentacja firmy Microsoft
description: "Jak stref DNS tooprotect zestawami rekordów i w systemie Microsoft Azure DNS."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a>Jak tooprotect DNS strefy i rejestruje

Strefy DNS i rekordy są kluczowych zasobów. Usunięcie strefy DNS lub nawet tylko pojedynczego rekordu DNS może spowodować awarię usług całkowitej.  Dlatego ważne jest krytyczne strefy DNS i rekordy są chronione przed nieautoryzowanym lub przypadkowe zmiany.

W tym artykule opisano, w jaki sposób usługi Azure DNS umożliwia tooprotect możesz stref DNS, a rekordy na takie zmiany.  Trwa stosowanie dwie funkcje zaawansowane zabezpieczenia udostępniane przez usługi Azure Resource Manager: [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) i [blokowania zasobów](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach

Azure opartej na rolach kontroli dostępu (RBAC) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure użytkowników, grup i zasobów. Przy użyciu funkcji RBAC, można przyznać dokładnie hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań. Aby uzyskać więcej informacji o sposobie RBAC ułatwia zarządzanie dostępem, zobacz [co to jest kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>roli "Współautor strefę DNS" Hello

roli "Współautor strefę DNS" Hello jest wbudowana dostarczany przez platformę Azure do zarządzania zasobami DNS.  Przypisywanie użytkowników tooa uprawnienia współautora strefy DNS lub grupy umożliwia zasobów DNS toomanage grupy, ale nie zasoby innego typu.

Na przykład załóżmy, że hello grupy zasobów "myzones" zawiera pięć stref dla Contoso Corporation. Udzielającym hello DNS administratora "Współautora strefę DNS" uprawnienia toothat grupy zasobów, umożliwia pełną kontrolę nad tych stref DNS. Ponadto pozwala uniknąć, udzielanie niepotrzebnych uprawnień, na przykład administrator DNS hello nie można utworzyć ani zatrzymać maszyn wirtualnych.

uprawnienia RBAC tooassign najprostszy sposób Hello jest [za pośrednictwem portalu Azure hello](../active-directory/role-based-access-control-configure.md).  Otwarcie bloku hello "kontroli dostępu (IAM)" dla grupy zasobów hello, a następnie kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" hello i wybierz hello wymagane użytkowników lub grup toogrant uprawnienia.

![Poziom grupy zasobów RBAC za pośrednictwem hello portalu Azure](./media/dns-protect-zones-recordsets/rbac1.png)

Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>Poziomu strefy RBAC

Reguły Azure RBAC można subskrypcji zastosowane tooa zasobów grupy lub tooan pojedynczego zasobu. W przypadku hello Azure DNS ten zasób może być poszczególnych stref DNS, lub nawet poszczególnych zestawu rekordów.

Na przykład załóżmy, że grupa zasobów hello "myzones" zawiera hello strefy "contoso.com" i subzone "customers.contoso.com" tworzonych rekordy CNAME dla każdego konta klienta.  toomanage konto używane Hello te rekordy CNAME należy przypisać uprawnienia toocreate rekordy w strefie "customers.contoso.com" hello tylko, nie powinien być toohello dostępu do innych stref.

Uprawnienia na poziomie strefy RBAC można można przyznać za pośrednictwem hello portalu Azure.  Otwarcie bloku "Kontrola dostępu (IAM)" hello strefy hello, a następnie kliknij przycisk "Dodaj", a następnie wybierz roli "Współautor strefę DNS" hello i wybierz hello wymagane użytkowników lub grup toogrant uprawnienia.

![Strefa DNS RBAC poziomu za pomocą hello portalu Azure](./media/dns-protect-zones-recordsets/rbac2.png)

Uprawnienia można również [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>Poziom RBAC zestawu rekordów

Firma Microsoft wykonaj krok dalej. Należy wziąć pod uwagę administratora wiadomości powitania dla Contoso Corporation, który potrzebuje dostępu toohello MX i rekordów TXT na powitania wierzchołku strefy "contoso.com" hello.  Użytkownik nie musi dostęp do tooany innych rekordów MX lub TXT lub rekordy tooany innego typu.  Usługa Azure DNS umożliwia możesz tooassign uprawnień na powitania zestawu rekordów poziomu, tooprecisely hello rekordów, które hello administratora poczty musi mieć dostęp do.  Witaj administratora poczty jest uprawnienie do dokładnie hello kontroli nich i jest toomake innych zmian.

Zestaw rekordów uprawnień na poziomie RBAC można skonfigurować za pośrednictwem portalu Azure za pomocą przycisku użytkowników"hello" w bloku zestawu rekordów hello hello:

![Poziom RBAC za pośrednictwem portalu Azure hello zestawu rekordów](./media/dns-protect-zones-recordsets/rbac3.png)

Zestaw rekordów uprawnień na poziomie RBAC można też [przyznane przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

polecenie równoważne Hello jest również [dostępne za pośrednictwem interfejsu wiersza polecenia Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Role niestandardowe

wbudowane roli "Współautor strefę DNS" Hello umożliwia pełną kontrolę nad zasobów DNS. Jego jest również możliwe toobuild własnego klienta Azure ról, tooprovide nawet precyzyjny system kontroli.

Rozważmy przykład Witaj, w której zostaje utworzony rekord CNAME w hello strefy "customers.contoso.com" dla każdego konta klienta Contoso Corporation ponownie.  toomanage konto używane Hello tych rekordów CNAME może być przyznany tylko rekordy CNAME toomanage uprawnienia.  Jest następnie rekordy toomodify innych typów (np. zmiana rekordów MX) lub wykonywania operacji na poziomie strefy takich jak usuwanie strefy.

Witaj poniższy przykład przedstawia niestandardową definicję roli do zarządzania tylko rekordy CNAME:

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

Hello właściwości akcje definiuje hello następujące uprawnienia dotyczące DNS:

* `Microsoft.Network/dnsZones/CNAME/*`przyznaje pełną kontrolę nad rekordy CNAME
* `Microsoft.Network/dnsZones/read`przyznaje stref DNS tooread uprawnień, ale nie toomodify ich włączenie możesz toosee hello strefy, w których hello jest tworzony CNAME.

pozostałe akcje są kopiowane z hello Hello [wbudowana Rola współautora strefy DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Przy użyciu niestandardowych tooprevent roli RBAC usunięcie rekordu ustawia podczas jednocześnie ich toobe aktualizacji nie jest skutecznej kontroli. Uniemożliwia zestawy rekordów usuwany, ale go nie uniemożliwia ich jest modyfikowany.  Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów hello, łącznie z usunięciem wszystkich rekordów tooleave "empty" zestawu rekordów. To ustawienie hello sam efekt co usunięcie rekordu hello ustawić z punktu widzenia rozpoznawania DNS.

Definicje ról niestandardowych obecnie nie można zdefiniować za pomocą hello portalu Azure. Można utworzyć niestandardową rolę, na podstawie tej definicji roli przy użyciu programu Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Go można również utworzyć za pomocą interfejsu wiersza polecenia Azure hello:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello roli można następnie przypisać w hello sam sposób jak wbudowane role, zgodnie z opisem we wcześniejszej części tego artykułu.

Aby uzyskać więcej informacji na temat sposobu toocreate, zarządzania i przypisz role niestandardowe, zobacz [role niestandardowe w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Blokowania zasobów

W tooRBAC dodanie usługi Azure Resource Manager obsługuje innego rodzaju kontrolę zabezpieczeń, to znaczy hello możliwości too'lock "zasobów. Jeżeli zasady RBAC pozwalają akcje hello toocontrol konkretnych użytkowników i grup, blokowania zasobów są stosowane toohello zasobów i obowiązują we wszystkich użytkowników i ról. Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).

Istnieją dwa typy zasobów blokady: **DoNotDelete** i **tylko do odczytu**. Te mogą być stosowane tooa strefy DNS lub tooan poszczególnych zestawu rekordów.  Witaj poniższych sekcjach opisano kilka typowych scenariuszy i w jaki sposób toosupport ich przy użyciu blokady zasobu.

### <a name="protecting-against-all-changes"></a>Ochrona przed wszystkimi zmianami

tooprevent trwa zmian, zastosuj strefy toohello blokady tylko do odczytu.  Zapobiega to zostanie utworzony i istniejących zestawów rekordów, zmodyfikowane lub usunięte nowych zestawów rekordów.

Blokad zasobów na poziomie strefy można tworzyć za pomocą hello portalu Azure.  W bloku strefy DNS hello, kliknij przycisk "Blokady", następnie "Dodaj":

![Blokad zasobów na poziomie strefy za pośrednictwem hello portalu Azure](./media/dns-protect-zones-recordsets/locks1.png)

Poziomu strefy zasób, którego blokad można również utworzyć za pomocą programu Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Konfigurowanie blokad zasobów platformy Azure nie jest obecnie obsługiwane za pośrednictwem hello wiersza polecenia platformy Azure.

### <a name="protecting-individual-records"></a>Ochrona poszczególne rekordy

tooprevent istniejącego rekordu DNS ustawiona przed zmianami, mają zastosowanie tylko do odczytu zestawu rekordów toohello blokady.

> [!NOTE]
> Stosowanie tooa blokady DoNotDelete zestawu rekordów nie jest skutecznej kontroli. Zapobiega zestawu przed usunięciem rekordów hello, ale go nie uniemożliwia jej jest modyfikowany.  Dozwolone modyfikacje obejmują dodawanie i usuwanie rekordów z zestawu rekordów hello, łącznie z usunięciem wszystkich rekordów tooleave "empty" zestawu rekordów. To ustawienie hello sam efekt co usunięcie rekordu hello ustawić z punktu widzenia rozpoznawania DNS.

Zestaw rekordów zasobów na poziomie blokad można obecnie tylko skonfigurowany przy użyciu programu Azure PowerShell.  Nie są obsługiwane w portalu Azure hello lub wiersza polecenia platformy Azure.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Ochrona przed usunięciem strefy

Po usunięciu strefę w usłudze Azure DNS wszystkich zestawów rekordów w strefie hello również zostaną usunięte.  Tej operacji nie można cofnąć.  Przypadkowego usunięcia strefy krytyczne ma wpływ firma toohave potencjalnych hello.  Dlatego jest bardzo ważne tooprotect przed usunięciem przypadkowemu strefy.

Zastosowanie strefy tooa blokady DoNotDelete zapobiega strefy hello przed usunięciem.  Jednak ponieważ blokady są dziedziczone przez zasoby podrzędne, uniemożliwia także żadnych zestawów rekordów w strefie hello przed usunięciem, który może być niepożądane.  Ponadto zgodnie z opisem w uwagi hello powyżej, jest również żadnego efektu, ponieważ nadal można usunąć rekordy z hello istniejące zestawy rekordów.

Alternatywnie należy rozważyć stosowanie rekord tooa blokady DoNotDelete ustawione w strefie hello, takiego jak zestaw rekordów SOA hello.  Ponieważ nie można usunąć strefy hello bez także usuwanie zestawów rekordów hello, chroni to przed usunięciem strefy, umożliwiając zestawów rekordów w ramach toobe strefy hello zmodyfikowany za darmo. Jeśli strefa hello toodelete podejmowana jest próba, usługi Azure Resource Manager wykryje to spowoduje również usunięcie zestawu rekordów SOA hello i bloki hello wywołania, ponieważ hello SOA jest zablokowany.  Brak zestawów rekordów są usuwane.

Witaj następującego polecenia programu PowerShell tworzy DoNotDelete blokadą rekord SOA hello hello podane strefy:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Innym sposobem jest tooprevent strefy przypadkowego usunięcia za pomocą operatora hello tooensure niestandardowej roli zabezpieczeń i toomanage konta używane usługi nie ma strefy stref usunąć uprawnienia. Gdy potrzebne są toodelete strefy, można wymusić delete dwuetapową, pierwszy udzielającym strefy uprawnienia do usuwania (na zakres hello strefy tooprevent Usuwanie strefy niewłaściwy hello) i drugi toodelete hello strefy.

Tej metody drugi jest korzyść hello, która działa we wszystkich strefach dostępne przez te konta, bez konieczności tooremember toocreate wszystkie blokady. Ma ona wadą hello czy kont z uprawnienia do usuwania strefy, takich jak hello właściciel subskrypcji, nadal przypadkowo można usunąć strefy krytyczne.

Jest to możliwe toouse obu podejść — blokowania zasobów i role niestandardowe — na powitania sam czas, jako ochrony strefy tooDNS podejście obrony zabezpieczeń.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat pracy z RBAC, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).
* Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokowania zasobów z usługi Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

