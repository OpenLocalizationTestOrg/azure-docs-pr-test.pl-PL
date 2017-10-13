---
title: Dystrybucje systemu Linux zatwierdzone | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat systemu Linux na dystrybucje zatwierdzone na platformie Azure, łącznie z wytycznymi Ubuntu, CentOS, Oracle i SUSE."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 39cb2464eb593a29c4436afb5c14419b704ebff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux na dystrybucje zatwierdzone przez platformę Azure
Partnerzy Podaj Linux obrazów w portalu Azure Marketplace. Pracujemy nad różne społeczności Linux można dodać więcej odmian do listy dystrybucyjnej zatwierdzone. Tymczasem dystrybucji, które nie są dostępne z poziomu portalu Marketplace, zawsze przełączeniem własne Linux przez zgodnie z wytycznymi na [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Obsługiwane dystrybucje i wersje
W poniższej tabeli wymieniono dystrybucje systemu Linux i wersje, które są obsługiwane na platformie Azure. Zapoznaj się [obrazy obsługę systemu Linux w programie Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) więcej szczegółowych informacji.

Sterowniki usługi integracji systemu Linux (LIS) dla funkcji Hyper-V i platformy Azure są moduły jądra, które Microsoft przyczynia się bezpośrednio do nadrzędnego jądra systemu Linux.  Niektóre sterowniki LIS są wbudowane w jądra dystrybucji domyślnie. Starsze dystrybucji, które są oparte na Red Hat Enterprise (RHEL) / CentOS są dostępne jako osobny plik do pobrania na [Linux Integration Services wersji 4.1 dla funkcji Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Zobacz [wymagania jądra systemu Linux](create-upload-generic.md#linux-kernel-requirements) Aby uzyskać więcej informacji o sterownikach LIS.

Agent systemu Linux Azure została już wcześniej zainstalowana na obrazów Azure Marketplace i są zwykle dostępne z repozytorium pakietów dystrybucji. Kod źródłowy znajduje się na [GitHub](https://github.com/azure/walinuxagent).

| Dystrybucja | Wersja | Sterowniki | Agent |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3 + 7.0 + |CentOS 6.3: [Pobierz LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +: W przypadku jądra |Pakiecie: [repozytorium](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |Jądra |Kod źródłowy: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7,9 +, 8.2 + |Jądra |Pakiet: W repozytorium w obszarze "agenta waagent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |Jądra |Pakiet: W repozytorium w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7 + 7.1 + |Jądra |Pakiet: W repozytorium w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES dla SAP<br>11 Z DODATKIEM SP4<br>Z DODATKIEM SP1 12 +|Jądra |Pakiet:<p> 11 WE [chmury: narzędzia](https://build.opensuse.org/project/show/Cloud:Tools) repozytorium<br>dla 12 zawarte w Module "Chmura publiczna" w obszarze "python-azure-agent"<br/>Kod źródłowy: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE przestępnego 42.1 + |Jądra |Pakiecie: [chmury: narzędzia](https://build.opensuse.org/project/show/Cloud:Tools) repozytorium, w obszarze "python-azure-agent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |Jądra |Pakiet: W repozytorium w obszarze "walinuxagent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Partnerzy

### <a name="coreos"></a>CoreOS
[https://CoreOS.com/docs/running-CoreOS/cloud-Providers/Azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Z witryny sieci Web CoreOS:

*CoreOS zaprojektowano pod kątem bezpieczeństwa, zgodności i niezawodności. Zamiast instalowania pakietów za pomocą yum lub stanie, CoreOS używa kontenerów Linux do zarządzania usługami na wyższym poziomie abstrakcji. Kod pojedynczą usługę i wszystkie zależności są umieszczane w kontenerze, który można uruchomić na jednym lub wielu komputerach CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-Microsoft-Azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ jest niezależne konsultacji i usług firmy, która specjalizuje się w projektowania i wdrażania rozwiązań professional przy użyciu bezpłatnego oprogramowania. Jako początkowych specjalistów open source Credativ ma międzynarodowego uznania z wielu działów IT korzystających z pomocy technicznej. W połączeniu z firmą Microsoft Credativ obecnie przygotowuje odpowiednie obrazy Debian Debian 8 (Joasia) oraz Debian przed 7 (Wheezy). Oba obrazy są specjalnie zaprojektowane do uruchamiania na platformie Azure, można łatwo zarządzać za pomocą platformy. Credativ będzie obsługiwać także długotrwałe utrzymanie i aktualizowanie Debian obrazów na platformie Azure za pośrednictwem jego centrach obsługi technicznej źródłowym Otwórz.

### <a name="oracle"></a>Oracle
[http://www.Oracle.com/technetwork/topics/cloud/FAQ-1963009.HTML](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Strategia programu Oracle polega na oferuje szeroką gamę rozwiązań dla chmur prywatnych i publicznych. Strategia zapewnia klientom wybór i elastyczność w sposób wdrażania oprogramowania Oracle w chmurach programu Oracle i innych chmur. Partnerstwo w zakresie programu Oracle z firmą Microsoft umożliwia klientom wdrożenia oprogramowania Oracle w chmur prywatnych i publicznych bez obaw certyfikacji firmy Microsoft i pomocy technicznej z programu Oracle.  Zobowiązań programu Oracle i inwestycji w rozwiązaniach chmury publicznej i prywatnej Oracle nie ulega zmianie.

### <a name="red-hat"></a>Red Hat
[http://www.RedHat.com/en/partners/Strategic-Alliance/Microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Na świecie głównym dostawcą rozwiązań typu open source, Red Hat pomaga ponad 90% firm listy Fortune 500 rozwiązać problemy biznesowe, Dopasuj informatyczne i strategii biznesowej oraz przygotowanie w przyszłości technologii. Red Hat robi to przez zapewnienie bezpiecznych rozwiązań za pomocą modelu biznesowego otwarte i ekonomiczny, przewidywalnych subskrypcji.

### <a name="suse"></a>SUSE
[http://www.SUSE.com/SUSE-Linux-Enterprise-Server-on-Azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server na platformie Azure to platforma sprawdzone, która zapewnia lepszą niezawodność i zabezpieczeń dla chmury obliczeniowej. Elastyczne platformy Linux w systemie SUSE bezproblemowo integruje się z usług w chmurze Azure do środowiska chmury można łatwo zarządzać dostarczania. Z więcej niż 9,200 certyfikowanych aplikacji z ponad 1800 niezależnym dostawcom oprogramowania dla systemu SUSE Linux Enterprise Server SUSE gwarantuje, że obciążeń działających w obsługiwanych w centrum danych można bez obaw wdrożyć na platformie Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/Azure](http://www.ubuntu.com/cloud/azure)

Canonical inżynieryjne i otwórz społeczności ładu dysków Powodzenie Ubuntu przez klienta, serwera i przetwarzania w chmurze, która obejmuje usługi w chmurze osobistej dla konsumentów. Canonical firmy wizję ujednolicone, bezpłatna platforma w Ubuntu, z telefonu do chmury, zawiera rodziny spójnego interfejsów dla telefonu, tablecie, TV i pulpitu. Wizja sprawia, że Ubuntu pierwszy wybór dla różnych instytucji od dostawców chmury publicznej do osoby podejmujące decyzje Electronics konsumenta i Ulubione między poszczególnych technologists.

Canonical deweloperzy i engineering centrach na całym świecie, unikatowo znajduje się do współpracy z sprzętu osoby podejmujące decyzje, dostawców zawartości i deweloperów oprogramowania Przesuń Ubuntu rozwiązań na rynku dla komputerów, serwerów i urządzeń przenośnych.
