---
title: "Równoważenie obciążenia aaaUsing usługi na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toocreate scenariusza za pomocą hello Azure portfolio równoważenia obciążenia: Traffic Manager, bramę aplikacji i moduł równoważenia obciążenia."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Przy użyciu usługi równoważenia obciążenia na platformie Azure

## <a name="introduction"></a>Wprowadzenie

Microsoft Azure udostępnia wiele usług do zarządzania ruchem w sieci i równoważenia obciążenia. Możesz użyć tych usług indywidualnie lub łączenie ich metod w zależności od potrzeb toobuild hello najlepszego rozwiązania.

W tym samouczku, firma Microsoft najpierw zdefiniować przypadek użycia klienta i wyświetlić sposób można go było bardziej niezawodne i wydajności za pomocą powitania po portfolio równoważenia obciążenia Azure: Traffic Manager, bramę aplikacji i moduł równoważenia obciążenia. Następnie udostępniamy instrukcje tworzenia wdrożenia, które jest geograficznie nadmiarowy, dystrybuuje ruch tooVMs i pomaga w zarządzaniu różnych typów żądań.

Na poziomie pojęciach każdy z tych usług pełni rolę różne hello hierarchii równoważenia obciążenia.

* **Menedżer ruchu** zapewnia DNS globalnego równoważenia obciążenia. Analizuje przychodzące żądania DNS i odpowiada punkt końcowy w dobrej kondycji, zgodnie z hello routingu zasad powitania klienta został wybrany. Dostępne są następujące opcje dla metody routingu:
  * Wydajność routingu toosend hello obiektu żądającego toohello najbliższy punkt końcowy pod względem opóźnienia.
  * Priorytet routingu toodirect wszystkie ruchu tooan punktu końcowego z innych punktów końcowych na kopii zapasowej.
  * Ważone działanie okrężne routingu, która dystrybuuje ruch według wagi hello, przypisany tooeach punktu końcowego.

  Witaj, klient połączy się bezpośrednio toothat punktu końcowego. Menedżer ruchu Azure wykrywa punkt końcowy jest zła, a następnie przekierowuje hello wystąpienia dobrej kondycji tooanother klientów. Odwołuje się zbyt[dokumentacji usługi Azure Traffic Manager](traffic-manager-overview.md) toolearn więcej o usłudze hello.
* **Brama aplikacji w** zawiera kontroler dostarczania aplikacji (ADC) jako usługa, oferty różnych warstwy 7 Równoważenie obciążenia sieciowego funkcji aplikacji. Pozwala ona klientom wydajność kolektywu serwerów sieci web toooptimize dzięki przeniesieniu brama aplikacji w toohello zakończenia SSL użycie Procesora CPU. Inne funkcje routingu warstwy 7 obejmują rozdzielanie ruchu przychodzącego, koligacji na podstawie plików cookie sesji, routingu adresów URL na podstawie ścieżki i toohost możliwości hello wiele witryn sieci Web za bramy pojedynczej aplikacji. Brama aplikacji można skonfigurować jako bramy łączącej z Internetem, bramę wyłącznie wewnętrznym lub obie te grupy. Brama aplikacji jest w pełni Azure zarządzanych, skalowalności i wysokiej dostępności. Zapewnia ona bogaty zestaw funkcji diagnostyki i rejestrowania, aby uprościć zarządzanie.
* **Moduł równoważenia obciążenia** jest integralną częścią hello Azure SDN stosu, udostępnia wysokiej wydajności i małych opóźnieniach 4 warstwy równoważenia obciążenia usługi dla wszystkich protokołów UDP i TCP protokołów. Zarządza połączeń przychodzących i wychodzących. Można skonfigurować publicznych oraz wewnętrznych końcowych z równoważeniem obciążenia i zdefiniuj toomap reguły ruchu przychodzącego miejsc docelowych puli tooback zakończenia połączenia przy użyciu protokołu TCP i HTTP badania kondycji opcje toomanage dostępności usługi.

## <a name="scenario"></a>Scenariusz

W tym przykładowym scenariuszu używamy prosty witryny sieci Web, który obsługuje dwa typy zawartości: obrazów i dynamicznie renderowanych stronach sieci Web. Witaj witryny sieci Web musi być geograficznie nadmiarowy, a powinien służyć swoim użytkownikom z hello najbliższego (można uzyskać najmniejsze opóźnienia) toothem lokalizacji. Hello Deweloper aplikacji postanowiła, że wszystkie adresy URL zgodne hello wzorzec/obrazów / * są obsługiwane z dedykowanym puli maszyn wirtualnych, które różnią się od reszty hello hello kolektywu serwerów sieci web.

