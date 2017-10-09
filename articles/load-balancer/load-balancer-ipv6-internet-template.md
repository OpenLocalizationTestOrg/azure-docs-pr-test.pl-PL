---
title: "aaaDeploy internetowy rozwiązania do równoważenia obciążenia w przypadku adresu IPv6 - szablonu Azure | Dokumentacja firmy Microsoft"
description: "Jak toodeploy IPv6 obsługi dla usługi równoważenia obciążenia Azure i maszyn wirtualnych z równoważeniem obciążenia."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Wdróż internetowy modułu równoważenia obciążenia rozwiązanie w przypadku adresu IPv6 przy użyciu szablonu

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](load-balancer-ipv6-internet-cli.md)
> * [Szablon](load-balancer-ipv6-internet-template.md)

Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP). Hello modułu równoważenia obciążenia zapewnia wysoką dostępność, przekazując przychodzący ruch między wystąpienie usługi działa prawidłowo usług w chmurze lub maszyn wirtualnych w zestawie usługi równoważenia obciążenia. Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.

## <a name="example-deployment-scenario"></a>Przykładowy scenariusz wdrażania

Witaj poniższym diagramie przedstawiono rozwiązania do równoważenia obciążenia hello wdrażane za pomocą szablonu przykład hello opisane w tym artykule.

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

W tym scenariuszu utworzysz hello następujących zasobów platformy Azure:

* Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany
* Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP
* dwa załadować równoważenia reguły toomap hello publiczne adresy VIP toohello prywatnej punkty końcowe
* Zestawu dostępności zawierający Witaj dwie maszyny wirtualne
* dwóch maszyn wirtualnych (VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Wdrażanie szablonu hello przy użyciu hello portalu Azure

W tym artykule odwołuje się do szablonu, który jest opublikowany w hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) galerii. Można pobrać szablonu hello z galerii hello lub uruchomić wdrożenia hello na platformie Azure bezpośrednio z galerii hello. W tym artykule przyjęto założenie, że komputer lokalny tooyour hello szablon został pobrany.

