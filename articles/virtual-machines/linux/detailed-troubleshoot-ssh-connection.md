---
title: "aaaDetailed SSH dotyczące rozwiązywania problemów w maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Szczegółowe kroki rozwiązywania problemów dotyczących problemów łączenie tooan maszyny wirtualnej platformy Azure SSH"
keywords: "SSH połączenia zostało odrzucone, ssh błędu, platforma azure ssh, połączenia SSH nie powiodło się"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>SSH szczegółowe kroki rozwiązywania problemów dotyczących problemów łączenie tooa maszyny Wirtualnej systemu Linux na platformie Azure
Istnieje wiele możliwych przyczyn tego powitania klienta SSH mogą nie być możliwe tooreach hello SSH usługi na powitania maszyny Wirtualnej. Jeśli wykonano za pomocą hello więcej [SSH ogólne kroki rozwiązywania problemów](troubleshoot-ssh-connection.md), należy toofurther rozwiązać problem z połączeniem hello. W tym artykule przedstawiono szczegółowe toodetermine kroki rozwiązywania problemów w przypadku, gdy kończy się niepowodzeniem hello połączenia SSH i w jaki sposób tooresolve go.

## <a name="take-preliminary-steps"></a>Czynności wstępne
Witaj poniższym diagramie przedstawiono składniki hello, które nie są związane.

