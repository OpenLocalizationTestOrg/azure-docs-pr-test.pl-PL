---
title: "Role usługi w chmurze Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a>Cloud Services — często zadawane pytania
Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące usługi w chmurze Microsoft Azure. Możesz również odwiedzić [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083) ogólne informacje Azure cennik i pomocy technicznej. Można również znaleźć [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

## <a name="certificates"></a>Certyfikaty
### <a name="where-should-i-install-my-certificate"></a>Gdzie zainstalować certyfikatu?
* **Moje**  
  Aplikacja certyfikatu z kluczem prywatnym (\*PFX, \*.p12).
* **URZĄD CERTYFIKACJI**  
  Wszystkie certyfikaty pośrednie Przejdź w tym magazynie (zasad i podrzędne urzędy certyfikacji).
* **GŁÓWNY**  
  Główny urząd certyfikacji sklepu, więc Twojego głównego certyfikatu urzędu certyfikacji należy tutaj wprowadzić.

### <a name="i-cant-remove-expired-certificate"></a>Nie można usunąć wygasłego certyfikatu
Azure uniemożliwia usunięcie certyfikatu, gdy jest używany. Należy usunąć wdrożenia, który używa certyfikatu lub aktualizuje wdrożenie przy użyciu różnych lub odnowionego certyfikatu.

### <a name="delete-an-expired-certificate"></a>Usuwanie wygasłego certyfikatu
Tak długo, jak certyfikat nie jest używany, można użyć [AzureCertificate Usuń](https://msdn.microsoft.com/library/azure/mt589145.aspx) polecenia cmdlet programu PowerShell, aby usunąć certyfikatu.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Wygasnąć certyfikatów o nazwie zarządzania usługą Windows Azure dla rozszerzeń
Te certyfikaty są tworzone w każdym przypadku, gdy rozszerzenie zostanie dodane do usługi w chmurze np. rozszerzenia usług pulpitu zdalnego. Te certyfikaty są używane tylko do szyfrowania i odszyfrowywania prywatna Konfiguracja rozszerzenia. Nie ma znaczenia, jeśli te certyfikaty wygaśnie. Data wygaśnięcia nie jest zaznaczone.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Certyfikaty, usuwać I nadal wyświetlane.
Te ciągle pojawiają się prawdopodobnie z powodu narzędzia, którego używasz, takiego jak Visual Studio. Przy każdym ponownym połączeniu z narzędziem, które używa certyfikatu, ponownie zostanie przekazany do platformy Azure.

### <a name="my-certificates-keep-disappearing"></a>Zachowaj zniknął certyfikatów
Gdy wystąpienie maszyny wirtualnej jest odtwarzany, wszystkie lokalne zmiany zostaną utracone. Użyj [zadanie uruchamiania](cloud-services-startup-tasks.md) instalowanie certyfikatów do maszyny wirtualnej w każdym uruchomieniu roli.

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a>Nie można znaleźć w portalu certyfikatów zarządzania
[Certyfikaty zarządzania](../azure-api-management-certs.md) są dostępne tylko w klasycznym portalu Azure. Bieżącego portalu platformy Azure nie korzysta z certyfikatów zarządzania. 

### <a name="how-can-i-disable-a-management-certificate"></a>Jak wyłączyć certyfikatu zarządzania
[Certyfikaty zarządzania](../azure-api-management-certs.md) nie może zostać wyłączone. Należy usunąć je za pośrednictwem klasycznego portalu Azure, jeśli nie chcesz, aby go już używać.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Jak utworzyć certyfikat SSL dla określonego adresu IP?
Postępuj zgodnie z instrukcjami w [utworzyć samouczek certyfikatu](cloud-services-certs-create.md). Użyj adresu IP z nazwą DNS.

## <a name="security"></a>Bezpieczeństwo
### <a name="disable-ssl-30"></a>Wyłączyć protokół SSL 3.0
Aby wyłączyć protokół SSL 3.0 i korzystanie z zabezpieczeń TLS, należy utworzyć zadanie uruchamiania, który jest udokumentowany na ten wpis w blogu: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-to-your-website"></a>Dodaj **nosniff** do witryny sieci Web
Aby uniemożliwić klientom wykrywanie typów MIME, Dodaj ustawienie w Twojej *web.config* pliku.

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

Można również dodać to ustawienie w usługach IIS. Użyj następującego polecenia z [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>Dostosowywanie usług IIS dla roli sieci web
Użyj skryptu uruchamiania usług IIS z [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.

## <a name="scaling"></a>Skalowanie
### <a name="i-cannot-scale-beyond-x-instances"></a>Nie można skalować poza X wystąpień
Subskrypcji platformy Azure ma limit liczby rdzeni, których można użyć. Skalowanie nie będzie działać, jeśli zostały użyte wszystkie dostępne rdzenie. Na przykład jeśli istnieje limit liczby rdzeni (100), oznacza to, może mieć 100 wystąpień maszyna wirtualna A1 o rozmiarze dla usługi w chmurze lub wystąpieniu maszyny wirtualnej o rozmiarze 50 A2.

## <a name="networking"></a>Sieć
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>I nie można zastrzec adresu IP w usłudze chmury wielu wirtualnych adresów IP
Najpierw upewnij się, że wystąpienie maszyny wirtualnej, który próbujesz zastrzec adresu IP dla jest włączona. Po drugie upewnij się, że używasz zastrzeżonych adresów IP dla odblokowane wdrożeń tymczasowych i produkcyjnych. **Nie** zmiany ustawień podczas uaktualniania jest wdrożenie.

## <a name="remote-desktop"></a>Pulpit zdalny
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Jak Pulpit zdalny gdy grupa NSG?
Dodaj reguły do grupy NSG, które zezwalają na ruch na portach **3389** i **20000**.  Pulpit zdalny używa portu **3389**.  Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować którego wystąpienia, aby nawiązać połączenie.  *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i umożliwić klientom wysyłanie plików cookie protokołu RDP i określ poszczególne wystąpienia do nawiązania połączenia.  *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.
