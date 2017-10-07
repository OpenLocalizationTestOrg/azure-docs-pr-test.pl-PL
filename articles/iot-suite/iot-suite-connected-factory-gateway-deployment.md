---
title: "aaaDeploy pakietu IoT Azure połączenia bramy fabryki | Dokumentacja firmy Microsoft"
description: "Sposób toodeploy bramę Windows lub Linux toohello łączności tooenable połączenia fabryki wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Wdrożyć bramę Windows lub Linux hello połączone fabryki wstępnie rozwiązania

Witaj oprogramowania wymagane toodeploy w bramie hello połączone fabryki wstępnie skonfigurowane rozwiązanie zawiera dwa składniki:

* Witaj *OPC Proxy* ustanawia tooIoT połączenia koncentratora. Witaj *OPC Proxy* następnie czeka na polecenia i kontroli wiadomości z hello zintegrowane OPC przeglądarki, która jest uruchamiana w portalu rozwiązania połączonych fabryki hello.
* Witaj *wydawcy OPC* łączy tooexisting lokalnymi OPC UA serwery i przekazuje komunikaty telemetrii od nich tooIoT koncentratora.

Oba te składniki są open source i są dostępne jako źródło w serwisie GitHub i jak kontenery Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [Wydawca OPC][lnk-publisher-github] | [Wydawca OPC][lnk-publisher-docker] |
| [Serwer Proxy OPC][lnk-proxy-github] | [Serwer Proxy OPC][lnk-proxy-docker] |

Nie publicznych adresów IP, lub luk w zaporze bramy hello są wymagane dla obu składnika. Hello OPC serwera Proxy i wydawcy OPC używają tylko ruchu wychodzącego porty 443, 5671 i 8883.

