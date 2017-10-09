---
title: "aaaEstimate pojemności replikacji na platformie Azure | Dokumentacja firmy Microsoft"
description: "Użyj tego artykułu tooestimate pojemności podczas replikowania z usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Planowanie pojemności do ochrony maszyn wirtualnych i serwerów fizycznych w usłudze Azure Site Recovery

Narzędzie Azure Site Recovery Capacity Planner Hello pomaga toofigure się z wymaganiami pojemności replikowanie maszyn wirtualnych funkcji Hyper-V, maszyn wirtualnych VMware oraz serwerach fizycznych systemu Windows i Linux, z usługą Azure Site Recovery.

Witaj tooanalyze planowania pojemności odzyskiwania lokacji przy użyciu środowiska źródłowego i obciążeń, należy oszacować wymagania dotyczące przepustowości i zasobów serwera, które będą potrzebne do lokalizacji źródłowej hello oraz zasoby hello (maszyn wirtualnych i magazynu itp.), które są potrzebne w celu hello Lokalizacja.

Można uruchomić narzędzie hello w kilka metod:

* **Planowanie szybkie**: Uruchom narzędzie hello w tym trybie tooget sieci i serwera prognozy oparte na średnich liczbach maszyn wirtualnych, dysków, magazynu i szybkość zmian.
* **Szczegółowe planowanie**: Uruchom narzędzie hello w tym trybie i podaj szczegóły poszczególnych obciążeń na poziomie maszyny Wirtualnej. Analizowanie zgodności maszyny Wirtualnej i uzyskać projekcje sieci i serwera.

## <a name="before-you-start"></a>Przed rozpoczęciem


1. Zbierz informacje o środowisku, w tym o maszynach wirtualnych, dysków dla maszyny Wirtualnej, magazynu na dysku.
2. Określ częstotliwość codziennych zmian (przenoszenia) dla replikowanych danych. toodo to:

   * Jeśli przeprowadzasz replikację maszyn wirtualnych funkcji Hyper-V, a następnie Pobierz hello [narzędzia do planowania pojemności funkcji Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) szybkość zmian hello tooget. [Dowiedz się więcej](site-recovery-capacity-planning-for-hyper-v-replication.md) o tym narzędziu. Firma Microsoft zaleca się, że możesz uruchomić to narzędzie za pośrednictwem toocapture tygodnia średnie.
   * Jeśli replikujesz maszyny wirtualne VMware, należy użyć hello [Azure lokacji odzyskiwania wdrożenia Planistę](./site-recovery-deployment-planner.md) toofigure limit hello churn — szybkości.
   * W przypadku replikowania serwerów fizycznych, należy najpierw tooestimate ręcznie.

## <a name="run-hello-quick-planner"></a>Uruchom hello szybkiego planowania
1. Pobierz i otwórz hello [usługi Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) narzędzia. Makra toorun, dlatego wybierz tooenable edycji i Włącz muszą się zawartości po wyświetleniu monitu.
2. W **wybierz typ planner** wybierz **szybkie Planner** hello polu listy.

   ![Wprowadzenie](./media/site-recovery-capacity-planner/getting-started.png)
3. W hello **Capacity Planner** arkusza, wprowadź hello wymagane informacje. Należy wypełnić wszystkie pola hello zaznaczona kółkiem na czerwono na poniższym zrzucie ekranu hello.

   * W **wybierz scenariusz**, wybierz **tooAzure funkcji Hyper-V** lub **tooAzure VMware/fizyczne**.
   * W **średnie dzienne zmienić częstotliwość (%)**, umieść w hello informacje należy zebrać, przy użyciu hello [narzędzia do planowania pojemności funkcji Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) lub hello [Azure lokacji odzyskiwania wdrożenia Planistę](./site-recovery-deployment-planner.md).  
   * **Kompresja** dotyczy tylko toocompression oferowane podczas replikowania maszyn wirtualnych VMware lub serwerów fizycznych tooAzure. Firma Microsoft oszacować 30% lub więcej, ale można zmodyfikować ustawienia hello zgodnie z potrzebami. Do replikowania maszyn wirtualnych funkcji Hyper-V tooAzure kompresji, można użyć urządzenia innych firm, takich jak Riverbed.
   * W **przechowywania danych wejściowych**, określ, jak długo mają być przechowywane repliki. Jeśli przeprowadzasz replikację VMware lub serwerów fizycznych, wprowadź wartość hello w dniach. Jeśli przeprowadzasz replikację funkcji Hyper-V, należy określić hello czasu w godzinach.
   * W **liczbę godzin, w których replikacji początkowej dla partii hello maszyn wirtualnych należy wykonać** i **liczbę maszyn wirtualnych na partię replikacji początkowej**, wprowadzania ustawień, które są używane wymagania dotyczące replikacji początkowej toocompute.  Podczas wdrażania usługi Site Recovery należy przesłać cały początkowego zestawu danych hello.

   ![Dane wejściowe](./media/site-recovery-capacity-planner/inputs.png)
4. Po została utworzona, w wartości hello hello środowiska źródłowego, wyświetlane dane wyjściowe obejmują:

   * **Przepustowość wymagana dla replikacji różnicowej** (MB/s). Przepustowość sieci dla replikacja różnicowa jest obliczana na powitania średni dzienny częstotliwości zmian danych.
   * **Przepustowość wymagana w przypadku replikacji początkowej** (MB/s). Przepustowość sieci dla replikacji początkowej jest obliczana na powitania replikacji początkowej wartości, które należy umieścić w.
   * **Magazynu (w GB) wymagany** jest hello Azure pamięci masowej wymagane.
   * **Łączna liczba IOPS na kontach magazynu w warstwie standardowa** jest obliczana na podstawie rozmiaru jednostki IOPS 8 KB na kontach magazynu w warstwie standardowa całkowita hello.  Dla hello szybkie Planner numer hello jest obliczany na podstawie wszystkich hello źródła maszyn wirtualnych dysków i codziennie częstotliwości zmian danych. Dla hello Planner szczegółowe, liczba hello jest obliczoną na podstawie całkowitą liczbę maszyn wirtualnych, które są mapowane toostandard maszynach wirtualnych platformy Azure i danych zmienić częstotliwość na tych maszynach wirtualnych.
   * **Liczba kont magazynu w warstwie standardowa** zapewnia hello łączna liczba tooprotect potrzebnych kont magazynu w warstwie standardowa hello maszyn wirtualnych. Konta standard storage można utrzymanie too20000 IOPS we wszystkich hello maszyn wirtualnych w magazynie standardowe i obsługiwane są maksymalnie 500 iops dla każdego dysku.
   * **Liczba obiektów blob dysków wymaganych** zapewnia hello liczba dysków, które zostaną utworzone w magazynie Azure.
   * **Liczba kont magazynu premium wymagane** zapewnia hello łączna liczba tooprotect wymagane konta magazynu premium hello maszyn wirtualnych. Źródło maszyny Wirtualnej o wysokiej IOPS (większe niż 20000) musi mieć konto magazynu w warstwie premium. Konto magazynu premium mogą przechowywać się too80000 IOPS.
   * **Łączna liczba IOPS na magazyn w warstwie premium** jest obliczana na podstawie rozmiaru jednostki IOPS 256 KB na kontach magazynu premium całkowita hello.  Dla hello szybkie Planner numer hello jest obliczany na podstawie wszystkich hello źródła maszyn wirtualnych dysków i codziennie częstotliwości zmian danych. Dla hello Planner szczegółowe, liczba hello jest obliczony na podstawie hello całkowitą liczbę maszyn wirtualnych, które są mapowane toopremium maszyny Wirtualnej platformy Azure (seria DS i GS) i danych hello zmienić częstotliwość na tych maszynach wirtualnych.
   * **Liczba serwerów konfiguracji wymaganych** pokazuje, ile serwerów konfiguracji są wymagane do wdrożenia hello.
   * **Liczby wymaganych serwerów dodatkowych procesów** pokazuje, czy są wymagane w dodanie toohello proces serwera, który jest uruchomiony na serwerze konfiguracji hello domyślnie serwery dodatkowych procesów.
   * **dodatkowy magazyn 100% w źródle hello** pokazuje, czy w lokalizacji źródłowej hello jest wymagany dodatkowy magazyn.

   ![Dane wyjściowe](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Uruchom hello szczegółowe planowania

1. Pobierz i otwórz hello [usługi Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) narzędzia. Makra toorun, dlatego wybierz tooenable edycji i Włącz muszą się zawartości po wyświetleniu monitu.
2. W **wybierz typ planner**, wybierz pozycję **szczegółowe Planner** hello polu listy.

   ![Wprowadzenie](./media/site-recovery-capacity-planner/getting-started-2.png)
3. W hello **kwalifikacji obciążenia** arkusza, wprowadź hello wymagane informacje. Należy podać wszystkie hello oznaczone jako pola.

   * W **rdzenie procesora**, określ hello łączna liczba rdzeni na serwerze źródłowym.
   * W **alokacji pamięci w Megabajtach**, określ rozmiar pamięci RAM powitania serwera źródłowego.
   * Witaj **liczbę kart sieciowych**, określ hello liczbę kart sieciowych na serwerze źródłowym.
   * W **całkowity magazynu (w GB)**, określ rozmiar całkowitą hello hello magazynu maszyny Wirtualnej. Na przykład jeśli serwer źródłowy hello ma 3 dysk 500 GB, całkowitego rozmiaru magazynu jest 1500 GB.
   * W **liczba dysków dołączonych**, określ hello całkowitej liczby dysków z serwera źródłowego.
   * W **wykorzystanie pojemności dysku**, określ hello średnie wykorzystanie.
   * W **codziennie zmienić częstotliwość (%)**, określ hello codzienne dane zmienić częstotliwość, z serwera źródłowego.
   * W **mapowania Azure rozmiar**, wprowadź hello rozmiar maszyny Wirtualnej platformy Azure, które mają toomap. Jeśli nie chcesz tego ręcznie toodo, kliknij przycisk **obliczeniowe maszyn wirtualnych IaaS**. Jeśli wprowadź ustawienia ręcznie, a następnie kliknij obliczeniowe maszyn wirtualnych IaaS, ponieważ proces obliczeń hello automatycznie rozpoznaje hello najlepszego dopasowania rozmiaru maszyny Wirtualnej platformy Azure mogą być zastępowane hello ręczne ustawienie.

   ![Kwalifikacja obciążenia](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Jeśli klikniesz przycisk **obliczeniowe maszyn wirtualnych IaaS** Oto, czego:

   * Sprawdza poprawność danych wejściowych obowiązkowe hello.
   * Oblicza wartość IOPS, a także sugeruje hello dopasowanie dla poszczególnych maszyn wirtualnych, które kwalifikują się do replikacji tooAzure aize najlepsze maszyny Wirtualnej platformy Azure. Jeśli nie można wykryć odpowiedni rozmiar maszyny Wirtualnej platformy Azure, że wygenerowany błąd. Na przykład jeśli hello liczba dysków dołączonych w 65, zgłaszany jest błąd ponieważ hello najwyższy rozmiar maszyny Wirtualnej platformy Azure jest 64.
   * Sugeruje konta magazynu, który może służyć do maszyny Wirtualnej platformy Azure.
   * Oblicza hello całkowitą liczbę kont magazynu w warstwie standardowa i premium kont magazynu wymagana dla obciążenia hello. Przewiń w dół hello tooview typ magazynu Azure i hello konta magazynu, który może służyć do serwera źródłowego.
   * Kończy i sortuje hello reszty tabeli hello na podstawie typu wymagane magazynu (standardowy lub premium) przypisany do maszyny Wirtualnej, a hello dołączona liczba dysków. Dla wszystkich maszyn wirtualnych, które spełniają wymagania hello Azure hello kolumny **jest wirtualna kwalifikowana?** pokazuje **tak**. Jeśli maszyny Wirtualnej nie można utworzyć kopii zapasowej tooAzure, zostanie wyświetlony błąd.

TooAE AA kolumn są dane wyjściowe i podaj informacje dotyczące każdej maszyny Wirtualnej.

![Kwalifikacja obciążenia](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Przykład
Na przykład sześć maszyn wirtualnych z wartościami hello tabelą hello narzędzia hello obliczana i przypisuje hello najlepsze dopasowanie maszyny Wirtualnej platformy Azure i wymagania dotyczące magazynu Azure hello.

![Kwalifikacja obciążenia](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Zanotuj następujące hello hello przykładowe dane wyjściowe:

  * Hello pierwsza kolumna jest kolumną weryfikacji hello maszyn wirtualnych, dysków i ilość danych churn.
  * Dwa konta magazynu w warstwie standardowa i premium jednego konta magazynu są potrzebne do pięciu maszynach wirtualnych.
  * VM3 nie kwalifikuje się do ochrony, ponieważ co najmniej jeden dysk jest więcej niż 1 TB.
  * VM1 i maszyny VM2 mogą używać hello pierwsze konto magazynu w warstwie standardowa
  * VM4 można użyć hello drugiego konta magazynu w warstwie standardowa.
  * VM5 i VM6 wymagane jest konto magazynu premium i można jednocześnie używać jednego konta.

    > [!NOTE]
    > IOPS na warstwy standardowa i premium magazynu są obliczane na powitania poziom maszyny Wirtualnej, a nie na poziomie dysku. Standardowa maszyna wirtualna może obsługiwać się too500 IOPS dla każdego dysku. Wartość IOPS dla dysku jest większa niż 500, należy najpierw Magazyn w warstwie premium. Jednak jeśli IOPS dla dysku jest więcej niż 500, ale IOPS dla hello całkowita dysków maszyny Wirtualnej są w hello obsługuje standardowe limity maszyny Wirtualnej platformy Azure (rozmiar maszyny Wirtualnej, liczbę dysków, liczba kart, Procesora, pamięci), planowania hello wybiera standardowe maszyny Wirtualnej i nie hello DS lub GS serii. Należy toomanually aktualizacji hello mapowania komórki rozmiaru platformy Azure z odpowiednią serii DS lub GS maszyny Wirtualnej.


Po wszystkich szczegółów hello znajdują się w miejscu, kliknij przycisk **przesyłania danych toohello planisty** tooopen hello **Capacity Planner** obciążeń są wyróżnione tooshow czy są one kwalifikuje się do ochrony, czy nie.

### <a name="submit-data-in-hello-capacity-planner"></a>Przesyłanie danych w hello planowania pojemności
1. Po otwarciu hello **Capacity Planner** arkusza zostanie wprowadzony na podstawie hello ustawień wybranymi przez użytkownika. Witaj word "Obciążenie" pojawia się w hello **źródła danych wejściowych Infra** komórki, tooshow, który hello danych wejściowych jest hello **kwalifikacji obciążenia** arkusza.
2. Jeśli chcesz toomake zmiany, należy toomodify hello **kwalifikacji obciążenia** arkuszu, a następnie kliknij przycisk **przesyłania danych toohello planisty** ponownie.  

   ![Narzędzie do planowania pojemności](./media/site-recovery-capacity-planner/capacity-planner.png)
