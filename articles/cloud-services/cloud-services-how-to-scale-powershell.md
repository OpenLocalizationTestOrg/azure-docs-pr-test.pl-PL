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
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="72e60-103">Jak usługa tooscale chmury w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="72e60-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="72e60-104">Tooscale środowiska Windows PowerShell można użyć roli sieci web lub roli proces roboczy przychodzący lub wychodzący przez dodanie lub usunięcie wystąpień.</span><span class="sxs-lookup"><span data-stu-id="72e60-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="72e60-105">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="72e60-105">Log in tooAzure</span></span>

<span data-ttu-id="72e60-106">Przed wykonaniem jakichkolwiek działań na subskrypcję za pomocą programu PowerShell, należy zalogować się:</span><span class="sxs-lookup"><span data-stu-id="72e60-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="72e60-107">Jeśli masz wiele subskrypcji skojarzonych z Twoim kontem, może być konieczne toochange hello bieżącej subskrypcji w zależności od tego, gdzie znajduje się usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="72e60-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="72e60-108">toocheck hello bieżącej subskrypcji, uruchom:</span><span class="sxs-lookup"><span data-stu-id="72e60-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="72e60-109">Jeśli potrzebujesz toochange hello bieżącej subskrypcji, uruchom:</span><span class="sxs-lookup"><span data-stu-id="72e60-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="72e60-110">Sprawdź hello bieżącą liczbę wystąpień dla roli użytkownika</span><span class="sxs-lookup"><span data-stu-id="72e60-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="72e60-111">Uruchom toocheck hello bieżący stan roli użytkownika:</span><span class="sxs-lookup"><span data-stu-id="72e60-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="72e60-112">Powinny zostać wyświetlone informacje o roli hello, włącznie z bieżącej wersji i wystąpienia licznika systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="72e60-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="72e60-113">W takim przypadku hello rola ma jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="72e60-113">In this case, hello role has a single instance.</span></span>

![Informacje o roli hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="72e60-115">Skalowanie w poziomie roli hello, dodając więcej wystąpień</span><span class="sxs-lookup"><span data-stu-id="72e60-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="72e60-116">tooscale wychodzących roli użytkownika, hello przebiegu żądaną liczbę wystąpień jako hello **liczba** toohello parametru **AzureRole zestaw** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="72e60-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="72e60-117">bloki polecenia cmdlet Hello na chwilę podczas hello nowe wystąpienia są udostępniane i uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="72e60-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="72e60-118">W tym czasie możesz otworzyć nowe okno programu PowerShell i wywołanie **Get AzureRole** jak pokazano wcześniej, zobaczysz hello nowego docelowego wystąpienia licznika.</span><span class="sxs-lookup"><span data-stu-id="72e60-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="72e60-119">I jeśli sprawdzić stan roli hello w portalu hello, powinny pojawić się nowe wystąpienie hello uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="72e60-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Począwszy od portalu wystąpienia maszyny Wirtualnej](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="72e60-121">Po rozpoczęciu ma hello nowych wystąpień hello polecenie cmdlet zwraca pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="72e60-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Powodzenie wzrost wystąpienia roli](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="72e60-123">Skalowanie w roli hello przez usunięcie wystąpień</span><span class="sxs-lookup"><span data-stu-id="72e60-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="72e60-124">Możesz skalować w roli przez usunięcie wystąpień w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="72e60-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="72e60-125">Hello zestaw **liczba** parametru na **AzureRole zestaw** toohello liczbę wystąpień ma toohave po zakończeniu hello skali w operacji.</span><span class="sxs-lookup"><span data-stu-id="72e60-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72e60-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72e60-126">Next steps</span></span>

<span data-ttu-id="72e60-127">Nie jest możliwe tooconfigure automatycznego skalowania dla usług w chmurze z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72e60-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="72e60-128">toodo, który zobacz [jak tooauto skalowania usługi w chmurze](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72e60-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
