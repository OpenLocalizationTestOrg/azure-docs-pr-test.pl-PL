---
title: "zalecenia dotyczące wysokiej dostępności usługi Advisor aaaAzure | Dokumentacja firmy Microsoft"
description: "Użyj doradcy Azure tooimprove wysokiej dostępności Azure wdrożeń."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Zalecenia doradcy w zakresie wysokiej dostępności

Azure Advisor pomaga zapewnić i zapewnić ciągłość hello aplikacji biznesowych o znaczeniu krytycznym. Można uzyskać wysoką dostępność zalecenia usługi Advisor hello **wysokiej dostępności** karta pulpitu nawigacyjnego usługi Advisor hello.

![Wysoka dostępność przycisk na pulpicie nawigacyjnym usługi Advisor hello](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Zapewnić odporność na uszkodzenia maszyny wirtualnej

Klasyfikator identyfikuje maszyn wirtualnych, które nie są częścią zestawu dostępności i zaleca przenoszenia ich do zestawu dostępności. Aby zapewnić nadmiarowość tooyour aplikacji, zalecamy grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności. Ta konfiguracja temu podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jednej maszyny wirtualnej jest dostępna i spełnia hello maszyny wirtualnej platformy Azure umowy dotyczącej poziomu usług. Można albo toocreate zbiór dostępności dla hello maszyny wirtualnej lub tooadd hello maszyny wirtualnej tooan istniejącego zestawu dostępności.

> [!NOTE]
> Jeśli wybierzesz toocreate dostępności, musisz dodać co najmniej jednej maszyny wirtualnej więcej do niego. Firma Microsoft zaleca, że grupa dwa lub więcej maszyn wirtualnych w dostępności ustawić tooensure co najmniej jedna maszyna jest dostępna podczas wystąpienia awarii.

![Zalecenia usługi Advisor: nadmiarowości maszyny wirtualnej, użyj zestawów dostępności](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Upewnij się, że odporność na uszkodzenia zestawu dostępności 

Klasyfikator identyfikuje zestawów dostępności, które zawierają jednej maszyny wirtualnej i zaleca się dodawania jednego lub więcej tooit maszyn wirtualnych. Aby zapewnić nadmiarowość tooyour aplikacji, zalecamy grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności. Ta konfiguracja temu podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jednej maszyny wirtualnej jest dostępna i spełnia hello maszyny wirtualnej platformy Azure umowy dotyczącej poziomu usług. Można wybrać obu toocreate maszyny wirtualnej lub toouse istniejącej maszyny wirtualnej i tooadd go toohello zestawu dostępności.  

![Zalecenia usługi Advisor: Dodaj co najmniej jeden zestaw dostępności toothis maszyny wirtualne](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Zapewnić odporność na uszkodzenia bramy aplikacji
tooensure hello ciągłość prowadzenia działalności biznesowej kluczowych aplikacji, które są obsługiwane przez usługę bramy aplikacji, usługi Advisor identyfikuje wystąpień bramy aplikacji, które nie są skonfigurowane na uszkodzenia, i sugeruje akcji korygowania, które można wykonać . Średnich i dużych pojedyncze wystąpienie aplikacji bramy identyfikuje Advisor i zaleca się dodawania co najmniej jedno wystąpienie więcej. Również instance jednego lub kilku aplikacji małych bramy identyfikuje i zaleca Migrowanie toomedium lub duże jednostki SKU. Klasyfikator zaleca tooensure te akcje, czy swoich wystąpień bramy aplikacji są skonfigurowane toosatisfy hello bieżącego wymaganiami SLA dla tych zasobów.

![Zalecenia usługi Advisor: Wdrażanie dwóch lub więcej wystąpień bramy średnich i dużych aplikacji o określonym rozmiarze](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Zwiększyć hello wydajność i niezawodność dysków maszyny wirtualnej

Klasyfikator identyfikuje maszyn wirtualnych przy użyciu standardowych dysków i zaleca toopremium dysków.
 
Usługa Azure Premium Storage oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach maszyn wirtualnych uruchomionych obciążeń/O wykonujących. Dyski maszyn wirtualnych, które używają konta premium magazynu przechowywania danych na dyskach półprzewodnikowych (SSD). Hello najlepszą wydajność aplikacji zaleca się, że zostaną zmigrowane wszystkie dyski maszyny wirtualnej wymagające wysokiej magazynu toopremium IOPS. 

Jeśli dyski nie wymagają wysokiej IOPS, można ograniczyć koszty, przechowując ich magazynu w warstwie standardowa. Standardowe magazynu przechowuje dane dysku maszyny wirtualnej na stacje dysków twardych (HDD) zamiast dysków SSD. Możesz wybrać toomigrate dysków toopremium dysków maszyny wirtualnej. Dyski w warstwie Premium są obsługiwane w większości maszyny wirtualnej jednostki SKU. Jednak w niektórych przypadkach, jeśli chcesz, aby dyski premium toouse, konieczne może tooupgrade maszyny wirtualnej jednostki SKU również.

![Zalecenia usługi Advisor: zwiększyć niezawodność hello dyski maszyny wirtualnej przez uaktualnienie toopremium dysków](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Ochrona danych maszyny wirtualnej przed przypadkowym usunięciem
Klasyfikator identyfikuje maszyny wirtualne, których kopia zapasowa nie jest włączona i zaleca się włączenie kopii zapasowej. Konfigurowanie kopii zapasowej maszyny wirtualnej zapewnia hello dostępność danych biznesowych o znaczeniu krytycznym i zapewnia ochronę przed przypadkowym usunięciem lub uszkodzenia.

![Zalecenia usługi Advisor: Skonfiguruj kluczowych danych tooprotect kopii zapasowej maszyny wirtualnej](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Zalecenia dotyczące wysokiej dostępności dostępu klasyfikatora

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W okienku po lewej stronie powitania kliknij **więcej usług**.

3. W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.  
 pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.

4. Na pulpicie nawigacyjnym usługi Advisor hello, kliknij przycisk hello **wysokiej dostępności** , a następnie wybierz hello subskrypcji, dla której ma zostać tooreceive zalecenia.

> [!NOTE]
> tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor. Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku. Jest to *jednorazowa operacja*. Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących zalecenia doradcy w zakresie zobacz:
* [Wprowadzenie tooAzure Advisor](advisor-overview.md)
* [Wprowadzenie do usługi Advisor](advisor-get-started.md)
* [Zalecenia doradcy w zakresie koszt](advisor-performance-recommendations.md)
* [Zalecenia doradcy w zakresie wydajności](advisor-performance-recommendations.md)
* [Zalecenia doradcy w zakresie zabezpieczeń](advisor-security-recommendations.md)