![Diagram pokazujący składniki usługi SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Witaj Poniższe etapy ułatwiają odizolowania hello źródła błędu hello i ustalić rozwiązania lub obejścia.

1. Sprawdź stan hello hello maszyny Wirtualnej w portalu hello.
   W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **maszyn wirtualnych** > *nazwę maszyny Wirtualnej*.

   Witaj stan okienka hello maszyny Wirtualnej powinny być widoczne **systemem**. Przewiń w dół tooshow ostatniej aktywności dla zasobów obliczeniowych, magazynu i zasobów sieciowych.

2. Wybierz **ustawienia** tooexamine punkty końcowe, adresy IP, grup zabezpieczeń sieci i innych ustawień.

   Witaj maszyny Wirtualnej powinny mieć punkt końcowy zdefiniowany dla ruchu protokołu SSH, który można wyświetlić w **punkty końcowe** lub  **[sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md)**. Punkty końcowe na maszynach wirtualnych, które zostały utworzone za pomocą Menedżera zasobów są przechowywane w grupie zabezpieczeń sieci. Sprawdź także, że hello zasady zostały zastosowane toohello sieciowej grupy zabezpieczeń i że jest przywoływany w hello podsieci.

tooverify łączność z siecią, sprawdź punkty końcowe skonfigurowane hello i zobacz, jeżeli można osiągnąć hello maszyny Wirtualnej za pomocą innego protokołu, na przykład HTTP lub innej usługi.

Po wykonaniu tych kroków spróbuj ponownie połączenia SSH hello.

## <a name="find-hello-source-of-hello-issue"></a>Znajdź źródło hello hello wydania
Klient SSH Hello na tym komputerze może zakończyć się niepowodzeniem usługi SSH hello tooreach na powitania maszyny Wirtualnej Azure tooissues lub błędy konfiguracji hello następujące obszary:

* [Komputer kliencki SSH](#source-1-ssh-client-computer)
* [Urządzenie brzegowe organizacji](#source-2-organization-edge-device)
* [Punkt końcowy usługi w chmurze i uzyskiwać dostęp do listy kontroli (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Sieciowe grupy zabezpieczeń](#source-4-network-security-groups)
* [Maszyna wirtualna Azure opartej na systemie Linux](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Źródło 1: SSH komputera klienckiego
tooeliminate komputera jako źródło hello awarii hello, sprawdź, czy go SSH połączeń tooanother lokalnie, komputer oparty na systemie Linux.

![Diagram, który prezentuje składniki komputera klienta SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Jeśli hello połączenia nie powiedzie się, sprawdź hello następujące problemy na komputerze:

* Ustawienie zapory lokalnej, która blokuje ruch SSH ruchu przychodzącego lub wychodzącego (TCP 22)
* Lokalnie zainstalowane oprogramowanie serwera proxy klienta, który uniemożliwia połączeń SSH
* Zainstalowanego lokalnie pakietu oprogramowania, który uniemożliwia połączeń SSH do monitorowania sieci
* Inne rodzaje oprogramowania zabezpieczającego, które monitorowania ruchu lub Zezwalaj/nie zezwalaj na określone typy ruchu

Jeśli zastosować jedną z tych warunków, tymczasowo wyłączyć hello oprogramowania i spróbuj SSH połączenia tooan lokalnego komputera toofind limit przyczyny hello połączenia hello jest blokowana na tym komputerze. Następnie skontaktowanie się z administratorem toocorrect hello oprogramowania ustawienia tooallow SSH połączenia sieciowe.

Jeśli korzystasz z uwierzytelniania certyfikatów, sprawdź ma folderu .ssh toohello tych uprawnień w katalogu macierzystego:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (lub innych plików, które zostały zapisane w ich kluczy prywatnych)
* Chmod 644 ~/.ssh/known_hosts (zawiera hosty, że nawiązano połączenie toovia SSH)

## <a name="source-2-organization-edge-device"></a>Źródło 2: Urządzenie brzegowe organizacji
tooeliminate urządzenia krawędzi organizacji jako źródło hello hello awarii, sprawdź, czy komputerze, który jest podłączony bezpośrednio toohello Internet ułatwia tooyour połączenia SSH maszyny Wirtualnej platformy Azure. Jeśli uzyskują dostęp do hello maszyny Wirtualnej za pośrednictwem sieci VPN lokacja lokacja lub połączenia Azure ExpressRoute, Pomiń zbyt[źródła 4: sieciowej grupy zabezpieczeń](#nsg).

![Diagram, który prezentuje urządzenie brzegowe organizacji](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Jeśli nie masz komputera, który jest bezpośrednio połączony toohello Internet, Utwórz nową maszynę Wirtualną Azure w jego własnej usługi chmury lub grupy zasobów i używać go. Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną z systemem Linux na platformie Azure](quick-create-cli.md). Po zakończeniu testowania, należy usunąć hello zasobów grupy lub maszyny Wirtualnej i w chmurze usługi.

Jeśli tworzysz połączenie SSH z komputerem, który jest bezpośrednio połączony toohello Internet, sprawdź urządzenie brzegowe organizacji dla:

* Wewnętrzny zapory, która blokuje ruch SSH hello Internet
* Serwer proxy, który uniemożliwia połączeń SSH
* Włamań lub oprogramowanie na urządzeniach w sieci krawędzi, która uniemożliwia połączeń SSH do monitorowania sieci

Współpraca z ustawień sieci administrator toocorrect hello organizacji krawędzi urządzenia tooallow SSH ruchu z hello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Źródło 3: Punkt końcowy usługi w chmurze i listy ACL
> [!NOTE]
> To źródło dotyczy tylko tooVMs, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania. Dla maszyn wirtualnych, które zostały utworzone za pomocą Menedżera zasobów, Pomiń zbyt[źródła 4: sieciowej grupy zabezpieczeń](#nsg).

końcowy usługi w chmurze hello tooeliminate i listy ACL jako źródło hello hello awarii, sprawdź, inną maszynę Wirtualną platformy Azure, w hello sama sieć wirtualną można wprowadzać tooyour połączenia SSH maszyny Wirtualnej.

![Diagram, który prezentuje punktu końcowego usługi w chmurze i listy kontroli dostępu](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Jeśli nie masz inną maszynę Wirtualną w hello tej samej sieci wirtualnej, można łatwo utworzyć. Aby uzyskać więcej informacji, zobacz [Utwórz Maszynę wirtualną systemu Linux na platformie Azure przy użyciu interfejsu wiersza polecenia hello](quick-create-cli.md). Usuń hello dodatkowe maszyny Wirtualnej, gdy po zakończeniu testowania.

W przypadku utworzenia połączenia SSH z maszyną Wirtualną w hello sam wirtualnych sieci, należy sprawdzić hello następujące obszary:

* **Konfiguracja punktu końcowego Hello transmisji SSH na docelowej hello maszyny Wirtualnej.** port prywatny TCP Hello hello punktu końcowego powinna odpowiadać hello port TCP, na które hello SSH nasłuchuje usługa na powitania maszyny Wirtualnej. (hello domyślny port to 22). Sprawdź numer portu SSH TCP hello w hello portalu Azure, wybierając **maszyn wirtualnych** > *nazwę maszyny Wirtualnej* > **ustawienia**  >  **Punkty końcowe**.
* **Witaj listy ACL dla punktu końcowego ruchu SSH hello na powitania docelowej maszyny wirtualnej.** Listy ACL umożliwia toospecify dozwolony lub niedozwolony ruch przychodzący z hello Internetu, na podstawie jego adresu IP źródłowego. Nieprawidłowo skonfigurowane listy kontroli dostępu można zapobiec toohello ruchu przychodzącego SSH punktu końcowego. Sprawdź tooensure z listy kontroli dostępu, jaki ruch przychodzący z hello publicznych adresów IP z serwera proxy lub na innym serwerze krawędzi jest dozwolony. Aby uzyskać więcej informacji, zobacz [list (kontroli dostępu ACL) o dostęp do sieci kontroli](../../virtual-network/virtual-networks-acl.md).

punkt końcowy hello tooeliminate jako źródło problemu hello usunąć bieżący punkt końcowy hello, utworzyć inny punkt końcowy i określ nazwę SSH hello (port TCP 22 numeru portu publicznego i prywatnego hello). Aby uzyskać więcej informacji, zobacz [Konfigurowanie punktów końcowych na maszynie wirtualnej na platformie Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Źródła 4: Grupy zabezpieczeń sieci
Grupy zabezpieczeń sieci Włącz toohave większą kontrolę nad dozwolonego ruchu przychodzącego i wychodzącego. Można utworzyć reguły, które obejmują podsieci oraz usług w sieci wirtualnej platformy Azure w chmurze. Sprawdź Twojej sieci zabezpieczeń grupy reguł tooensure tego tooand ruchu SSH z hello jest dozwolone przez Internet.
Aby uzyskać więcej informacji, zobacz [dotyczące grup zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md).

Umożliwia także weryfikowanie IP toovalidate hello NSG konfiguracji. Aby uzyskać więcej informacji, zobacz [omówienie monitorowania sieci platformy Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Źródło 5: Opartych na systemie Linux maszyny wirtualnej platformy Azure
Źródło ostatniej Hello o potencjalnych problemach jest hello Azure samej maszyny wirtualnej.

![Diagram, który prezentuje opartych na systemie Linux maszyny wirtualnej platformy Azure](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Jeśli jeszcze tego nie zrobiono tego wcześniej, wykonaj instrukcje hello [tooreset hasła lub SSH dla maszyn wirtualnych z systemem Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Spróbuj ponownie nawiązać połączenie z komputera. Jeśli nadal nie, hello należą hello możliwe problemy:

* Witaj usługi SSH nie jest uruchomiona na powitania docelowej maszyny wirtualnej.
* Witaj usługi SSH nie nasłuchuje na porcie TCP 22. tootest, zainstaluj klienta programu telnet komputera lokalnego i uruchom "telnet *cloudServiceName*. cloudapp.net 22". Ten krok określa umożliwia punkt końcowy SSH toohello komunikacji przychodzących i wychodzących, jeśli hello maszyny wirtualnej.
* Zapora lokalnego Hello na powitania docelowej maszyny wirtualnej ma reguł, które uniemożliwiają przychodzącego i wychodzącego ruchu SSH.
* Włamań lub oprogramowania, które działa na powitania maszyny wirtualnej platformy Azure do monitorowania sieci uniemożliwia nawiązanie połączenia SSH.

## <a name="additional-resources"></a>Dodatkowe zasoby
Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z dostęp do aplikacji, zobacz [Rozwiązywanie problemów dotyczących dostępu tooan aplikacja była uruchomiona na maszynie wirtualnej platformy Azure](troubleshoot-app-connection.md)
