---
title: "aaaConnecting Twojego zabezpieczeń produktów toohello zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia możesz tooconnect tooOperations produkty zabezpieczeń zabezpieczeń pakietu administracyjnego i rozwiązanie inspekcji za pomocą typowego formatu zdarzeń."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Łączenie z zabezpieczeń produktów toohello zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji 
Ten dokument ułatwia połączenie z produktów zabezpieczeń hello OMS zabezpieczeń i rozwiązanie inspekcji. obsługiwane są następujące źródła Hello:

- Zdarzenia w formacie Common Event Format (CEF)
- Zdarzenia Cisco ASA


## <a name="what-is-cef"></a>Co to jest format CEF?
Typowe formatu zdarzeń (CEF) jest branży formatem u góry komunikaty dziennika systemowego, używane przez wielu dostawców tooallow zdarzeń zgodności zabezpieczeń między różnymi platformami. Zabezpieczenia OMS i inspekcji rozwiązanie obsługuje wprowadzanie danych przy użyciu CEF, co pozwala tooconnect produkty zabezpieczeń z zabezpieczeniami OMS. 

Nawiązując połączenie z tooOMS źródła danych, jest możliwe tootake zaletą hello następujące funkcje, które są częścią tej platformy:

- Wyszukiwanie i korelacja
- Inspekcja
- Alerty
- Analiza zagrożeń
- Problemy godne uwagi

## <a name="collection-of-security-solution-logs"></a>Zbieranie dzienników rozwiązań dotyczących zabezpieczeń

Zabezpieczenia pakietu OMS obsługują zbieranie dzienników w formacie CEF przez dzienniki systemu i dzienniki rozwiązania [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). W tym przykładzie hello źródło (komputer, który generuje dzienniki hello) jest uruchomiony demon syslog ng komputera z systemem Linux i docelowy hello jest OMS zabezpieczeń. komputer z systemem Linux hello tooprepare należy hello tooperform następujące zadania:

- Pobierz hello Agent pakietu OMS dla systemu Linux, 1.2.0-25 wersji lub nowszej.
- Postępuj zgodnie z sekcji hello **krótki przewodnik instalowania** z [w tym artykule](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall i dołączyć hello agenta tooyour roboczym.

Zazwyczaj hello agent jest zainstalowany na innym komputerze z hello są generowane, na których dzienniki hello. Komputer agenta przekazywania hello dzienniki toohello zwykle wymaga hello następujące kroki:

- Na maszynie agenta hello, skonfiguruj hello rejestrowania produktu/machine tooforward hello wymagane zdarzenia toohello demon syslog (rsyslog lub syslog ng).
- Włącz hello demon syslog na wiadomości powitania od agenta maszyny tooreceive z systemu zdalnego.

Na maszynie agenta hello hello zdarzeń muszą toobe wysyłane z portem UDP toolocal demon syslog hello 25226. Hello agent nasłuchuje przychodzących zdarzeń na tym porcie. Hello poniżej przedstawiono przykładową konfigurację do wysyłania wszystkie zdarzenia z agenta toohello systemu lokalnego hello (można modyfikować toofit konfiguracji hello ustawienia lokalne):

1. Witaj Otwórz okno terminala i przejdź toohello katalogu */etc/syslog-ng /* 
2. Utwórz nowy plik *zabezpieczeń config-omsagent.conf* i Dodaj hello następującej zawartości: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Pobierz plik hello *security_events.conf* i umieścić w */etc/opt/microsoft/omsagent/conf/omsagent.d/* w komputerze agenta pakietu OMS hello.
4. Wpisz poniższe polecenie hello demon syslog hello toorestart: *dla ng syslog, uruchom:*
    
    ```
    sudo service rsyslog restart
    ```

    *Uruchamianie demona rsyslog:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Wpisz poniższe polecenie hello hello toorestart Agent pakietu OMS:

    *Uruchamianie demona syslog-ng:*
    
    ```
    sudo service omsagent restart
    ```

    *Uruchamianie demona rsyslog:*
    
    ```
    systemctl restart omsagent
    ```
6. Wpisz poniższe polecenie hello i przejrzyj hello wynik tooconfirm, że nie ma żadnych błędów w dzienniku agenta pakietu OMS hello:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Przeglądanie zebranych zdarzeń zabezpieczeń

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Po hello konfiguracji przez program hello zdarzeń zabezpieczeń zostanie uruchomiony toobe pozyskanych przez zabezpieczenia OMS. toovisualize tych zdarzeń, otwórz hello dziennik wyszukiwania, wpisz polecenie hello *typu = CommonSecurityLog* w hello pola wyszukiwania i naciśnij klawisz ENTER. Witaj poniższy przykład przedstawia wynik hello tego polecenia Zwróć uwagę, że w takim przypadku zabezpieczeń OMS już pozyskanych dzienniki zabezpieczeń z wielu dostawców:
   
![Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Można uściślić wyszukiwanie dla jednego dostawcy, na przykład toovisualize dzienniki online Cisco, typ: *typu = CommonSecurityLog DeviceVendor = Cisco*. dla dowolnego nagłówka CEF także podstawowe extensios hello podczas inne rozszerzenia "Niestandardowe rozszerzenie" lub nie zostanie wstawiony do pola "AdditionalExtensions" Hello "CommonSecurityLog" ma wstępnie zdefiniowane pola. Można użyć hello pola niestandardowe funkcji tooget dedykowanego pola z niego. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Dostęp do komputerów, dla których brak oceny linii bazowej
OMS obsługuje opinii linii bazowej hello domeny systemu Windows Server 2008 R2 tooWindows Server 2012 R2. Ostateczna wersja linii bazowej dla systemu Windows Server 2016 nie jest jeszcze opracowana i zostanie dodana natychmiast po jej opublikowaniu. Wszystkie inne systemy operacyjne skanowania za pomocą oceny linii bazowej OMS zabezpieczeń i inspekcji są wyświetlane w obszarze hello **komputery z brakującą oceny linii bazowej** sekcji.

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób tooconnect Twojego tooOMS rozwiązania CEF. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

