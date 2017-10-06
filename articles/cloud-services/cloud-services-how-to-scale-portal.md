---
title: "aaaAuto skalowania usługi w chmurze w portalu hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello reguł skalowania automatycznego tooconfigure portalu dla roli sieci web usługi w chmurze lub roli proces roboczy na platformie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>W jaki sposób tooconfigure automatyczne skalowanie usługi w chmurze w portalu hello
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-scale-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-scale.md)

Warunki można ustawić dla roli proces roboczy usługi chmury, wyzwalające skali przychodzący lub wychodzący operacji. warunki Hello hello roli może być oparta na powitania Procesora, dysku lub obciążenia sieciowego hello roli. Można również ustawić warunek w oparciu metryki komunikat kolejki lub hello z innego zasobu platformy Azure skojarzonych z Twoją subskrypcją.

> [!NOTE]
> Ten artykuł dotyczy usługi w chmurze role sieci web i proces roboczy. Po utworzeniu maszyny wirtualnej (klasyczne) bezpośrednio, znajduje się w usłudze w chmurze. Standardowa maszyny wirtualnej można skalować przez skojarzenie jej z [zestawu dostępności](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) i ręcznie włączyć je lub wyłączyć.

## <a name="considerations"></a>Zagadnienia do rozważenia
Należy rozważyć następujące informacje, przed skonfigurowaniem skalowanie aplikacji hello:

* Skalowanie jest zagrożony użycia rdzeni.

    Większe wystąpień roli za pomocą większej liczby rdzeni. Można skalować aplikacji tylko przed upływem limitu hello rdzeni dla Twojej subskrypcji. Na przykład załóżmy, że w subskrypcji ma limit liczby rdzeni (20). Po uruchomieniu aplikacji z dwie średnich chmury usługi (łącznie 4 rdzenie) można tylko zwiększać innych wdrożeń usługi w chmurze w ramach subskrypcji przez hello pozostałe 16 rdzeni. Aby uzyskać więcej informacji na temat rozmiarów, zobacz [rozmiary usługi w chmurze](cloud-services-sizes-specs.md).

* Możesz skalować oparte na próg komunikat kolejki. Aby uzyskać więcej informacji o tym, jak kolejki toouse, zobacz [jak toouse hello usługi magazynu kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Można również skalować innych zasobów skojarzonych z Twoją subskrypcją.

* tooenable wysoką dostępność aplikacji, należy upewnić się, że jest wdrażany z dwóch lub więcej wystąpień roli. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Gdzie znajduje się skali
Po wybraniu usługi w chmurze powinny być widoczne bloku usługi chmury hello.

1. W bloku usługi chmury hello, na powitania **ról i wystąpień** kafelka, wybierz hello nazwę hello usługi w chmurze.   
   **WAŻNE**: Upewnij się, że chmura hello tooclick usługi roli, nie hello wystąpienia roli, który znajduje się poniżej roli hello.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Wybierz hello **skali** kafelka.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Automatyczne skalowanie
Można skonfigurować ustawienia skalowania dla roli, albo w dwóch trybach **ręczne** lub **automatyczne**. Ręczne zgodnie z regułami, ustaw hello bezwzględną liczbę wystąpień. Automatyczne umożliwia jednak tooset, które powinny być skalowane reguły, które kontrolują sposób oraz jak dużo można.

Zestaw hello **skalowanie przez** opcję zbyt**reguły wydajności i harmonogram**.

![Ustawienia skalowania usługi chmury z profilu i reguł](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Istniejący profil.
2. Dodaj regułę hello nadrzędnego profilu.
3. Dodaj inny profil.

Wybierz **Dodaj profil**. Hello profil określa tryb, który ma być toouse skali hello: **zawsze**, **cyklu**, **Stała data**.

Po skonfigurowaniu profilu hello i reguły wybierz hello **zapisać** ikona u góry hello.

#### <a name="profile"></a>Profil
profilu Hello Ustawia minimalną i maksymalna liczba wystąpień dla hello skalowania, a także, gdy jest aktywny tego zakresu skali.

* **Zawsze**

    Zawsze Zachowuj ten zakres dostępnych wystąpień.  

    ![Usługi w chmurze, która zawsze skalowania](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Cyklu**

    Wybierz zestaw dni hello tooscale tygodnia.

    ![Skali usługi chmury, za pomocą harmonogramu cyklu](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Daty stałej**

    Rola hello tooscale zakres daty stałej.

    ![Skali usługi chmury z datą stałej](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Po skonfigurowaniu profilu hello wybierz hello **OK** u dołu hello hello blok profilu.

#### <a name="rule"></a>Reguła
Reguły są dodawane tooa profilu i stanowią warunek wyzwalający hello skali.

wyzwalacz reguły Hello jest oparta na metryki usługi w chmurze hello (użycie procesora CPU, aktywności dysku lub działanie sieci) toowhich można dodać wartość warunkowego. Ponadto można mieć wyzwalacza hello w oparciu metryki komunikat kolejki lub hello z innego zasobu platformy Azure skojarzonych z Twoją subskrypcją.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Po skonfigurowaniu reguły hello wybierz hello **OK** przycisk u dołu hello hello reguły bloku.

## <a name="back-toomanual-scale"></a>Utwórz kopię toomanual skali
Przejdź toohello [ustawień skalowania](#where-scale-is-located) i zestaw hello **skalowanie przez** opcję zbyt**liczba wystąpień ustawiana ręcznie**.

![Ustawienia skalowania usługi chmury z profilu i reguł](./media/cloud-services-how-to-scale-portal/manual-basics.png)

To ustawienie powoduje usunięcie automatyczne skalowanie z roli hello i, można ustawić liczbę wystąpień hello bezpośrednio.

1. Witaj opcji skalowania (ręczne lub automatyczne).
2. Rola wystąpienia suwaka tooset hello wystąpień tooscale do.
3. Wystąpienia hello tooscale roli do.

Po skonfigurowaniu ustawień skalowania hello wybierz hello **zapisać** ikona u góry hello.
