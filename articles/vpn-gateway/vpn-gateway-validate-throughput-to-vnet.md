---
title: "Sprawdzanie poprawności sieci VPN tooa przepustowość sieci wirtualnej Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Witaj celem niniejszego dokumentu jest toohelp użytkownika zweryfikować hello przepływność sieci z ich tooan zasoby lokalne maszyny wirtualnej platformy Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Jak sieci wirtualnej przepływności tooa toovalidate sieci VPN

Połączenie bramy sieci VPN włącza bezpieczny, łączności między lokalizacjami tooestablish między sieci wirtualnej w systemie Azure i lokalnej infrastruktury IT.

W tym artykule przedstawiono sposób toovalidate przepływność sieci z hello lokalnymi tooan zasobów maszyny wirtualnej platformy Azure. Umożliwia także wskazówki dotyczące rozwiązywania problemów.

>[!NOTE]
>Ten artykuł dotyczy toohelp diagnozowanie i rozwiązywanie typowych problemów. Jeśli masz problem hello toosolve przy użyciu następujących informacji, hello [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Omówienie

Witaj połączenie bramy sieci VPN obejmuje hello następujące składniki:

- Lokalnego urządzenia sieci VPN (wyświetlanie listy [zweryfikowane urządzenia sieci VPN)](vpn-gateway-about-vpn-devices.md#devicetable).
- Publicznego Internetu
- Brama sieci VPN
- Maszyna wirtualna platformy Azure

powitania po diagram przedstawia hello logicznej łączność tooan sieci lokalnej sieci wirtualnej platformy Azure za pośrednictwem sieci VPN.

![Sieci logiczne tooMSFT sieci łączności klienta przy użyciu sieci VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Oblicz hello maksymalna oczekiwana wejście/wyjście

1.  Ustal wymagania dotyczące przepływności linii bazowej aplikacji.
2.  Określ swoje limity przepływność bramy sieci VPN platformy Azure. Aby uzyskać pomoc, zobacz sekcję hello "łącznej przepływności według jednostki SKU i sieci VPN typu" [planowania i projektowania dla bramy sieci VPN](vpn-gateway-plan-design.md).
3.  Określić hello [maszyny Wirtualnej Azure przepływności wskazówki](../virtual-machines/virtual-machines-windows-sizes.md) dla rozmiar maszyny Wirtualnej.
4.  Określ przepustowość usługodawcy internetowego (ISP).
5.  Obliczanie przepływności oczekiwanego - minimalnej przepustowości (maszyna wirtualna, brama usługodawcy internetowego) * 0,8.

Jeśli Twoje obliczeniowej przepływności nie spełnia wymagania dotyczące przepływności linii bazowej aplikacji, należy tooincrease hello przepustowości hello zasobu, który został zidentyfikowany jako "wąskie gardło" hello. tooresize bramy sieci VPN platformy Azure, zobacz [zmiana jednostka SKU bramy](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize maszyny wirtualnej, zobacz [Zmień rozmiar maszyny Wirtualnej](../virtual-machines/virtual-machines-windows-resize-vm.md). Jeśli nie występują oczekiwanego przepustowości połączenia z Internetem, można również toocontact usługodawcy.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Sprawdź poprawność przepływność sieci przy użyciu narzędzia wydajności

Ta powinna być sprawdzana podczas godziny poza szczytem, jak nasycenie przepływności tunelu VPN podczas testowania nie daje prawidłowych wyników.

Narzędzie Hello, używanego dla tego testu jest dotyczące programu Iperf; która działa w systemach Windows i Linux i trybach klienta i serwera. Jest ograniczona too3 GB/s dla maszyn wirtualnych systemu Windows.

To narzędzie nie wykonuje żadnych toodisk operacje odczytu/zapisu. Tworzy wyłącznie automatycznie wygenerowany ruch TCP z jednego toohello zakończenia, inne. Statystyka oparta na eksperymenty, która hello dostępna przepustowość między klientem i serwerem węzłów on wygenerowany. Podczas testowania między dwoma węzłami, co działa jako serwer hello i hello innych jako klienta. Po zakończeniu tego testu, firma Microsoft zaleca, aby odwrócić hello ról tootest zarówno przekazywanie i pobieranie przepływności na obu węzłów.

### <a name="download-iperf"></a>Pobierz dotyczące programu Iperf
Pobierz [dotyczące programu Iperf;](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Aby uzyskać więcej informacji, zobacz [dokumentacji dotyczące programu Iperf;](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >produkty innych firm Hello omówione w tym artykule są wytwarzane przez producentów niezależnych od firmy Microsoft. Firma Microsoft nie udziela żadnych gwarancji, dorozumianych ani żadnego innego o hello wydajności ani niezawodności tych produktów.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Uruchom dotyczące programu Iperf; (iperf3.exe)
1. Włącz reguły NSG/list kontroli dostępu zezwala na ruch hello (na potrzeby testowania na maszynie Wirtualnej Azure publiczny adres IP).

2. W obu węzłach Włącz wyjątek zapory dla portu 5001.

    **System Windows:** następujące hello Uruchom polecenie jako administrator:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    Reguła hello tooremove podczas testowania zostanie zakończone, uruchom to polecenie:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux:** obrazów systemu Linux platformy Azure są ograniczająca zapory. Czy aplikacja nasłuchuje na porcie, hello ruch jest dozwolony przez. Otwarte jawnie portów może być konieczne niestandardowych obrazów, które są zabezpieczone. Typowe zapory systemu operacyjnego Linux warstwy obejmują `iptables`, `ufw`, lub `firewalld`.

3. W węźle serwera hello Zmień katalog toohello, w której jest wyodrębniany iperf3.exe. Następnie uruchom dotyczące programu Iperf; w trybie serwera i ustaw go toolisten na porcie 5001 jako hello następującego polecenia:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. W węźle powitania klienta zmienić toohello katalogu zawierającego narzędzia dotyczące programu Iperf; jest wyodrębniany, a następnie uruchom hello następujące polecenie:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    powitania klienta to powoduje ruch na porcie 5001 toohello serwera przez 30 sekund. Witaj flagi "-P" wskazujące, że użyto 32 węzeł serwera toohello równoczesnych połączeń.

    Hello poniższym ekranie przedstawiono hello dane w tym przykładzie:

    ![Dane wyjściowe](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. Witaj toopreserve (OPCJONALNIE) testowanie wyników, uruchom to polecenie:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Po wykonaniu poprzednich kroków hello, należy wykonać hello cofnąć te same czynności z rolami hello, tak, aby hello węzeł serwera teraz powitania klienta i na odwrót.

## <a name="address-slow-file-copy-issues"></a>Rozwiązać problemy kopii pliku powolne
Mogą wystąpić powolne pliku kopiowanie przy użyciu Eksploratora Windows lub przeciągania i upuszczania za pomocą sesji protokołu RDP. Tego problemu jest zwykle tooone lub oba hello następujące czynniki:

- Podczas kopiowania plików, aplikacji kopiowania plików, takich jak Eksplorator Windows i protokołu RDP, nie należy używać wiele wątków. W celu poprawy wydajności użyj aplikacji kopii pliku wielowątkowych takiego jak [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy plików za pomocą wątków 16 lub 32. numer wątku hello toochange kopiowanie plików w programie Richcopy, kliknij przycisk **akcji** > **opcje kopiowania** > **skopiowanie pliku**.<br><br>
![Zagadnienia dotyczące kopiowania plików powolne](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Za mało szybkość odczytu/zapisu dysku maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z magazynu Azure](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interfejs połączonej zewnętrznego urządzenia lokalnego
Jeśli hello lokalnego urządzenia sieci VPN adres internetowy jest uwzględniona w hello [sieci lokalnej](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definicji na platformie Azure, mogą wystąpić toobring brakiem hello zakończy połączenie sieci VPN, sporadyczne lub problemów z wydajnością.

## <a name="checking-latency"></a>Sprawdzanie opóźnienia
Użyj tracert tootrace tooMicrosoft Azure krawędzi urządzenia toodetermine, jeśli istnieją wszelkich opóźnień powyżej 100 ms między przeskoków.

Z sieci lokalnej hello, uruchom *tracert* toohello VIP hello Azure bramy lub maszyny Wirtualnej. Gdy zostanie wyświetlony tylko * zwrócone, wiadomo, został osiągnięty hello Azure krawędzi. Po wyświetleniu nazwy DNS, które obejmują "MSN" zwrócił wiadomo, że został osiągnięty hello firmy Microsoft w sieci szkieletowej.<br><br>
![Sprawdzanie opóźnienia](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji lub uzyskać pomoc zapoznaj się hello następującego łącza:

- [Zoptymalizować przepływność sieci maszyn wirtualnych platformy Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Pomoc techniczna firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
