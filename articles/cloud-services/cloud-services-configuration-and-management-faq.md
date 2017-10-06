---
title: "Zarządzanie i aaaConfiguration problemy dotyczące Microsoft Azure Cloud Services często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono hello często zadawane pytania dotyczące konfiguracji i zarządzania dla usługi w chmurze Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Konfigurowanie i zarządzanie problemy dotyczące usług Azure Cloud Services: często zadawane pytania (FAQ)

Ten artykuł zawiera często zadawane pytania dotyczące problemów dotyczących konfiguracji i zarządzania dla [usługi w chmurze Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Jak dodać "nosniff" toomy witryny sieci Web?
tooprevent klientom wykrywanie typy MIME hello, Dodaj ustawienie w Twojej *web.config* pliku.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

Można również dodać to ustawienie w usługach IIS. Użyj hello następujące polecenie z hello [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Jak dostosować usług IIS dla roli sieci web?
Użyj skryptu uruchamiania usług IIS hello z hello [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.

## <a name="i-cannot-scale-beyond-x-instances"></a>Nie można skalować poza X wystąpień
Subskrypcji platformy Azure ma limit na powitania liczba rdzeni, których można użyć. Skalowanie nie będzie działać, jeśli zostały użyte wszystkie dostępne rdzenie hello. Na przykład jeśli istnieje limit liczby rdzeni (100), oznacza to, może mieć 100 wystąpień maszyna wirtualna A1 o rozmiarze dla usługi w chmurze lub wystąpieniu maszyny wirtualnej o rozmiarze 50 A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Jak wdrożyć dostępu opartej na rolach dla usługi w chmurze?
Usługi w chmurze nie obsługuje hello model kontroli dostępu opartej na rolach (RBAC), ponieważ nie jest usługa Azure Resource Manager na podstawie.

Zobacz [Azure RBAC, a administratorzy subskrypcji klasycznego](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Jak ustawić limit czasu bezczynności powitania dla usługi równoważenia obciążenia Azure?
Hello limitu czasu można określić w pliku definicji (csdef) usługi następująco:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Zobacz [nowy: można skonfigurować limit czasu bezczynności dla usługi równoważenia obciążenia Azure](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) Aby uzyskać więcej informacji.

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Można wewnętrzny pracownicy firmy Microsoft wystąpień usługi toocloud RDP bez uprawnienia?
Następujące firmy Microsoft, które strict procesu, który nie zezwala na wewnętrzny całego tooRDP do usługi w chmurze bez pisemnej zgody (adres e-mail lub innych pisemnej) z właścicielem hello lub ich osobę przez wyznaczoną.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Łańcuch certyfikatów hello certyfikatu SSL usługi chmury jest niekompletna
Firma Microsoft zaleca klientom zainstalowanie hello łańcucha certyfikatów Pełna (certyfikatu liścia, certyfikaty pośrednich i certyfikatu głównego) zamiast tylko hello liścia certyfikatu. Po zainstalowaniu właśnie certyfikatu liścia hello użytkownik korzysta z łańcucha certyfikatów hello toobuild Windows przez krótki hello listy CTL. Jeśli sieci sporadyczne problemy lub usługą DNS wystąpić w Azure lub usługi Windows Update, gdy Windows próbuje toovalidate hello certyfikatu, hello certyfikatu może być uznawane za nieprawidłowe. Instalując hello łańcucha certyfikatów pełne, można uniknąć tego problemu. Witaj blogu w [jak tooinstall łańcuchowa certyfikat SSL](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) przedstawia sposób toodo to.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Jak skojarzyć statycznego usługi w chmurze toomy adres IP?
tooset statycznych adresów IP, należy toocreate zastrzeżonego adresu IP. Ten zastrzeżony adres IP może być skojarzony tooa nowe chmury usługi lub tooan istniejącego wdrożenia. Zobacz powitania po dokumentów, aby uzyskać szczegółowe informacje:
* [Jak toocreate zastrzeżonego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Zarezerwowania adresu IP hello istniejącą usługę w chmurze](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Skojarzyć zastrzeżonego adresu IP tooa nową usługę w chmurze](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Skojarzyć zastrzeżonego tooa IP uruchamiania wdrożenia](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Skojarzyć zastrzeżonego adresu IP tooa usługą w chmurze przy użyciu pliku konfiguracji usługi](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Co to jest hello limit przydziału dla usługi w chmurze?
Zobacz [ogranicza specyficzne dla usługi](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Dlaczego dysk hello na Moje maszyny Wirtualnej usługi chmury Wyświetla bardzo mało wolnego miejsca na dysku?
Jest to oczekiwane zachowanie, a nie powinny powodować dowolnej aplikacji tooyour problem. Rejestrowanie jest włączone dla dysku % w maszynach wirtualnych PaaS platformy Azure, która wykorzystuje zasadniczo double hello ilość miejsca na pliki zwykle zajmują uproot hello %. Jednak istnieje kilka sposobów toobe pamiętać, że zasadniczo włączenie tej funkcji do innych niż problem.

Witaj rozmiar dysku % approot % jest obliczany jako wartość < rozmiar cspkg + rozmiar maksymalny dziennika > + margines wolnego miejsca lub 1,5 GB w zależności od jest większy. Witaj rozmiar maszyny Wirtualnej nie ma żadnego wpływu na tego obliczenia. (hello rozmiar maszyny Wirtualnej wpływa tylko na powitania rozmiar dysku C: tymczasowe hello.) 

Jest nieobsługiwany toowrite toohello % approot % dysku. Jeśli piszesz toohello maszyny Wirtualnej platformy Azure, należy to zrobić w tymczasowej zasobów LocalStorage (lub innych opcji, takie jak magazyn obiektów Blob, plików Azure itp.). Dlatego hello ilość wolnego miejsca w folderze % approot % hello nie ma sensu. Jeśli nie masz pewności, czy aplikacja jest pisanie toohello % approot % dysku, możesz pozwolić zawsze usługi Uruchom kilka dni, a następnie porównaj hello "przed" i "after" rozmiary. 

Azure nie zapisze żadnych toohello % approot % dysku. Hello wirtualnego dysku twardego jest utworzone na podstawie Twojej cspkg i instalowany w hello maszyny Wirtualnej platformy Azure, hello jedynym elementem, który może zapisać toothis dysku po aplikacji. 

Ustawienia dziennika Hello są niemożliwą do skonfigurowania, więc nie można wyłączyć go.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Co to są hello funkcje i możliwości dostępnych adresów IP/identyfikatorów Azure podstawowe i przed atakami DDOS?
Platforma Azure ma adresów IP/identyfikatorów w centrum danych serwerów fizycznych toodefend przed zagrożeniami. Ponadto klienci mogą wdrożyć rozwiązania innych firm zabezpieczeń, takie jak zapory aplikacji sieci web, zapory sieciowe ochrony przed złośliwym kodem, wykrywania nieautoryzowanego dostępu, systemów zapobiegania (Identyfikatory/IP) i więcej. Aby uzyskać więcej informacji, zobacz [ochrony danych i zasobów i być zgodne ze standardami zabezpieczeń globalnych](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft stale monitoruje zagrożenia toodetect serwerów, sieci i aplikacji. Podejście multipronged zarządzanie zagrożeniami Azure używa wykrywania nieautoryzowanego dostępu, rozproszonej odmowa usługi (DDoS) ataki zapobiegania, penetracji testowania, analizy behawioralnej, wykrywanie anomalii i uczenia maszynowego tooconstantly zwiększenia poziomu jej obrony i ograniczenia ryzyka. Antimalware Microsoft Azure chroni usług w chmurze Azure i maszyn wirtualnych. Masz rozwiązań innych firm zabezpieczeń toodeploy opcji hello z dodatkowo, takich jak okno zapory aplikacji sieci web, zapory sieciowe, ochrony przed złośliwym oprogramowaniem i nieautoryzowanego dostępu i zapobiegania systemów (Identyfikatory/adresów IP).

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Dlaczego IIS zatrzymać zapisywania katalogu dziennika toohello?
Wykorzystał hello przydziału magazynu lokalnego zapisywania katalogu dziennika toohello. Aby rozwiązać ten problem, wykonaj jedno z trzech zdarzeń:
* Włącz diagnostykę dla usług IIS i diagnostyki hello okresowo przeniesione tooblob magazynu.
* Ręcznie usuń pliki dziennika z hello katalog rejestrowania.
* Zwiększ limit przydziału dla zasobów lokalnych.

Aby uzyskać więcej informacji zobacz hello w następujących dokumentach:
* [Przechowywanie i przeglądanie danych diagnostycznych w usłudze Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
* [Dzienniki programu IIS zatrzymuje zapisu w usłudze w chmurze](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Co to jest celem hello hello "Rozszerzeń systemu Windows Azure Tools szyfrowania certyfikatu dla"?
Te certyfikaty są tworzone automatycznie zawsze, gdy rozszerzenie zostanie dodane toohello usługi w chmurze. Najczęściej jest hello rozszerzenia WAD lub hello rozszerzenia protokołu RDP, ale może to być inne, takie jak hello rozszerzenie ochrony przed złośliwym oprogramowaniem lub moduł zbierający dzienniki. Te certyfikaty są używane tylko do szyfrowania i odszyfrowywania hello prywatna Konfiguracja rozszerzenia hello. Data wygaśnięcia Hello nigdy nie jest zaznaczone, przez co nie ma znaczenia, jeśli hello certyfikat wygasł. 

Te certyfikaty, można zignorować. Aby wyczyścić hello certyfikatów, możesz spróbować usuwając je wszystkie. Azure zgłosi błąd przy próbie toodelete certyfikatu, który jest używany.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Sposób generowania certyfikatu żądania Podpisania bez "Używać protokołu RDP" w wystąpieniu toohello
Zobacz hello następujących wytycznych:

>[Uzyskiwanie certyfikatu do użytku z systemem Windows Azure witryn sieci Web (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Należy pamiętać, że CSR jest tylko plik tekstowy. Nie ma toobe utworzony z maszyny hello gdzie certyfikat hello ostatecznie będzie używany. Chociaż ten dokument jest przeznaczony dla usług aplikacji, hello tworzenia CSR jest rodzajowy i ma zastosowanie również do usługi w chmurze.
