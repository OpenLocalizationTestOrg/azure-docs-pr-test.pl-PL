---
title: "usługi w chmurze platformy Azure w programie Windows PowerShell aaaScale | Dokumentacja firmy Microsoft"
description: "(klasyczne) Dowiedz się, jak toouse PowerShell tooscale roli sieci web lub roli proces roboczy lub pomniejszyć na platformie Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Jak usługa tooscale chmury w programie PowerShell

Tooscale środowiska Windows PowerShell można użyć roli sieci web lub roli proces roboczy przychodzący lub wychodzący przez dodanie lub usunięcie wystąpień.  

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Przed wykonaniem jakichkolwiek działań na subskrypcję za pomocą programu PowerShell, należy zalogować się:

```powershell
Add-AzureAccount
```

Jeśli masz wiele subskrypcji skojarzonych z Twoim kontem, może być konieczne toochange hello bieżącej subskrypcji w zależności od tego, gdzie znajduje się usługa w chmurze. toocheck hello bieżącej subskrypcji, uruchom:

```powershell
Get-AzureSubscription -Current
```

Jeśli potrzebujesz toochange hello bieżącej subskrypcji, uruchom:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Sprawdź hello bieżącą liczbę wystąpień dla roli użytkownika

Uruchom toocheck hello bieżący stan roli użytkownika:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Powinny zostać wyświetlone informacje o roli hello, włącznie z bieżącej wersji i wystąpienia licznika systemu operacyjnego. W takim przypadku hello rola ma jedno wystąpienie.

![Informacje o roli hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Skalowanie w poziomie roli hello, dodając więcej wystąpień

tooscale wychodzących roli użytkownika, hello przebiegu żądaną liczbę wystąpień jako hello **liczba** toohello parametru **AzureRole zestaw** polecenia cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

bloki polecenia cmdlet Hello na chwilę podczas hello nowe wystąpienia są udostępniane i uruchomiony. W tym czasie możesz otworzyć nowe okno programu PowerShell i wywołanie **Get AzureRole** jak pokazano wcześniej, zobaczysz hello nowego docelowego wystąpienia licznika. I jeśli sprawdzić stan roli hello w portalu hello, powinny pojawić się nowe wystąpienie hello uruchamiania:

![Począwszy od portalu wystąpienia maszyny Wirtualnej](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Po rozpoczęciu ma hello nowych wystąpień hello polecenie cmdlet zwraca pomyślnie:

![Powodzenie wzrost wystąpienia roli](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Skalowanie w roli hello przez usunięcie wystąpień

Możesz skalować w roli przez usunięcie wystąpień w hello tak samo. Hello zestaw **liczba** parametru na **AzureRole zestaw** toohello liczbę wystąpień ma toohave po zakończeniu hello skali w operacji.

## <a name="next-steps"></a>Następne kroki

Nie jest możliwe tooconfigure automatycznego skalowania dla usług w chmurze z programu PowerShell. toodo, który zobacz [jak tooauto skalowania usługi w chmurze](cloud-services-how-to-scale-portal.md).
