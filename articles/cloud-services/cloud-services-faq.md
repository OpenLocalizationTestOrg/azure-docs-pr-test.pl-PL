---
title: "Role usługi w chmurze aaaAzure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi w chmurze Azure. Odpowiedzi na często zadawane pytania dotyczące certyfikatów, role sieci web i roli proces roboczy."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Cloud Services — często zadawane pytania
Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące usługi w chmurze Microsoft Azure. Możesz również odwiedzić hello [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083) ogólne informacje Azure cennik i pomocy technicznej. Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

## <a name="certificates"></a>Certyfikaty
### <a name="where-should-i-install-my-certificate"></a>Gdzie zainstalować certyfikatu?
* **Moje**  
  Aplikacja certyfikatu z kluczem prywatnym (\*PFX, \*.p12).
* **URZĄD CERTYFIKACJI**  
  Wszystkie certyfikaty pośrednie Przejdź w tym magazynie (zasad i podrzędne urzędy certyfikacji).
* **GŁÓWNY**  
  Witaj głównego urzędu certyfikacji sklepu, więc Twojego głównego certyfikatu urzędu certyfikacji należy tutaj wprowadzić.

### <a name="i-cant-remove-expired-certificate"></a>Nie można usunąć wygasłego certyfikatu
Azure uniemożliwia usunięcie certyfikatu, gdy jest używany. Należy tooeither usunięcie hello wdrożenia korzystającego z certyfikatu hello lub wdrożenia hello aktualizacji przy użyciu różnych lub odnowionego certyfikatu.

### <a name="delete-an-expired-certificate"></a>Usuwanie wygasłego certyfikatu
Tak długo, jak hello certyfikatu nie jest używany, można użyć hello [AzureCertificate Usuń](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove polecenia cmdlet programu PowerShell certyfikatu.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Wygasnąć certyfikatów o nazwie zarządzania usługą Windows Azure dla rozszerzeń
Te certyfikaty są tworzone w każdym przypadku, gdy rozszerzenie zostanie dodane usługi w chmurze toohello takich jak hello rozszerzenia usług pulpitu zdalnego. Te certyfikaty są używane tylko do szyfrowania i odszyfrowywania hello prywatna Konfiguracja rozszerzenia hello. Nie ma znaczenia, jeśli te certyfikaty wygaśnie. Data wygaśnięcia Hello nie jest zaznaczone.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Certyfikaty, usuwać I nadal wyświetlane.
Te ciągle pojawiają się prawdopodobnie z powodu narzędzia, którego używasz, takiego jak Visual Studio. Przy każdym ponownym połączeniu z narzędziem, które używa certyfikatu, konieczne będzie ponownie tooAzure przekazane.

### <a name="my-certificates-keep-disappearing"></a>Zachowaj zniknął certyfikatów
Podczas odtwarzania hello wystąpienie maszyny wirtualnej, wszystkie lokalne zmiany zostaną utracone. Użyj [zadanie uruchamiania](cloud-services-startup-tasks.md) maszyny wirtualnej toohello certyfikaty tooinstall każdej roli hello czasu uruchamiania.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Nie można znaleźć certyfikatów zarządzania w portalu hello
[Certyfikaty zarządzania](../azure-api-management-certs.md) są dostępne tylko w hello klasycznego portalu Azure. Witaj bieżącego portalu platformy Azure nie korzysta z certyfikatów zarządzania. 

### <a name="how-can-i-disable-a-management-certificate"></a>Jak wyłączyć certyfikatu zarządzania
[Certyfikaty zarządzania](../azure-api-management-certs.md) nie może zostać wyłączone. Należy usunąć je za pośrednictwem hello klasycznego portalu Azure, jeśli nie chcesz, aby je toobe już używać.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Jak utworzyć certyfikat SSL dla określonego adresu IP?
Postępuj zgodnie ze wskazówkami hello hello [utworzyć samouczek certyfikatu](cloud-services-certs-create.md). Użyj adresu IP hello, jak hello nazwy DNS.

## <a name="security"></a>Bezpieczeństwo
### <a name="disable-ssl-30"></a>Wyłączyć protokół SSL 3.0
toodisable protokołu SSL 3.0 i użycie zabezpieczeń TLS, Utwórz zadanie uruchamiania, który jest udokumentowany na ten wpis w blogu: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Dodaj **nosniff** tooyour witryny sieci Web
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

### <a name="customize-iis-for-a-web-role"></a>Dostosowywanie usług IIS dla roli sieci web
Użyj skryptu uruchamiania usług IIS hello z hello [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.

## <a name="scaling"></a>Skalowanie
### <a name="i-cannot-scale-beyond-x-instances"></a>Nie można skalować poza X wystąpień
Subskrypcji platformy Azure ma limit na powitania liczba rdzeni, których można użyć. Skalowanie nie będzie działać, jeśli zostały użyte wszystkie dostępne rdzenie hello. Na przykład jeśli istnieje limit liczby rdzeni (100), oznacza to, może mieć 100 wystąpień maszyna wirtualna A1 o rozmiarze dla usługi w chmurze lub wystąpieniu maszyny wirtualnej o rozmiarze 50 A2.

## <a name="networking"></a>Sieć
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>I nie można zastrzec adresu IP w usłudze chmury wielu wirtualnych adresów IP
Najpierw upewnij się, że to wystąpienie maszyny wirtualnej hello, który próbujesz tooreserve hello IP dla jest włączony. Po drugie upewnij się, wdrożeń odblokowane hello tymczasowych i produkcyjnych używasz zastrzeżonych adresów IP. **Nie** ustawień hello podczas uaktualniania jest hello wdrożenia.

## <a name="remote-desktop"></a>Pulpit zdalny
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Jak Pulpit zdalny gdy grupa NSG?
Dodaj toohello reguły NSG, które zezwalają na ruch na portach **3389** i **20000**.  Pulpit zdalny używa portu **3389**.  Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować tooconnect wystąpienia, które do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i Zezwalaj na powitania klienta toosend pliku cookie protokołu RDP i określ tooconnect poszczególnych wystąpień do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.