Hello kroki opisane w tym artykule opisano sposób toodeploy a bramy przy użyciu rozwiązania Docker albo [Windows](#windows-deployment) lub [Linux](#linux-deployment). Brama Hello umożliwia łączność toohello połączone fabryki wstępnie skonfigurowane rozwiązanie.

> [!NOTE]
> oprogramowanie bramy Hello działającą w kontenerze Docker hello jest [Azure IoT krawędzi].

## <a name="windows-deployment"></a>Wdrażanie systemu Windows

> [!NOTE]
> Jeśli nie masz jeszcze urządzenie bramy, firma Microsoft zaleca się, że kupić komercyjnych bramy w jednym z naszych partnerów. Odwiedź hello [katalogu urządzenia Azure IoT] lista bramy urządzeń zgodnych z hello połączone fabryki rozwiązania. Postępuj zgodnie z instrukcjami hello z tooset urządzenia hello zapasowej hello bramy. Można również użyć hello następujące instrukcje toomanually ustawić jedną z istniejących bram.

### <a name="install-docker"></a>Zainstaluj Docker

Zainstaluj [Docker dla systemu Windows] na urządzenie bramy z systemem Windows. Podczas instalacji systemu Windows Docker wybrać dysk na tooshare maszyny z hosta z Docker. następujące zrzut ekranu przedstawia udostępniania hello D dysku w systemie Windows Hello:

![Zainstaluj Docker][img-install-docker]

Następnie utwórz folder o nazwie **docker** w katalogu głównym hello hello udostępnionego dysku.
Ten krok można również wykonać po zainstalowaniu docker z hello **ustawienia** menu.

### <a name="configure-hello-gateway"></a>Konfigurowanie bramy hello

1. Należy hello **iothubowner** parametry połączenia pakietu IoT Azure połączone wdrożenia bramy hello toocomplete wdrożenie fabryki. W hello [portalu Azure], przejdź tooyour Centrum IoT w grupie zasobów hello utworzone podczas wdrażania rozwiązania fabryki hello połączony. Kliknij przycisk **zasady dostępu współużytkowanego** tooaccess hello **iothubowner** ciąg połączenia:

    ![Znajdź hello parametry połączenia Centrum IoT][img-hub-connection]

    Kopiuj hello **parametry połączenia — klucz podstawowy** wartość.

1. Konfigurowanie bramy hello Centrum IoT, uruchamiając Witaj dwie bramy modułów **po** z wiersza polecenia, używając:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt; ** jest nazwa hello toogive tooyour OPC UA wydawcy w formacie hello **wydawcy.&lt; nazwę FQDN&gt;**. Na przykład, jeśli jest nazywany siecią fabryki **myfactorynetwork.com**, hello **ApplicationName** wartość jest **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt; ** jest hello **iothubowner** skopiowany w poprzednim kroku hello parametry połączenia. Ten ciąg połączenia jest używana tylko w tym kroku, nie będzie potrzebny w hello następujące kroki:

    Używasz hello mapowane D:\\docker folder (hello `-v` argument) nowsze toopersist Witaj dwie certyfikatów X.509, korzystających z modułów bramy hello.

### <a name="run-hello-gateway"></a>Uruchom hello bramy

1. Uruchom ponownie bramę hello przy użyciu następującego polecenia hello:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Ze względów bezpieczeństwa certyfikatów X.509 hello dwa utrwalone w hello D:\\docker folder zawiera hello klucza prywatnego. Ogranicz dostęp toothis folderu toohello poświadczeń (zazwyczaj **Administratorzy**) Użyj kontenera Docker hello toorun. Kliknij prawym przyciskiem myszy hello D:\\docker folderu, wybierz **właściwości**, następnie **zabezpieczeń**, a następnie **Edytuj**. Nadaj **Administratorzy** Pełna kontrola i usunąć inne osoby:

    ![Udziel uprawnień tooDocker udziału][img-docker-share]

1. Sprawdź łączność sieciową. W wierszu polecenia wprowadź polecenie hello `ping publisher.<your fully qualified domain name>` tooping bramy. Jeśli hello docelowy jest nieosiągalny, Dodaj adres IP hello i nazwę pliku hosts toohello bramy dla bramy. Witaj plik hosts znajduje się w hello **Windows\\System32\\sterowniki\\itp** folderu.

1. Następnie spróbuj wydawcą toohello tooconnect przy użyciu lokalnego klienta OPC UA uruchomionych na powitania bramy. Witaj OPC UA punkt końcowy adres URL jest `opc.tcp://publisher.<your fully qualified domain name>:62222`. Jeśli nie masz OPC Agent użytkownika klienta, możesz pobrać i użyć [open source OPC Agent użytkownika klienta].

1. Jeśli te testy lokalnego została ukończona pomyślnie, przejdziesz toohello **połączyć własny serwer UA OPC** w hello połączonych fabryki rozwiązanie portalu. Wprowadź adres URL punktu końcowego wydawcy hello (`tcp://publisher.<your fully qualified domain name>:62222`) i kliknij przycisk **Connect**. Zostanie wyświetlone ostrzeżenie, certyfikatu, a następnie kliknij **Kontynuuj.** Obok wystąpi błąd hello tego wydawcy nie ufaj hello Agent użytkownika klienta sieci Web. tooresolve ten błąd, hello kopiowania **Agent użytkownika klienta sieci Web** certyfikatu z hello **D:\\docker\\certyfikatów odrzucił\\certyfikaty** folderu toohello **D:\\docker\\aplikacji UA\\certyfikaty** folderu na powitania bramy. Nie trzeba toorestart hello bramy. Powtórz ten krok. Teraz możesz połączyć toohello bramy z chmury hello i są gotowe tooadd OPC UA serwerów toohello rozwiązania.

### <a name="add-your-opc-ua-servers"></a>Dodaj serwery OPC UA

1. Przeglądaj toohello **połączyć własny serwer UA OPC** w hello połączonych fabryki rozwiązanie portalu. Wykonaj te same czynności, jak w powyższej sekcji tooestablish hello zaufanie między hello połączonych fabryki portalu i hello serwera OPC UA powitalne. Ten krok pozwala ustanowić wzajemnego zaufania certyfikatów hello z hello połączony fabryki portalu i hello OPC UA serwera i tworzy połączenie.

1. Przeglądaj hello OPC UA węzły drzewa OPC UA serwera, kliknij prawym przyciskiem myszy hello OPC węzłów, a następnie wybierz **publikowania**. Dla publikacji toowork w ten sposób hello OPC UA serwera i wydawcy hello musi znajdować się na powitania tej samej sieci. Innymi słowy, jeśli hello w pełni kwalifikowana nazwa domeny wydawcy hello jest **publisher.mydomain.com** nazwę FQDN hello hello OPC UA serwer musi być, na przykład **myopcuaserver.mydomain.com**. Ustawienia są różne, należy ręcznie dodać węzły toohello publishesnodes.json pliku w hello **D:\\docker** folderu. Hello publishesnodes.json plik jest automatycznie generowany na powitania najpierw pomyślne publikowania OPC węzła.

1. Dane telemetryczne teraz wypływających z urządzeniem bramy hello. Można wyświetlić dane telemetryczne hello w hello **lokalizacje fabryki** widok portalu połączonych fabryki hello w obszarze **nowa fabryka**.

## <a name="linux-deployment"></a>Wdrożenie systemu Linux

> [!NOTE]
> Jeśli nie masz jeszcze urządzenie bramy, firma Microsoft zaleca się, że kupić komercyjnych bramy w jednym z naszych partnerów. Odwiedź hello [katalogu urządzenia Azure IoT] lista bramy urządzeń zgodnych z hello połączone fabryki rozwiązania. Postępuj zgodnie z instrukcjami hello z tooset urządzenia hello zapasowej hello bramy. Można również użyć hello następujące instrukcje toomanually ustawić jedną z istniejących bram.

[Zainstaluj Docker] na urządzeniu z systemem Linux bramy.

### <a name="configure-hello-gateway"></a>Konfigurowanie bramy hello

1. Należy hello **iothubowner** parametry połączenia pakietu IoT Azure połączone wdrożenia bramy hello toocomplete wdrożenie fabryki. W hello [portalu Azure], przejdź tooyour Centrum IoT w grupie zasobów hello utworzone podczas wdrażania rozwiązania fabryki hello połączony. Kliknij przycisk **zasady dostępu współużytkowanego** tooaccess hello **iothubowner** ciąg połączenia:

    ![Znajdź hello parametry połączenia Centrum IoT][img-hub-connection]

    Kopiuj hello **parametry połączenia — klucz podstawowy** wartość.

1. Konfigurowanie bramy hello Centrum IoT, uruchamiając Witaj dwie bramy modułów **po** z powłoki z:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt; ** jest nazwą hello hello OPC UA aplikacji hello bramy tworzy w formacie hello **wydawcy.&lt; nazwę FQDN&gt;**. Na przykład **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt; ** jest hello **iothubowner** skopiowany w poprzednim kroku hello parametry połączenia. Ten ciąg połączenia jest używana tylko w tym kroku, nie będzie potrzebny w hello następujące kroki:

    Użyj hello **/ shared** folder (hello `-v` argument) nowszego toopersist Witaj dwie certyfikatów X.509, korzystających z modułów bramy hello.

### <a name="run-hello-gateway"></a>Uruchom hello bramy

1. Uruchom ponownie bramę hello przy użyciu następującego polecenia hello:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Ze względów bezpieczeństwa certyfikatów X.509 hello dwa utrwalone w hello **/ shared** folder zawiera hello klucza prywatnego. Użyj toorun limit dostępu toothis folderu toohello poświadczenia hello kontenera Docker. tooset hello uprawnienia dla **głównego** , użyj hello `chmod` powłoki poleceń w folderze hello.

1. Sprawdź łączność sieciową. Z powłoki, wprowadź polecenie hello `ping publisher.<your fully qualified domain name>` tooping bramy. Jeśli hello docelowy jest nieosiągalny, Dodaj adres IP hello i nazwę pliku hosts tooyour bramy dla bramy. Witaj plik hosts znajduje się w hello **/itp** folderu.

1. Następnie spróbuj wydawcą toohello tooconnect przy użyciu lokalnego klienta OPC UA uruchomionych na powitania bramy. Witaj OPC UA punkt końcowy adres URL jest `opc.tcp://publisher.<your fully qualified domain name>:62222`. Jeśli nie masz OPC Agent użytkownika klienta, możesz pobrać i użyć [open source OPC Agent użytkownika klienta].

1. Jeśli te testy lokalnego została ukończona pomyślnie, przejdziesz toohello **połączyć własny serwer UA OPC** w hello połączonych fabryki rozwiązanie portalu. Wprowadź adres URL punktu końcowego wydawcy hello (`tcp://publisher.<your fully qualified domain name>:62222`) i kliknij przycisk **Connect**. Zostanie wyświetlone ostrzeżenie, certyfikatu, a następnie kliknij **Kontynuuj.** Obok wystąpi błąd hello tego wydawcy nie ufaj hello Agent użytkownika klienta sieci Web. tooresolve ten błąd, hello kopiowania **Agent użytkownika klienta sieci Web** certyfikatu z hello **/udostępnione/odrzucone certyfikatów/certyfikaty** toohello folderu **/shared/UA aplikacji/certyfikaty** folder na powitania bramy. Nie trzeba toorestart hello bramy. Powtórz ten krok. Teraz możesz połączyć toohello bramy z chmury hello i są gotowe tooadd OPC UA serwerów toohello rozwiązania.

### <a name="add-your-opc-ua-servers"></a>Dodaj serwery OPC UA

1. Przeglądaj toohello **połączyć własny serwer UA OPC** w hello połączonych fabryki rozwiązanie portalu. Wykonaj te same czynności, jak w powyższej sekcji tooestablish hello zaufanie między hello połączonych fabryki portalu i hello serwera OPC UA powitalne. Ten krok pozwala ustanowić wzajemnego zaufania certyfikatów hello z hello połączony fabryki portalu i hello OPC UA serwera i tworzy połączenie.

1. Przeglądaj hello OPC UA węzły drzewa OPC UA serwera, kliknij prawym przyciskiem myszy hello OPC węzłów, a następnie wybierz **publikowania**. Dla publikacji toowork w ten sposób hello OPC UA serwera i wydawcy hello musi znajdować się na powitania tej samej sieci. Innymi słowy, jeśli hello w pełni kwalifikowana nazwa domeny wydawcy hello jest **publisher.mydomain.com** nazwę FQDN hello hello OPC UA serwer musi być, na przykład **myopcuaserver.mydomain.com**. Ustawienia są różne, należy ręcznie dodać węzły toohello publishesnodes.json pliku w hello **/ shared** folderu. Hello publishesnodes.json jest generowana automatycznie na powitania najpierw pomyślne publikowania OPC węzła.

1. Dane telemetryczne teraz wypływających z urządzeniem bramy hello. Można wyświetlić dane telemetryczne hello w hello **lokalizacje fabryki** widok portalu połączonych fabryki hello w obszarze **nowa fabryka**.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat architektury hello fabryki połączonych hello wstępnie skonfigurowane rozwiązanie, zobacz [połączonych fabryki wstępnie skonfigurowane rozwiązanie wskazówki][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker dla systemu Windows]: https://www.docker.com/docker-windows
[Wykaz urządzenia IoT Azure]: https://catalog.azureiotsuite.com/?q=opc
[Witryna Azure Portal]: http://portal.azure.com/
[open source OPC Agent użytkownika klienta]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Zainstaluj Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy