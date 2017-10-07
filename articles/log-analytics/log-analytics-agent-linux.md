---
title: aaaConnect Twojego tooOperations komputery z systemem Linux Management Suite (OMS) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooconnect komputery z systemem Linux hostowanych w Azure, chmury lub tooOMS lokalnymi przy użyciu hello Agent pakietu OMS dla systemu Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Połącz z komputerów z systemem Linux tooOperations Management Suite (OMS) 

Z programu Microsoft Operations Management Suite (OMS), można zbierać i działają na danych generowanych przez komputery z systemem Linux i kontener rozwiązań, takich jak Docker znajdującej się w lokalnym centrum danych jako serwerów fizycznych lub maszynach wirtualnych, maszyny wirtualne w usługi hostowanych w chmurze, takiej jak Amazon Web Services (AWS) lub Microsoft Azure. Umożliwia także dostępne w OMS rozwiązania do zarządzania takich jak zmiana śledzenia zmian w konfiguracji tooidentify i tooproactively aktualizacje oprogramowania toomanage zarządzania aktualizacjami Zarządzanie cyklem życia hello sieci maszyn wirtualnych systemu Linux. 

Witaj Agent pakietu OMS dla systemu Linux komunikuje się wychodzące z hello usługę za pośrednictwem portu TCP 443 i hello komputer łączy toocommunicate tooa zapory lub serwera proxy serwera na powitania Internet, przejrzyj [Konfigurowanie hello agenta do użycia z serwera proxy HTTP serwera lub bramy OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand zmiany konfiguracji, należy zastosować toobe.  Jeśli monitorowanych hello komputerze z System Center 2016 - Operations Manager lub programu Operations Manager 2012 R2, mogą być wieloadresowego hello OMS usługi toocollect danych i usługi przesyłania dalej toohello i nadal być monitorowane przez program Operations Manager.  Komputery z systemem Linux monitorowane przez grupę zarządzania programu Operations Manager, który jest zintegrowany z usługą OMS nie mają konfiguracji dla źródła danych i do przodu zbieranych danych za pośrednictwem hello grupy zarządzania.  agent pakietu OMS Hello nie może być skonfigurowany tooreport toomore niż jeden obszar roboczy.  

Jeśli zasady zabezpieczeń IT nie zezwalają na toohello tooconnect Twojego sieci Internet komputerów, hello agenta może być skonfigurowany tooconnect toohello bramy OMS tooreceive konfiguracji informacji i wysyłania danych zebranych w zależności od rozwiązania hello, do których masz włączone. Aby uzyskać więcej informacji i kroki na tooconfigure Twojego toocommunicate OMS agenta systemu Linux za pośrednictwem bramy OMS toohello usługę, zobacz temat [połączyć tooOMS komputerów przy użyciu hello bramy OMS](log-analytics-oms-gateway.md).  

Witaj Poniższy diagram przedstawia połączenia hello hello zarządzane z wykorzystaniem agentów na komputerach systemu Linux i OMS, w tym kierunku hello i portów.

![Komunikacja agenta bezpośrednio z diagramu OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Wymagania systemowe
Przed rozpoczęciem należy przejrzeć następujące szczegóły tooverify spełnia wymagania wstępne hello hello.

### <a name="supported-linux-operating-systems"></a>Obsługiwane systemy operacyjne Linux
obsługiwane są oficjalnie powitania po dystrybucje systemu Linux.  Jednak hello Agent pakietu OMS dla systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 i 7 (x86/x64)
* Oracle Linux 5, 6 i 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 i 7 (x86/x64)
* Debian GNU/Linux 6, 7 i 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, LTS 16.04 (x86/x64)
* SUSE Linux Enterprise Server 11 i 12 (x86/x64)

### <a name="network"></a>Sieć
Hello informacje poniżej listy hello proxy i informacje o konfiguracji zapory wymagany w przypadku hello Linux toocommunicate agenta z usługą OMS. Ruch jest wychodzący z usługą OMS toohello sieci. 

|Zasób agenta| Porty |  
|------|---------|  
|*.ods.opinsights.azure.com | Port 443|   
|*.oms.opinsights.azure.com | Port 443|   
|*.blob.Core.Windows.NET/ | Port 443|   
|*.azure-automation.net | Port 443|  

### <a name="package-requirements"></a>Wymagania pakietu

 **Wymagany pakiet**   | **Opis**   | **Minimalna wersja**
--------------------- | --------------------- | -------------------
Glibc | Biblioteka C GNU   | 2.5-12 
Biblioteki Openssl | Biblioteki OpenSSL | 0.9.8e lub 1.0
Narzędzie curl | cURL klienta sieci web | 7.15.5
Ctypes języka Python | | 
PAM | Uwierzytelnianie podłączane moduły | 

> [!NOTE]
>  Rsyslog lub syslog ng są wymagane toocollect komunikaty dziennika systemowego. demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. toocollect syslog danych z tej wersji tych dystrybucji hello rsyslog demon powinien być zainstalowany i skonfigurowany tooreplace sysklog 

Hello agent zawiera kilka pakietów. Witaj wersji pliku zawiera następujące dostępnych przez uruchomione hello powłoki pakietu z pakietów hello `--extract`:

**Pakiet** | **Wersja** | **Opis**
----------- | ----------- | --------------
omsagent | 1.4.0 | Witaj Operations Management Suite agenta dla systemu Linux
omsconfig | 1.1.1 | Konfiguracja agenta dla hello Agent pakietu OMS
OMI | 1.2.0 | Otwórz infrastruktury zarządzania (OMI) - lightweight serwer modelu wspólnych informacji
scx | 1.6.3 | OMI CIM dostawców dla metryki wydajności systemu operacyjnego
Apache cimprov | 1.0.1 | Monitorowanie dostawcę dla OMI wydajności Apache HTTP Server. Zainstalowany w przypadku wykrycia Apache HTTP Server.
MySQL cimprov | 1.0.1 | Monitorowanie dostawcę dla OMI wydajności serwera MySQL. Zainstalowany w przypadku wykrycia MySQL/MariaDB serwera.
docker cimprov | 1.0.0 | Dostawca docker OMI. Zainstalowany w przypadku wykrycia Docker.

### <a name="compatibility-with-system-center-operations-manager"></a>Zgodność z programem System Center Operations Manager
Witaj Agent pakietu OMS dla systemu Linux udostępnia pliki binarne agenta hello agenta programu System Center Operations Manager. Jeśli zainstalujesz hello Agent pakietu OMS dla systemu Linux w systemie, w obecnie zarządzany przez program Operations Manager hello OMI i SCX pakietów na komputerze hello tooa nowszej wersji. W tej wersji, hello OMS i System Center 2016 - agentów programu Operations Manager/Operations Manager 2012 R2 dla systemu Linux są zgodne. 

> [!NOTE]
> System Center 2012 SP1 i wcześniejsze wersje obecnie nie są zgodne lub nie jest obsługiwany z hello Agent pakietu OMS dla systemu Linux.<br>
> Jeśli hello Agent pakietu OMS dla systemu Linux jest zainstalowana tooa komputer, który nie jest aktualnie monitorowane przez program Operations Manager, a następnie chcesz toomonitor hello komputera z programem Operations Manager, należy zmodyfikować hello [konfiguracji OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) uprzedniego toodiscovering hello komputera. **Ten krok jest *nie* niezbędny w przypadku hello agenta programu Operations Manager została zainstalowana przed hello Agent pakietu OMS dla systemu Linux.**

### <a name="system-configuration-changes"></a>Zmiany konfiguracji systemu
Po zainstalowaniu hello Agent pakietu OMS pakietów systemu Linux, hello następujące dodatkowe czynności konfiguracyjne systemowe zmiany zostaną zastosowane. Te artefakty muszą zostać usunięte po odinstalowaniu hello omsagent pakietu.

* Użytkownik bez uprawnień o nazwie: `omsagent` jest tworzony. To jest program hello konta hello omsagent demon działa jako.
* Plik "Dołącz" sudoers jest tworzony w /etc/sudoers.d/omsagent. To autoryzuje omsagent toorestart hello syslog i demonów omsagent. Jeśli dyrektywy "Dołącz" sudo nie są obsługiwane w wersji hello zainstalowany sudo, te wpisy są zapisywane zbyt/etc/sudoers.
* Konfiguracja syslog Hello jest zmodyfikowany tooforward podzbiór zdarzeń toohello agenta. Aby uzyskać więcej informacji, zobacz hello **Konfigurowanie zbierania danych** poniższej sekcji

### <a name="upgrade-from-a-previous-release"></a>Uaktualnianie z poprzedniej wersji
Uaktualnienie z wersji starszej niż 1.0.0-47 jest obsługiwane w tej wersji. Przeprowadzanie instalacji hello z hello `--upgrade` polecenia uaktualnia wszystkie składniki hello agenta toohello najnowszej wersji.

## <a name="installing-hello-agent"></a>Instalowanie agenta hello

W tej sekcji opisano, jak pakietami poszczególne składniki agenta hello hello tooinstall Agent pakietu OMS dla systemu Linux przy użyciu bunndle, który zawiera Debian i obr. / min.  Go zainstalować bezpośrednio lub wyodrębnione tooretrieve hello indywidualne pakiety.  

Najpierw należy OMS identyfikator i klucz, który można znaleźć przełączając toohello [klasycznego portalu OMS](https://mms.microsoft.com).  Na powitania **omówienie** stronę z hello górnego menu wybierz **ustawienia**, a następnie przejdź zbyt**połączone serwery Sources\Linux**.  Zobacz hello wartość toohello prawej **identyfikator obszaru roboczego** i **klucz podstawowy**.  Skopiuj i Wklej zarówno do Twojego ulubionego edytora.    

1. Witaj pobieranie najnowszych [Agent pakietu OMS Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) lub [Agent pakietu OMS Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) z usługi GitHub.  
2. Transfer hello odpowiedniego pakietu (x86 lub x64) tooyour komputer z systemem Linux przy użyciu protokołu scp/sftp.
3. Instalacja pakietu hello przy użyciu hello `--install` lub `--upgrade` argumentu. 

    > [!NOTE]
    > Jeśli wszystkie istniejące pakiety są instalowane, takich jak po hello agent programu System Center Operations Manager dla systemu Linux jest już zainstalowany, użyj hello `--upgrade` argumentu. tooconnect tooOperations Management Suite podczas instalacji, podaj hello `-w <WorkspaceID>` i `-s <Shared Key>` parametrów.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall i podłączone bezpośrednio
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>Pakiet agenta hello tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall i dołączyć tooa roboczym w chmurze dla instytucji rządowych nam
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Konfigurowanie agenta hello do użycia przy użyciu protokołu HTTP serwera proxy lub bramy OMS
Witaj Agent pakietu OMS dla systemu Linux obsługuje komunikacji przy użyciu protokołu HTTP lub HTTPS serwera proxy lub bramy OMS toohello usługę.  Zarówno w przypadku anonimowych, jak i podstawowe uwierzytelnianie (nazwy użytkownika i hasła) jest obsługiwane.  

### <a name="proxy-configuration"></a>Konfiguracja serwera proxy
Wartość konfiguracji serwera proxy Hello ma hello następującej składni:

`[protocol://][user:password@]proxyhost[:port]`

Właściwość|Opis
-|-
Protokół|http lub https
Użytkownika|Opcjonalna nazwa użytkownika dla uwierzytelniania serwera proxy
hasło|Opcjonalne hasło dla uwierzytelniania serwera proxy
proxyhost|Adres lub nazwę FQDN serwera proxy hello/OMS bramy
port|Numer portu opcjonalne dla serwera proxy hello/OMS bramy

Na przykład: `http://user01:password@proxy01.contoso.com:8080`

podczas instalacji lub modyfikując plik konfiguracji proxy.conf powitania po zakończeniu instalacji można określić powitania serwera proxy.   

### <a name="specify-proxy-configuration-during-installation"></a>Określ konfigurację serwera proxy podczas instalacji
Witaj `-p` lub `--proxy` argument dla pakietu instalacji omsagent hello określa toouse konfiguracji serwera proxy hello. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Definiowanie konfiguracji serwera proxy hello w pliku
Konfiguracja serwera proxy Hello można ustawić w plikach hello `/etc/opt/microsoft/omsagent/proxy.conf` i `/etc/opt/microsoft/omsagent/conf/proxy.conf `. pliki Hello można bezpośrednio utworzyć lub edytować, ale ich uprawnienia muszą być użytkownika omiuser hello toogrant zaktualizowane uprawnienie do odczytu w hello plików. Na przykład:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Usuwanie konfiguracji serwera proxy hello
tooremove konfiguracji serwera proxy w uprzednio zdefiniowanej i Przywróć łączność toodirect, usuń plik proxy.conf hello:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Dołączanie w usłudze Operations Management Suite
Jeśli klucz i identyfikator obszaru roboczego nie zostały podane podczas instalacji pakietu hello, hello agent musi być następnie zarejestrowany Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Przy użyciu wiersza polecenia hello dołączania
Uruchom polecenie omsadmin.sh hello, podając identyfikator obszaru roboczego hello i klucz obszaru roboczego. To polecenie musi uruchomić jako główny (z podniesienia uprawnień sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Przy użyciu pliku dołączania
1.  Utwórz plik hello `/etc/omsagent-onboard.conf`. Plik Hello musi być zdatny do odczytu i zapisu dla katalogu głównego.
`sudo vi /etc/omsagent-onboard.conf`
2.  Wstaw hello następujące wiersze w pliku hello identyfikator i klucz wstępny:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Uruchom następujące polecenie tooOnboard tooOMS hello:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Witaj, plik zostanie usunięty na pomyślnego dołączenia.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Włącz hello Agent pakietu OMS dla systemu Linux tooreport tooSystem Center Operations Manager
Wykonaj następujące kroki tooconfigure hello Agent pakietu OMS dla grupy zarządzania programu System Center Operations Manager Linux tooreport tooa hello.  

1. Edytuj plik hello`/etc/opt/omi/conf/omiserver.conf`
2. Upewnij się, że powitania od wiersza z **httpsport =** definiuje hello portu 1270. Takie jak:`httpsport=1270`
3. Uruchom ponownie serwer OMI hello:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Dzienniki agentów
Witaj dzienniki dla hello Agent pakietu OMS dla systemu Linux można znaleźć w: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello dzienniki dla hello omsconfig (konfiguracja agenta) programu można znaleźć w: `/var/opt/microsoft/omsconfig/log/` dzienniki dla składników OMI i SCX hello (udostępniających dane metryk wydajności) można znaleźć w folderze:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Dziennik obrotu konfiguracji ##
Hello dziennika obracania konfiguracji omsagent można znaleźć w folderze:`/etc/logrotate.d/omsagent-<workspace id>`

ustawienia domyślne Hello są: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Odinstalowywanie hello Agent pakietu OMS dla systemu Linux
Hello pakietów agenta można odinstalować pliku SH pakietu hello uruchomionych z hello `--purge` argumentu, który powoduje całkowite usunięcie hello agent i jego konfiguracja z hello komputera.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problem: Nie można tooconnect za pośrednictwem serwera proxy tooOMS

#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* proxy Hello określony podczas dołączania była nieprawidłowa
* punkty końcowe usługi OMS Hello nie są whitelistested w centrum danych. 

#### <a name="resolutions"></a>Rozwiązania
1. Reonboard toohello usługę z hello Agent pakietu OMS dla systemu Linux przy użyciu następującego polecenia z opcją hello hello `-v` włączone. Dzięki temu pełne dane wyjściowe agenta hello łączących się za pośrednictwem hello proxy toohello usługę. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Przejrzyj sekcję hello [Konfigurowanie hello agenta do użycia z serwera proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify zostały poprawnie skonfigurowane hello toocommunicate agenta za pośrednictwem serwera proxy.    
* Sprawdź, który hello następujących punktów końcowych usługi OMS są białej:

    |Zasób agenta| Porty |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Port 443|   
    |*.oms.opinsights.azure.com | Port 443|   
    |ods.systemcenteradvisor.com | Port 443|   
    |*.blob.Core.Windows.NET/ | Port 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problem: Komunikat o błędzie 403 podczas próby tooonboard

#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Data i godzina jest nieprawidłowa na serwerze z systemem Linux 
* Identyfikator i klucz obszaru roboczego, używane są nieprawidłowe

#### <a name="resolution"></a>Rozwiązanie

1. Sprawdź czas hello na serwerze Linux z datą polecenia hello. Jeśli czas hello +/-15 minut od bieżącego czasu dołączania kończy się niepowodzeniem. toocorrect tej aktualizacji hello datę i/lub strefy czasowej serwera z systemem Linux. 
2. Sprawdź, czy zainstalowano najnowszą wersję hello hello Agent pakietu OMS dla systemu Linux.  Najnowsza wersja Hello teraz powiadamia użytkownika, jeśli czas pochylenia powoduje błąd dołączania hello.
3. Reonboard przy użyciu poprawny identyfikator i klucz obszaru roboczego instrukcjami instalacji hello wcześniej w tym temacie.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problem: Widzisz 500 i 404 błąd w pliku dziennika hello bezpośrednio po dołączania
Jest to znany problem występujący podczas pierwszego przekazywania danych Linux pod obszarem roboczym pakietu OMS. Nie dotyczy to danych wysłanego lub usługa obsługi.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problem: Nie widać żadnych danych w portalu OMS hello

#### <a name="probable-causes"></a>Prawdopodobne przyczyny

- Toohello dołączania usługę nie powiodło się.
- Toohello połączenia, który jest zablokowany przez usługę OMS
- Agent pakietu OMS dla systemu Linux danych jest wykonywana kopia zapasowa

#### <a name="resolutions"></a>Rozwiązania
1. Sprawdź, czy hello dołączania usługę zakończyła się pomyślnie sprawdzając Jeśli hello następujący plik istnieje:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Przy użyciu hello Reonboard `omsadmin.sh` instrukcje wiersza polecenia
3. Jeśli przy użyciu serwera proxy, zobacz kroki rozwiązania proxy toohello wydanego wcześniej.
4. W niektórych przypadkach kiedy hello Agent pakietu OMS dla systemu Linux nie może skomunikować się z hello usługę, danych na agencie hello jest rozmiar buforu pełnej toohello umieszczonych w kolejce, czyli 50 MB. Witaj Agent pakietu OMS Linux powinien zostać uruchomiony ponownie, uruchamiając następujące polecenie hello: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Tego problemu w 1.1.0-28 wersję agenta i nowszych.
> 