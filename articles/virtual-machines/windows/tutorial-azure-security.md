---
title: "aaaAzure Centrum zabezpieczeń i systemu Windows maszyny wirtualne na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zabezpieczeń dla maszyny wirtualnej systemu Windows Azure z Centrum zabezpieczeń Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Monitorowanie zabezpieczeń maszyny wirtualnej przy użyciu Centrum zabezpieczeń Azure

Centrum zabezpieczeń Azure ułatwia wgląd we Azure zasobu rozwiązania w zakresie zabezpieczeń. Centrum zabezpieczeń zapewnia zintegrowane zabezpieczenia monitorowania. Można wykryć zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone. Z tego samouczka, dowiesz się o Centrum zabezpieczeń Azure i jak:
 
> [!div class="checklist"]
> * Konfigurowanie zbierania danych
> * Ustawianie zasad zabezpieczeń
> * Wyświetl i rozwiąż problemy z konfiguracją kondycji
> * Przejrzyj wykrytych zagrożeń  

## <a name="security-center-overview"></a>Omówienie Centrum zabezpieczeń

Centrum zabezpieczeń identyfikuje potencjalne problemy z konfiguracją maszyny wirtualnej (VM), a Ustawianie zagrożenia bezpieczeństwa. Mogą one obejmować maszyn wirtualnych, których brakuje grup zabezpieczeń sieci niezaszyfrowane dyski i atakami siłowymi protokołu RDP (Remote Desktop). Witaj informacje są wyświetlane na pulpicie nawigacyjnym Centrum zabezpieczeń hello na wykresach łatwe do odczytania.

pulpit nawigacyjny Centrum zabezpieczeń w hello portalu Azure, w menu hello, wybierz hello tooaccess **Centrum zabezpieczeń**. Na pulpicie nawigacyjnym hello można wyświetlić hello kondycji zabezpieczeń środowiska Azure, Znajdź liczbę zalecanych rozwiązań i wyświetlić bieżący stan hello alertów zagrożeń. Każdy toosee wysokiego poziomu wykresu można rozwinąć więcej szczegółów.

![Pulpit nawigacyjny Centrum zabezpieczeń](./media/tutorial-azure-security/asc-dash.png)

Centrum zabezpieczeń wykracza poza danych odnajdywania tooprovide zalecenia dotyczące problemów, które wykryje. Na przykład jeśli maszyna wirtualna została wdrożona bez dołączonego sieciowej grupy zabezpieczeń, Centrum zabezpieczeń wyświetla zalecenia, korygowania prostych kroków, które można wykonać. Otrzymasz automatycznego korygowania bez opuszczania kontekstu hello Centrum zabezpieczeń.  

![Zalecenia](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Konfigurowanie zbierania danych

Zanim będzie mógł pobrać widoczność w konfiguracjach zabezpieczeń maszyny Wirtualnej, należy tooset się zbieranie danych Centrum zabezpieczeń. Obejmuje to włączenie funkcji zbierania danych i tworzenie toohold zbierane dane konta magazynu platformy Azure. 

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję. 
2. Aby uzyskać **zbierania danych**, wybierz pozycję **na**.
3. Wybierz konto magazynu toocreate **wybierz konto magazynu**. Następnie wybierz opcję **OK**.
4. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**. 

agenta zbierania danych Centrum zabezpieczeń Hello jest instalowany na wszystkich maszynach wirtualnych, a rozpoczęciem zbierania danych. 

## <a name="set-up-a-security-policy"></a>Skonfiguruj zasady zabezpieczeń

Zasady zabezpieczeń są toodefine używane hello elementy, dla których Centrum zabezpieczeń służy do zbierania danych i podano zalecenia. Można zastosować zasady zabezpieczeń toodifferent zestawy zasobów platformy Azure. Mimo że domyślnie zasobów platformy Azure są sprawdzane dla wszystkich elementów zasad, można wyłączyć elementy poszczególnych zasad dla wszystkich zasobów platformy Azure lub dla grupy zasobów. Aby uzyskać szczegółowe informacje na temat zasad zabezpieczeń Centrum zabezpieczeń, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](../../security-center/security-center-policies.md). 

tooset się zasady zabezpieczeń dla wszystkich zasobów systemu Azure:

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zasady zabezpieczeń**, a następnie wybierz subskrypcję.
2. Wybierz **zasady zapobiegania**.
3. Włącz lub Wyłącz zasady elementów, które mają tooapply tooall zasobów platformy Azure.
4. Po wybraniu ustawienia, wybierz **OK**.
5. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**. 

tooset politykę dla określonej grupy zasobów:

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zasady zabezpieczeń**, a następnie wybierz grupę zasobów.
2. Wybierz **zasady zapobiegania**.
3. Włącz lub wyłącz elementów zasad czy chcesz, aby grupa zasobów toohello tooapply.
4. W obszarze **dziedziczenia**, wybierz pozycję **Unique**.
5. Po wybraniu ustawienia, wybierz **OK**.
6. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.  

Ponadto można wyłączyć zbieranie danych dla określonej grupy zasobów na tej stronie.

W hello poniższy przykład, zostało utworzone unikatowe zasady dla grupy zasobów o nazwie *myResoureGroup*. W tej zasadzie dysku szyfrowanie i sieci web aplikacji zapory zalecenia są wyłączone.

