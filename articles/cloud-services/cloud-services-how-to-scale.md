---
title: "aaaAuto skalowania usługi w chmurze w portalu klasycznym hello | Dokumentacja firmy Microsoft"
description: "(klasyczne) Dowiedz się, jak toouse hello reguł skalowania automatycznego klasycznego portalu tooconfigure dla roli sieci web usługi w chmurze lub roli proces roboczy na platformie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>W jaki sposób tooconfigure automatyczne skalowanie usługi w chmurze w portalu klasycznym hello
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-scale-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-scale.md)

Na stronie skali hello hello klasycznego portalu Azure można skonfigurować ustawienia skalowania automatycznego dla roli sieci web lub roli proces roboczy. Alternatywnie można skonfigurować, ręczne skalowanie zamiast opartych na regułach Skalowanie automatyczne.

> [!NOTE]
> Ten artykuł dotyczy usługi w chmurze role sieci web i proces roboczy. Po utworzeniu maszyny wirtualnej (klasyczne) bezpośrednio, znajduje się w usłudze w chmurze. Niektóre z tych informacji jest stosowana toothese typy maszyn wirtualnych. Skalowanie zestawu dostępności maszyn wirtualnych jest po prostu wyłączając je włączane i wyłączane na podstawie hello skali reguł, które można skonfigurować. Aby uzyskać więcej informacji o maszynach wirtualnych i zestawów dostępności, zobacz [hello Zarządzaj dostępność maszyn wirtualnych](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Należy rozważyć następujące informacje, przed skonfigurowaniem skalowanie aplikacji hello:

* Skalowanie jest zagrożony użycia rdzeni.

    Większe wystąpień roli za pomocą większej liczby rdzeni. Można skalować aplikacji tylko przed upływem limitu hello rdzeni dla Twojej subskrypcji. Na przykład załóżmy, że w subskrypcji ma limit liczby rdzeni (20). Po uruchomieniu aplikacji z dwie średnich chmury usługi (łącznie 4 rdzenie) można tylko zwiększać innych wdrożeń usługi w chmurze w ramach subskrypcji przez hello pozostałe 16 rdzeni. Aby uzyskać więcej informacji na temat rozmiarów, zobacz [rozmiary usługi w chmurze](cloud-services-sizes-specs.md).

* Należy utworzyć kolejkę i skojarzyć go z roli, zanim można skalować aplikacji opartej na próg komunikatu. Aby uzyskać więcej informacji, zobacz [jak toouse hello usługi magazynu kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Zasoby, które są połączone tooyour można skalować usługi w chmurze. Aby uzyskać więcej informacji o łączeniu zasobów, zobacz [porady: łączenie usługi w chmurze tooa zasobów](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable wysoką dostępność aplikacji, należy upewnić się, że jest wdrażany z dwóch lub więcej wystąpień roli. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Skalowanie harmonogramu
Domyślnie wszystkie role nie postępuj zgodnie z określonym harmonogramem. W związku z tym wszystkie ustawienia zmienić się razy tooall oraz wszystkie dni w roku hello. Jeśli chcesz, możesz skonfigurować ręczne lub automatyczne skalowanie dla jednego z następujących trybów hello:

* Dni tygodnia
* Weekendy
* Nocy tygodnia
* Mornings tygodnia
* Konkretne daty
* Zakresy określonej daty

Witaj ustawienia harmonogramu jest skonfigurowany w hello [klasycznego portalu Azure](https://manage.windowsazure.com/) na powitania  
**Usługi w chmurze** > **\[usługi w chmurze\]** > **skali** > **\[środowisko produkcyjne lub tymczasowe\]**  strony.

Kliknij przycisk hello **Konfigurowanie uruchomień** przycisk dla każdej roli ma toochange.

![Automatyczne skalowanie usługi chmury zgodnie z harmonogramem][scale_schedules]

## <a name="manual-scale"></a>Ręczne skali
Na powitania **skali** strony, można ręcznie zwiększyć lub zmniejszyć liczbę hello uruchomionych wystąpień w usłudze w chmurze. To ustawienie jest skonfigurowane dla każdego harmonogram, który został utworzony lub tooall czasu, jeśli nie utworzono harmonogramu.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.
   
   > [!TIP]
   > Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.

2. Kliknij przycisk **skali**.
3. Wybierz harmonogram hello ma toochange opcje do skalowania. *Nie określonych godzinach* jest hello domyślną, jeśli masz Brak zdefiniowanych harmonogramów.
4. Znajdź hello **skali według metryki** a następnie wybierz opcję **Brak**. To ustawienie jest hello domyślnego dla wszystkich ról.
5. Każda rola hello w usłudze w chmurze ma suwak do zmiany numer hello toouse wystąpień.
   
    ![Ręcznie skalować roli usługi chmury][manual_scale]
   
    Jeśli potrzebujesz więcej wystąpień, może być konieczne toochange hello [rozmiar maszyny wirtualnej usługi w chmurze](cloud-services-sizes-specs.md).
6. Kliknij pozycję **Zapisz**.  
   Wystąpienia roli są dodawane lub usuwane w oparciu o wybrane opcje.

> [!TIP]
> Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.

## <a name="automatic-scale---cpu"></a>Automatyczne skalowanie - Procesora
W tym trybie skaluje Jeśli hello średnią wartość procentową wykorzystania Procesora powyżej lub poniżej określonej wartości progowe. Wystąpienia roli są tworzone lub usuwane w takim przypadku.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.
   
   > [!TIP]
   > Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.

2. Kliknij przycisk **skali**.
3. Wybierz harmonogram hello ma toochange opcje do skalowania. *Nie określonych godzinach* jest hello domyślną, jeśli masz Brak zdefiniowanych harmonogramów.
4. Znajdź hello **skali według metryki** a następnie wybierz opcję **Procesora**.
5. Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, użycia Procesora docelowy hello (tootrigger a skalowania w górę) oraz liczbę wystąpień tooscale górę i w dół przez.

![Skalowanie roli usługi chmury, obciążenie procesora cpu][cpu_scale]

> [!TIP]
> Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.

## <a name="automatic-scale---queue"></a>Automatyczne skalowanie - kolejki
Ten tryb jest automatycznie skalowany Jeśli hello liczbę wiadomości w kolejce powyżej lub poniżej określonego progu. Wystąpienia roli są tworzone lub usuwane w takim przypadku.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.
   
   > [!TIP]
   > Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.

2. Kliknij przycisk **skali**.
3. Znajdź hello **skali według metryki** a następnie wybierz opcję **kolejki**.
4. Teraz można skonfigurować minimalną i maksymalną zakresu wystąpień ról, kolejka hello i liczba kolejki wiadomości tooprocess dla każdego wystąpienia i ile tooscale wystąpień w górę i w dół przez.

![Skalowanie roli usługi chmury, kolejki komunikatów][queue_scale]

> [!TIP]
> Zawsze, gdy zostanie wyświetlony ![][tip_icon] Przenieś tooit Twojego myszy i można uzyskać pomoc dotyczącą ustawienie określone.

## <a name="scale-linked-resources"></a>Skalowanie połączonych zasobów
Często skalowanie roli jest bazy danych hello tooscale korzystne, która aplikacja hello używa również. Jeśli link hello usługi w chmurze toohello bazy danych, możesz uzyskać dostęp hello skalowanie ustawień dla tego zasobu, klikając odpowiednie łącze hello.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello chmury usługi.
   
   > [!TIP]
   > Jeśli nie widzisz usługi w chmurze, może być konieczne toochange z **produkcji** za**przemieszczania** lub na odwrót.

2. Kliknij przycisk **skali**.
3. Znajdź hello **połączone zasobów** sekcji, a następnie kliknij przycisk **Zarządzaj skalowania dla tej bazy danych**.
   
   > [!NOTE]
   > Jeśli nie widzisz **połączone zasobów** sekcji, prawdopodobnie nie masz żadnych połączonych zasobów.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