1. Otwórz hello portalu Azure i zaloguj się przy użyciu konta mającego uprawnienia toocreate maszyny wirtualne i zasoby sieciowe w ramach subskrypcji platformy Azure. Ponadto chyba, że korzystasz z istniejących zasobów, hello konto na potrzeby toocreate uprawnienia grupy zasobów i konto magazynu.
2. Kliknij przycisk "+ New" z hello menu, a następnie wpisz "szablon" w polu wyszukiwania hello. Wybierz "Wdrożenie szablonu" hello wyników wyszukiwania.

    ![lb-ipv6 — portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. W hello wszystko bloku, kliknij przycisk "Wdrażania szablonu."

    ![lb-ipv6 — portal — krok 3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Kliknij przycisk "Utwórz".

    ![lb-ipv6 — portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Kliknij pozycję "Edytuj szablon". Usuń istniejącą zawartość hello i kopiowania/wklejania w hello całą zawartość pliku szablonu hello (tooinclude hello rozpoczęcia i zakończenia {}), następnie kliknij przycisk "Zapisz".

    > [!NOTE]
    > Jeśli używasz programu Microsoft Internet Explorer możesz wkleić wyświetlane okno dialogowe z pytaniem, Schowka systemu Windows toohello dostępu tooallow. Kliknij pozycję "Zezwalaj na dostęp."

    ![lb-ipv6 — portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Kliknij pozycję "Edytuj parametry". W bloku parametrów hello Podaj wartości hello na powitania wskazówki w hello sekcji parametrów szablonu, a następnie kliknij przycisk Zapisz, tooclose hello parametry bloku. W bloku wdrożenie niestandardowe hello Wybierz subskrypcję, istniejącą grupę zasobów lub utwórz je. Jeśli tworzysz grupę zasobów, następnie wybierz lokalizację dla grupy zasobów hello. Następnie kliknij przycisk **postanowienia prawne**, następnie kliknij przycisk **zakupu** dla hello postanowienia prawne. Azure rozpoczyna wdrażanie hello zasobów. Może potrwać kilka minut toodeploy wszystkie zasoby hello.

    ![lb-ipv6 — portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Aby uzyskać więcej informacji na temat tych parametrów, zobacz hello [szablonu parametry i zmienne](#template-parameters-and-variables) sekcji w dalszej części tego artykułu.

7. zasoby hello toosee utworzone przez szablon powitania kliknij przycisk Przeglądaj, przewiń w dół listy hello do możesz wyświetlić "Grupy zasobów", a następnie kliknij go.

    ![lb-ipv6 — portal — krok 7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. W bloku grupy zasobów hello kliknij nazwę hello hello grupę zasobów, która została określona w kroku 6. Możesz wyświetlić listę wszystkich zasobów hello, które zostały wdrożone. Jeśli wszystkie poszło dobrze, powinien powiedzieć "Powodzenie" w obszarze "Ostatniego wdrożenia". Jeśli nie, sprawdź, czy hello konta, którego używasz, ma uprawnienia toocreate hello niezbędne zasoby.

    ![lb-ipv6 — portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Jeśli natychmiast po ukończeniu kroku 6 możesz przeglądać grup zasobów, "Ostatniego wdrożenia" będzie wyświetlany stan hello "Wdrażanie" podczas wdrażania hello zasobów.

9. Kliknij przycisk "myIPv6PublicIP" hello liście zasobów. Zostanie wyświetlony, ma adres IPv6 w polu adres IP, i że jego nazwa DNS jest określona dla parametru dnsNameforIPv6LbIP hello w kroku 6 wartość hello. Ten zasób jest hello publicznego IPv6 adresu i nazwy hosta, który jest dostępny tooInternet komputerów klienckich.

    ![lb-ipv6 — portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Sprawdzanie poprawności łączności

Po pomyślnym wdrożeniu hello szablonu można zweryfikować łączności, wykonując następujące zadania hello:

1. Zaloguj się toohello portalu Azure i połącz tooeach hello maszyny wirtualne utworzone przez hello szablonu wdrożenia. Jeśli wdrożono Maszynę wirtualną serwera systemu Windows, uruchom polecenie ipconfig/z wiersza polecenia. Możesz sprawdzić, czy hello maszyny wirtualne mają adresy IPv4 i IPv6. Jeśli wdrożono maszyn wirtualnych systemu Linux należy tooconfigure hello systemu operacyjnego Linux tooreceive dynamiczne adresy IPv6 przy użyciu hello instrukcjami dla dystrybucji systemu Linux.
2. W kliencie połączony z Internetem IPv6 inicjują połączenia toohello publiczny adres IPv6 hello usługi równoważenia obciążenia. tooconfirm, który hello modułu równoważenia obciążenia jest równoważenia między maszynami wirtualnymi hello dwa, takich jak Microsoft Internet Information Services (IIS) serwera sieci web można zainstalować na każdym hello maszyn wirtualnych. Hello domyślnej strony sieci web na każdym serwerze mogą zawierać tekst hello "Server0" lub "Serwer1" toouniquely go zidentyfikować. Następnie otwórz przeglądarkę internetową na kliencie podłączonej do Internetu IPv6 i Przeglądaj hostname toohello, określona dla parametru dnsNameforIPv6LbIP hello hello obciążenia równoważenia tooconfirm end-to-end IPv6 łączności tooeach maszyny Wirtualnej. Jeśli widzisz tylko hello strony sieci web z tylko jednego serwera, może być konieczne tooclear pamięć podręczną przeglądarki. Otwórz wiele prywatnych sesji przeglądania. Powinna zostać wyświetlona odpowiedź z każdego serwera.
3. W kliencie podłączonej do Internetu IPv4 inicjują połączenia toohello publiczny adres IPv4 hello usługi równoważenia obciążenia. tooconfirm, który hello modułu równoważenia obciążenia jest równoważenia obciążenia Witaj dwie maszyny wirtualne, można przetestować za pomocą usług IIS, zgodnie z opisem w kroku 2.
4. Z każdej maszyny Wirtualnej inicjują połączenia wychodzącego tooan IPv6 lub urządzenie IPv4 podłączonej do Internetu. W obu przypadkach hello źródłowy adres IP zostały odebrane przez urządzenie docelowe hello jest hello publiczny adres IPv4 lub IPv6 hello usługi równoważenia obciążenia.

> [!NOTE]
> Protokół ICMP dla protokołów IPv4 i IPv6 są zablokowane w hello sieć platformy Azure. W związku z tym ICMP narzędzia, takie jak ping zawsze zakończyć się niepowodzeniem. tootest połączenie, użyj zamiast protokołu TCP, takie jak TCPing lub hello polecenia cmdlet programu PowerShell Test-NetConnection. Należy pamiętać, że adresy IP wyświetlane na diagramie hello hello są przykładowe wartości, które można napotkać. Ponieważ adresy hello IPv6 są przypisywane dynamicznie, hello adresów, które otrzymujesz różnią się i zależą od regionu. Ponadto są często hello publiczny adres IPv6 na toostart usługi równoważenia obciążenia hello z prefiksem innego niż hello prywatnych adresów IPv6 w puli zaplecza hello.

## <a name="template-parameters-and-variables"></a>Parametry szablonu i zmienne

Szablon usługi Azure Resource Manager zawiera wiele zmiennych i parametrów dostosować tooyour potrzeb. Zmienne są używane dla wartości stałych zrezygnować toochange użytkownika. Parametry są używane dla wartości mają tooprovide użytkownika, wdrażając hello szablonu. Szablon przykład Hello jest skonfigurowany dla hello scenariusz opisany w tym artykule. Można dostosować ten tooneeds środowiska.

przykład Witaj szablon używany w tym artykule obejmuje następujące hello zmiennych i parametrów:

| Parametr / zmiennej | Uwagi |
| --- | --- |
| adminUsername |Określ hello nazwa konta administratora hello używana toosign toohello maszynom wirtualnym. |
| adminPassword |Określ hello hasło dla konta administratora hello używane toosign w toohello maszynom wirtualnym. |
| dnsNameforIPv4LbIP |Określ nazwę hosta DNS hello ma tooassign jako nazwę publiczną hello hello usługi równoważenia obciążenia. Ta nazwa jest rozpoznawany jako publiczny adres IPv4 toohello usługi równoważenia obciążenia. Nazwa Hello musi być małe litery i odpowiada hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Określ nazwę hosta DNS hello ma tooassign jako nazwę publiczną hello hello usługi równoważenia obciążenia. Ta nazwa jest rozpoznawany jako publiczny adres IPv6 toohello usługi równoważenia obciążenia. Nazwa Hello musi być małe litery i odpowiada hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Może to być hello sama nazwa jak hello adres IPv4. Gdy klient wysyła zapytanie DNS dla tej nazwy Azure zwróci zarówno hello A, jak i rekordów AAAA, gdy nazwa hello są udostępniane. |
| vmNamePrefix |Określ prefiks nazwy hello maszyny Wirtualnej. Szablon Hello dołącza numer (0, 1, itp.) toohello nazwy podczas hello maszyny wirtualne są tworzone. |
| nicNamePrefix |Określ prefiks nazwy interfejsu sieciowego hello. Szablon Hello dołącza numer (0, 1, itp.) nazwa toohello podczas tworzenia hello interfejsów sieciowych. |
| storageAccountName |Wprowadź nazwę istniejącego konta magazynu hello lub określ nazwę nowej toobe jeden utworzone przez szablon hello hello. |
| availabilitySetName |Wprowadź nazwę dostępności hello ustawić toobe używane z hello maszyny wirtualne |
| addressPrefix |Prefiks adresu Hello używany zakres adresów hello toodefine hello sieci wirtualnej |
| subnetName |Hello nazwę podsieci hello utworzone dla hello sieci wirtualnej |
| subnetPrefix |Prefiks adresu Hello używany zakres adresów hello toodefine hello podsieci |
| vnetName |Określ nazwę hello hello używane przez hello maszyn wirtualnych w sieci wirtualnej. |
| ipv4PrivateIPAddressType |Metoda alokacji Hello używana w przypadku hello prywatnego adresu IP (statyczna lub dynamiczna) |
| ipv6PrivateIPAddressType |Metoda alokacji Hello używana w przypadku hello prywatnego adresu IP (dynamiczny). Protokół IPv6 obsługuje tylko dynamicznej alokacji. |
| numberOfInstances |wdrożone przez szablon hello zrównoważonym Hello liczba obciążenia |
| ipv4PublicIPAddressName |Podaj nazwę DNS hello ma toocommunicate toouse z hello publiczny adres IPv4 hello usługi równoważenia obciążenia. |
| ipv4PublicIPAddressType |Metoda alokacji Hello służąca do hello publicznego adresu IP (statyczna lub dynamiczna) |
| Ipv6PublicIPAddressName |Podaj nazwę DNS hello ma toocommunicate toouse z hello publiczny adres IPv6 hello usługi równoważenia obciążenia. |
| ipv6PublicIPAddressType |Metoda alokacji Hello używana hello publicznego adresu IP (dynamiczny). Protokół IPv6 obsługuje tylko dynamicznej alokacji. |
| lbName |Określ nazwę hello hello usługi równoważenia obciążenia. Ta nazwa jest wyświetlana w portalu hello lub używany podczas odwoływania się tooit za pomocą polecenia interfejsu wiersza polecenia lub środowiska PowerShell. |

Hello pozostałe zmienne w szablonie hello zawierają pochodnej wartości, które są przypisywane, gdy platforma Azure tworzy hello zasobów. Nie należy zmieniać tych zmiennych.