![Unikatowe zasady](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Wyświetl kondycję konfiguracji maszyny Wirtualnej

Po utworzeniu włączone zbieranie danych i ustaw zasadę zabezpieczeń, Centrum zabezpieczeń rozpoczyna tooprovide alertów i zalecenia. Podczas wdrażania maszyn wirtualnych, hello danych kolekcji agent jest zainstalowany. Centrum zabezpieczeń jest następnie wypełniane przy użyciu danych hello nowych maszyn wirtualnych. Aby uzyskać szczegółowe informacje o kondycji konfiguracji maszyny Wirtualnej, zobacz [ochrony maszyn wirtualnych w Centrum zabezpieczeń](../../security-center/security-center-virtual-machine-recommendations.md). 

Ponieważ dane są zbierane, są agregowane hello kondycja zasobów dla każdej maszyny Wirtualnej i powiązanych zasobów platformy Azure. Witaj informacje są wyświetlane na wykresie łatwe do odczytania. 

Kondycja zasobów tooview:

1.  Na pulpicie nawigacyjnym Centrum zabezpieczeń hello w obszarze **kondycja zabezpieczeń zasobów**, wybierz pozycję **obliczeniowe**. 
2.  Na powitania **obliczeniowe** bloku, wybierz opcję **maszyn wirtualnych**. Ten widok zawiera podsumowanie hello stanu konfiguracji dla wszystkich maszyn wirtualnych.

![Obliczenia bazy danych kondycji](./media/tutorial-azure-security/compute-health.png)

toosee wszystkie zalecenia dotyczące maszyny Wirtualnej, wybierz hello maszyny Wirtualnej. Zalecenia i korygowania są opisane bardziej szczegółowo w następnej sekcji hello tego samouczka.

## <a name="remediate-configuration-issues"></a>Korygowanie problemów z konfiguracją

Po rozpoczęciu toopopulate z danymi konfiguracji Centrum zabezpieczeń zalecenia są wykonywane na podstawie zasad zabezpieczeń hello skonfigurowane. Na przykład jeśli maszyna wirtualna została skonfigurowana bez skojarzonej sieciowej grupy zabezpieczeń, tworzone są zalecenia toocreate jeden. 

Lista wszystkich zaleceń wymienionych toosee: 

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zalecenia**.
2. Wybierz określonego zalecenia. Zostanie wyświetlona lista wszystkich zasobów, dla których ma zastosowanie hello zalecenia.
3. tooapply zalecenie, wybierz określonego zasobu. 
4. Wykonaj instrukcje hello czynności korygujące. 

W wielu przypadkach Centrum zabezpieczeń zapewnia można wykonać kroki można wykonać tooaddress zalecenie bez opuszczania Centrum zabezpieczeń. W hello poniższy przykład Centrum zabezpieczeń wykryje grupy zabezpieczeń sieci, która ma nieograniczony reguły ruchu przychodzącego. Na stronie zalecenie hello, można wybrać hello **edytowanie reguły ruchu przychodzącego** przycisku. zostanie wyświetlone Hello interfejsu użytkownika, która jest wymagana toomodify hello reguły. 

![Zalecenia](./media/tutorial-azure-security/remediation.png)

Zgodnie z zaleceniami zostaną rozwiązane, są one oznaczone jako rozwiązane. 

## <a name="view-detected-threats"></a>Wyświetl wykrytych zagrożeń

Ponadto tooresource konfiguracji zaleceń Centrum zabezpieczeń wyświetla alertów wykrywania zagrożeń. Funkcja alerty zabezpieczeń Hello agreguje dane zbierane z każdej maszyny Wirtualnej Azure dzienniki sieci i zagrożenia bezpieczeństwa toodetect rozwiązań partnerskich połączonych względem zasobów platformy Azure. Aby uzyskać szczegółowe informacje o funkcji wykrywania zagrożeń Centrum zabezpieczeń, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](../../security-center/security-center-detection-capabilities.md).

Funkcja alerty zabezpieczeń Hello wymaga cennik toobe warstwy zwiększyło się z Centrum zabezpieczeń hello *wolne* za*standardowe*. 30-dniowej **bezpłatnej wersji próbnej** jest dostępna w przypadku przenoszenia toothis wyższej warstwy cenowej. 

Warstwa cenowa hello toochange:  

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję.
2. Wybierz **warstwa cenowa**.
3. Wybierz hello nową warstwę, a następnie wybierz **wybierz**.
4. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**. 

Po zmianie hello warstwy cenowej, wykres alerty zabezpieczeń hello rozpoczyna toopopulate wykryciu zagrożenia bezpieczeństwa.

![Alerty zabezpieczeń](./media/tutorial-azure-security/security-alerts.png)

Wybierz informacje tooview alertu. Na przykład możesz wyświetlić opis hello zagrożeń, czas wykrycia hello, wszystkie próby zagrożeń i hello zalecanych czynności naprawczych. W hello poniższy przykład ataków siłowych RDP wykryto z 294 nieudanych prób RDP. Zalecane rozwiązanie jest dostępne.

![Atak protokołu RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Następne kroki
W tym samouczku Konfigurowanie Centrum zabezpieczeń Azure, a następnie przejrzeć maszyn wirtualnych w Centrum zabezpieczeń. W tym samouczku omówiono:

> [!div class="checklist"]
> * Konfigurowanie zbierania danych
> * Ustawianie zasad zabezpieczeń
> * Wyświetl i rozwiąż problemy z konfiguracją kondycji
> * Przejrzyj wykrytych zagrożeń

Następny samouczek toolearn toohello należy poprawić, jak toocreate CI/CD potoku z Visual Studio Team Services i maszyny Wirtualnej systemu Windows usług IIS.

> [!div class="nextstepaction"]
> [Visual Studio Team Services CI/CD potoku](./tutorial-vsts-iis-cicd.md)