Ponadto hello domyślną maszyny Wirtualnej pulę obsługę zawartości dynamicznej hello musi tootalk tooa wewnętrznej bazy danych znajdującej się na klastrze wysokiej dostępności. wdrożenie całej Hello jest skonfigurowana za pośrednictwem usługi Azure Resource Manager.

Przy użyciu usługi Traffic Manager, bramę aplikacji i usługi równoważenia obciążenia umożliwia tooachieve tej witryny sieci Web te cele projektowania:

* **Nadmiarowość geograficzna Multi**: Jeśli jeden region ulegnie awarii, trasy menedżera ruchu bezproblemowo ruchu toohello region najbliższy bez żadnej interwencji ze właściciel aplikacji hello.
* **Mniejsze opóźnienia**: ponieważ Traffic Manager automatycznie kieruje powitania klienta toohello najbliżej regionu, powitania klienta napotyka mniejsze opóźnienia podczas żądania hello zawartości strony sieci Web.
* **Skalowalność niezależne**: ponieważ obciążenia aplikacji sieci web hello jest oddzielona typu zawartości, właściciel aplikacji hello można skalować obciążeń żądania powitania od siebie niezależne. Brama aplikacji w zapewnia, że ruch hello jest routingiem toohello pule prawo oparte na powitania określone zasady i hello kondycji aplikacji hello.
* **Równoważenie obciążenia wewnętrznego**: ponieważ moduł równoważenia obciążenia jest przed hello klastra o wysokiej dostępności, tylko hello aktywne i dobrej kondycji punktu końcowego dla bazy danych jest narażonych toohello aplikacji. Ponadto administrator bazy danych można zoptymalizować hello obciążenia przez dystrybucję replik aktywnym i pasywnym klastra hello niezależnie od hello aplikacji frontonu. Moduł równoważenia obciążenia zapewnia klastra o wysokiej dostępności toohello połączeń i zapewnia tylko dobrej kondycji bazy danych żądania połączenia.

Witaj Poniższy diagram przedstawia architekturę hello tego scenariusza:

![Diagram równoważenia obciążenia architektury](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> W tym przykładzie jest tylko jeden z wielu możliwych konfiguracji równoważenia obciążenia usług hello, które platforma Azure oferuje. Można łączyć Menedżera ruchu, bramę aplikacji i usługi równoważenia obciążenia i dopasowany toobest potrzebami równoważenia obciążenia. Na przykład jeśli odciążanie protokołu SSL lub przetwarzania warstwy 7 nie jest konieczne, usługi równoważenia obciążenia można użyć zamiast Application Gateway.

## <a name="setting-up-hello-load-balancing-stack"></a>Konfigurowanie hello stosu równoważenia obciążenia

### <a name="step-1-create-a-traffic-manager-profile"></a>Krok 1: Tworzenie profilu Menedżera ruchu

1. W portalu Azure hello, kliknij przycisk **nowy**, a następnie wyszukaj hello marketplace "Profilu Menedżera ruchu".
2. Na powitania **profilu usługi Traffic Manager utwórz** bloku, wprowadź hello następujące podstawowe informacje:

  * **Nazwa**: należy podać nazwę prefiks DNS profilu Menedżera ruchu.
  * **Metoda routingu**: Wybierz hello zasad metody routingu ruchu. Aby uzyskać więcej informacji na temat metod hello, zobacz [Traffic Manager metody routingu ruchu](traffic-manager-routing-methods.md).
  * **Subskrypcja**: Wybierz subskrypcję hello, który zawiera profil hello.
  * **Grupa zasobów**: hello wybierz grupę zasobów, która zawiera profil hello. Może być grupą nowy lub istniejący zasób.
  * **Lokalizacja grupy zasobów**: Usługa Menedżera ruchu jest globalna i niepowiązana tooa lokalizacji. Należy jednak określić region hello grupy, którym znajduje się hello metadane skojarzone z profilem Menedżera ruchu hello. Ta lokalizacja nie ma wpływu na dostępność środowiska uruchomieniowego hello hello profilu.

3. Kliknij przycisk **Utwórz** hello toogenerate profilu usługi Traffic Manager.

  ![Blok "Tworzenie Menedżera ruchu"](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Krok 2: Tworzenie hello bramy aplikacji

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij **nowy** > **sieci** > **brama aplikacji w**.
2. Wprowadź następujące podstawowe informacje na temat bramy aplikacji hello hello:

  * **Nazwa**: hello nazwy bramy aplikacji hello.
  * **Rozmiar jednostki SKU**: hello rozmiaru bramy aplikacji hello, dostępne jako mały, średni lub duży.
  * **Liczba wystąpień**: hello liczba wystąpień, wartość z zakresu od 2 do 10.
  * **Grupa zasobów**: hello grupę zasobów, która przechowuje hello bramy aplikacji. Można go istniejącą grupę zasobów lub do nowego.
  * **Lokalizacja**: hello region bramy aplikacji hello, która jest sama hello lokalizacji jako grupa zasobów hello. lokalizacji Hello jest ważne, ponieważ hello sieć wirtualna i publiczny adres IP musi znajdować się w hello tej samej lokalizacji co brama hello.
3. Kliknij przycisk **OK**.
4. Zdefiniuj hello sieci wirtualnej, podsieci IP frontonu i konfiguracji odbiornika dla bramy aplikacji hello. W tym scenariuszu jest adres IP frontonu hello **publicznych**, dzięki czemu toobe później dodane jako toohello punktu końcowego profilu Menedżera ruchu.
5. Skonfiguruj hello odbiornika z jednym hello następujące opcje:
    * Jeśli używasz protokołu HTTP nie ma nic tooconfigure. Kliknij przycisk **OK**.
    * Jeśli jest używany protokół HTTPS, konfiguracji są wymagane dodatkowe. Odwołuje się zbyt[Utwórz bramę aplikacji](../application-gateway/application-gateway-create-gateway-portal.md), rozpoczynając od kroku 9. Po zakończeniu konfiguracji powitania kliknij **OK**.

#### <a name="configure-url-routing-for-application-gateways"></a>Konfigurowanie adresu URL routingu dla bramy aplikacji

Po wybraniu puli zaplecza bramy aplikacji, który jest skonfigurowany przy użyciu reguły na podstawie ścieżki przyjmuje wzorzec ścieżki adresu URL żądania hello dodanie działania okrężnego tooround dystrybucji. W tym scenariuszu dodajemy toodirect reguły na podstawie ścieżki dowolny adres URL z "/images/\*" puli serwerów toohello obrazu. Aby uzyskać więcej informacji na temat konfigurowania adresu URL na podstawie ścieżki routingu dla bramy aplikacji można znaleźć zbyt[Tworzenie reguły na podstawie ścieżki dla bramy aplikacji](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagram warstwa sieci web bramy aplikacji](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. W grupie zasobów przejść toohello wystąpienie bramy aplikacji hello, który został utworzony w powyższej sekcji hello.
2. W obszarze **ustawienia**, wybierz pozycję **pul zaplecza**, a następnie wybierz **Dodaj** hello tooadd maszyn wirtualnych, które mają tooassociate z pul zaplecza warstwa sieci web hello.
3. Na powitania **Dodaj pulę zaplecza** bloku, wprowadź nazwę hello hello puli zaplecza i wszystkie adresy IP hello hello maszyn, które znajdują się w puli hello. W tym scenariuszu połączono dwie pule serwera zaplecza maszyn wirtualnych.

  ![Blok "Dodaj pulę zaplecza" bramy aplikacji](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. W obszarze **ustawienia** bramy aplikacji hello, wybierz **reguły**, a następnie kliknij przycisk hello **opartych na ścieżce** tooadd przycisk reguły.

  ![Przycisk "Na podstawie ścieżki" reguły bramy aplikacji](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Na powitania **reguły na podstawie ścieżki Dodaj** bloku, skonfiguruj regułę hello zapewniając hello następujących informacji.

   Podstawowe ustawienia:

   + **Nazwa**: hello przyjazną nazwę reguły hello, który jest dostępny w portalu hello.
   + **Odbiornik**: hello odbiornik, który jest używany dla hello reguły.
   + **Domyślna pula zaplecza**: hello używane z regułą domyślnego hello toobe puli zaplecza.
   + **Domyślne ustawienia HTTP**: używane z regułą domyślnego hello toobe ustawienia hello HTTP.

   Ścieżka reguły:

   + **Nazwa**: hello przyjazną nazwę reguły na podstawie ścieżki hello.
   + **Ścieżki**: hello reguły ścieżki, która jest używana do przesyłania ruchu.
   + **Puli zaplecza**: hello toobe puli zaplecza używane z tą regułą.
   + **Ustawienie HTTP**: hello HTTP toobe ustawienia używane z tą regułą.

   > [!IMPORTANT]
   > Ścieżki: Ścieżkach prawidłowy musi rozpoczynać się od "/". Witaj symbolu wieloznacznego "\*" jest dozwolona tylko na końcu hello. Nieprawidłowa przykładów /xyz, /xyz\*, lub /xyz/\*.

   ![Blok "Dodaj ścieżkę na podstawie reguły" bramy aplikacji](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Krok 3: Dodawanie punktów końcowych usługi Traffic Manager toohello bramy aplikacji

W tym scenariuszu Menedżera ruchu jest bram tooapplication podłączonej (zgodnie z konfiguracją w poprzednich krokach hello), które znajdują się w różnych regionach. Po skonfigurowaniu bramy aplikacji hello, hello następnym krokiem jest tooconnect ich tooyour profilu usługi Traffic Manager.

1. Otwórz profil Menedżera ruchu. toodo tak, Szukaj w grupie zasobów lub wyszukiwanie nazwy hello hello profilu Menedżera ruchu z **wszystkie zasoby**.
2. Wybierz w okienku po lewej stronie powitania **punkty końcowe**, a następnie kliknij przycisk **Dodaj** tooadd punktu końcowego.

  ![Przycisk usługi Traffic Manager punkty końcowe "Dodaj"](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Na powitania **dodać punkt końcowy** bloku Utwórz punkt końcowy, wprowadzając hello następujących informacji:

  * **Typ**: Wybierz typ hello równoważenia tooload punktu końcowego. W tym scenariuszu wybierz **punktu końcowego platformy Azure** ponieważ połączono go toohello wystąpień bramy aplikacji, które zostały wcześniej skonfigurowane.
  * **Nazwa**: Wprowadź nazwę hello hello punktu końcowego.
  * **Typ zasobu docelowy**: Wybierz **publicznego adresu IP** , a następnie w obszarze **zasób docelowy**, wybierz hello publicznego adresu IP bramy aplikacji hello, który został wcześniej skonfigurowany.

   ![Blok "Dodaj punkt końcowy" Menedżera ruchu](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Teraz możesz przetestować konfigurację dostępu do niego hello DNS profilu usługi Traffic Manager (w tym przykładzie: TrafficManagerScenario.trafficmanager.net). Można ponownie wysłać żądania, wywołaj lub doprowadzić do maszyn wirtualnych i serwery sieci web, które zostały utworzone w różnych regionach i zmienić tootest ustawienia profilu usługi Traffic Manager hello konfigurację.

### <a name="step-4-create-a-load-balancer"></a>Krok 4: Tworzenie usługi równoważenia obciążenia

W tym scenariuszu usługi równoważenia obciążenia dystrybuuje połączeń z bazami danych toohello warstwy sieci web hello w ramach klastra o wysokiej dostępności.

Jeśli klaster wysokiej dostępności bazy danych używa funkcji AlwaysOn programu SQL Server, zapoznaj się zbyt[skonfigurować jeden lub więcej zawsze na dostępność odbiorniki grupy](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) instrukcje krok po kroku.

Aby uzyskać więcej informacji na temat konfigurowania wewnętrznego modułu równoważenia obciążenia, zobacz [utworzyć wewnętrznego modułu równoważenia obciążenia w portalu Azure hello](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij **nowy** > **sieci** > **modułu równoważenia obciążenia**.
2. Na powitania **modułu równoważenia obciążenia Utwórz** bloku, wybierz nazwę dla Twojej usługi równoważenia obciążenia.
3. Zestaw hello **typu** za**wewnętrzne**i wybierz odpowiednią sieć wirtualna hello i podsieć tooreside usługi równoważenia obciążenia hello w.
4. W obszarze **przypisywania adresów IP**, wybierz opcję **dynamiczne** lub **statycznych**.
5. W obszarze **grupy zasobów**, wybierz grupę zasobów powitania dla usługi równoważenia obciążenia hello.
6. W obszarze **lokalizacji**, wybierz odpowiedni region powitania dla usługi równoważenia obciążenia hello.
7. Kliknij przycisk **Utwórz** modułu równoważenia obciążenia hello toogenerate.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Połączenie usługi równoważenia obciążenia toohello warstwy wewnętrznej bazy danych

1. Z grupy zasobów Znajdź hello modułu równoważenia obciążenia, który został utworzony w poprzednich krokach hello.
2. W obszarze **ustawienia**, kliknij przycisk **pul zaplecza**, a następnie kliknij przycisk **Dodaj** tooadd puli zaplecza.

  ![Blok "Dodaj pulę zaplecza" moduł równoważenia obciążenia](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Na powitania **Dodaj pulę zaplecza** bloku, wprowadź nazwę hello hello puli zaplecza.
4. Dodaj poszczególnych maszyn lub puli zaplecza toohello zestawu dostępności.

#### <a name="configure-a-probe"></a>Skonfiguruj sondę

1. W moduł równoważenia obciążenia w obszarze **ustawienia**, wybierz pozycję **sondy**, a następnie kliknij przycisk **Dodaj** tooadd badanie.

 ![Blok "Dodaj sondy" moduł równoważenia obciążenia](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Na powitania **sondowania Dodaj** bloku, wprowadź nazwę hello hello sondy.
3. Wybierz hello **protokołu** hello sondy. Dla bazy danych może być sondowaniem TCP, a nie badania HTTP. toolearn więcej informacji na temat sondy modułu równoważenia obciążenia można znaleźć zbyt[sondy modułu równoważenia obciążenia omówienie](../load-balancer/load-balancer-custom-probe-overview.md).
4. Wprowadź hello **portu** z Twojej toobe bazy danych używane do uzyskiwania dostępu do badania hello.
5. W obszarze **interwał**, określ, jak często tooprobe hello aplikacji.
6. W obszarze **próg złej kondycji**, określ hello liczbę niepowodzeń sondy, ciągłe musi nastąpić toobe wirtualna zaplecza hello określana jako zła.
7. Kliknij przycisk **OK** toocreate hello sondowania.

#### <a name="configure-hello-load-balancing-rules"></a>Konfigurowanie reguł równoważenia obciążenia hello

1. W obszarze **ustawienia** moduł równoważenia obciążenia, wybierz **reguły równoważenia obciążenia**, a następnie kliknij przycisk **Dodaj** toocreate reguły.
2. Na powitania **reguły równoważenia obciążenia Dodaj** bloku, wprowadź hello **nazwa** hello reguły równoważenia obciążenia.
3. Wybierz hello **adresu IP frontonu** z hello usługi, w tym równoważenia obciążenia **protokołu**, i **portu**.
4. W obszarze **portu zaplecza**, określ hello toobe port używany w puli zaplecza hello.
5. Wybierz hello **puli zaplecza** i hello **sondowania** utworzonych hello poprzednie kroki tooapply hello reguły.
6. W obszarze **trwałości sesji**, wybierz sposób hello toopersist sesji.
7. W obszarze **limitów czasu bezczynności**, określ hello liczbę minut przed upływem limitu czasu bezczynności.
8. W obszarze **pływający adres IP**, wybierz opcję **wyłączone** lub **włączone**.
9. Kliknij przycisk **OK** toocreate hello reguły.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Krok 5: Łączenie warstwa sieci web usługi równoważenia obciążenia toohello dla maszyn wirtualnych

Teraz możemy skonfigurować hello IP adres usługi równoważenia obciążenia frontonu portu i w aplikacji hello, które są uruchomione na maszyny wirtualne warstwy sieci web dla połączeń bazy danych. Ta konfiguracja jest aplikacje określonych toohello, które działają na tych maszynach wirtualnych. tooconfigure hello docelowy adres IP i port, zapoznaj się z dokumentacją aplikacji toohello. adres IP hello toofind hello frontonie, hello portalu Azure Przejdź puli adresów IP frontonu toohello hello **ustawienia usługi równoważenia obciążenia** bloku.

![Okienko nawigacji "Adresu IP frontonu puli" moduł równoważenia obciążenia](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Następne kroki

* [Omówienie Menedżera ruchu](traffic-manager-overview.md)
* [Omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md)
* [Omówienie usługi Azure Load Balancer](../load-balancer/load-balancer-overview.md)
