---
title: Informacje o wersji zestawu Microsoft Azure stosu Development Kit | Dokumentacja firmy Microsoft
description: "Ulepszenia, poprawki i znane problemy dotyczące Azure stosu Development Kit."
services: azure-stack
documentationcenter: 
author: andredm7
manager: femila
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: andredm
ms.openlocfilehash: 88247733c945de277e4d74b049d5edc6e4d97d3b
ms.sourcegitcommit: 1d423a8954731b0f318240f2fa0262934ff04bd9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="azure-stack-development-kit-release-notes"></a>Informacje o wersji platformy Azure stosu Development Kit

*Dotyczy: Azure stosu Development Kit*

Te informacje o wersji zawierają informacje dotyczące ulepszeń, poprawki i znane problemy w systemie Azure stosu Development Kit. Jeśli nie masz pewności, której używasz wersji, możesz [sprawdzić za pomocą portalu](azure-stack-updates.md#determine-the-current-version).

## <a name="build-201801032"></a>Kompilacja 20180103.2

### <a name="new-features-and-fixes"></a>Nowe funkcje i poprawki

- Zobacz [nowe funkcje i poprawki](azure-stack-update-1712.md#new-features-and-fixes) sekcji 1712 stosu Azure aktualizacji informacje o wersji programu Azure stosu zintegrowanych systemów.

    > [!IMPORTANT]
    > Niektóre elementy na liście **nowe funkcje i poprawki** sekcji mają zastosowanie tylko do stosu Azure zintegrowanych systemów.

### <a name="known-issues"></a>Znane problemy
 
#### <a name="deployment"></a>Wdrożenie
- Należy określić serwer czasu za pomocą adresu IP podczas wdrażania.

#### <a name="infrastructure-management"></a>Zarządzanie infrastrukturą
- Nie należy włączać infrastruktura kopii zapasowej na **infrastruktura kopii zapasowej** bloku.
- Adres IP kontrolera zarządzania płytą główną i modelu nie są wyświetlane w ważne informacje węzła jednostki skalowania. To zachowanie jest oczekiwane w Azure stosu Development Kit.

#### <a name="portal"></a>Portal
- Może pojawić się pustego pulpitu nawigacyjnego w portalu. Aby odzyskać pulpitu nawigacyjnego, wybierz koło zębate ikonę w prawym górnym rogu portalu, a następnie wybierz **przywrócić ustawienia domyślne**.
- Po wyświetleniu właściwości grupy zasobów, **Przenieś** przycisk jest niedostępny. To zachowanie jest oczekiwane. Przeniesienie grup zasobów między subskrypcjami nie jest obecnie obsługiwane.
-  Na każdy przepływ pracy, gdzie wybierz subskrypcji, grupy zasobów lub lokalizacji w listy rozwijanej może wystąpić jeden lub więcej z następujących problemów:

   - Może pojawić się pusty wiersz na początku listy. Nadal można wybrać elementu zgodnie z oczekiwaniami.
   - Jeśli na liście elementów na liście rozwijanej jest krótki, nie można przeglądać nazwy elementu.
   - Jeśli masz wiele subskrypcji użytkownika listy rozwijanej grupy zasobów może być pusta. 

   Aby obejść problemy z ostatnich dwóch, możesz wpisać nazwę subskrypcji lub grupy zasobów (jeśli ją znasz), lub można użyć programu PowerShell.

- Zobaczysz **wymagana aktywacja** alert ostrzeżenia, zaleceniem można zarejestrować zestawu Azure stosu Development Kit. To zachowanie jest oczekiwane.
- Jeśli **składnika** kliknięciu łącza za pomocą dowolnego **rolę infrastruktury** alertów, powstałe w ten sposób **omówienie** bloku próbuje załadować środowisko i kończy się niepowodzeniem. Ponadto ** omówienie ** bloku jest nie upłynął limit czasu.
- Usunięcie użytkownika powoduje subskrypcje zasoby oddzielone. Jako obejście najpierw usuń zasoby użytkownika lub grupy zasobów całej, a następnie usuń subskrypcji użytkownika.
- Nie jest możliwe wyświetlić uprawnienia do subskrypcji przy użyciu portali stosu Azure. Jako rozwiązanie alternatywne można sprawdzić uprawnień za pomocą programu PowerShell.
 
#### <a name="marketplace"></a>Portal Marketplace
- Niektóre elementy marketplace są usuwane w tej wersji z powodu problemów ze zgodnością. Te zostaną ponownie włączone po dalszych weryfikacji.
- Użytkownicy można przeglądać pełnego portalu marketplace bez subskrypcji i widoczne elementy administracyjne, takie jak plany i oferty. Te elementy są niefunkcjonalne dla użytkowników.
 
#### <a name="compute"></a>Wystąpienia obliczeniowe
- Użytkownicy skorzystać z opcji, aby utworzyć maszynę wirtualną z magazynu geograficznie nadmiarowego. Ta konfiguracja powoduje niepowodzenie tworzenia maszyny wirtualnej. 
- Można skonfigurować dostępność maszyn wirtualnych, ustaw tylko z jednej domeny błędów i jedną domenę aktualizacji.
- Brak nie doświadczenie marketplace, aby utworzyć zestawy skalowania maszyny wirtualnej. Można utworzyć skali ustawić za pomocą szablonu.
- Ustawienia skalowania dla zestawy skalowania maszyny wirtualnej nie są dostępne w portalu. Jako rozwiązanie alternatywne można zastosować [programu Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set). Z powodu różnic wersji programu PowerShell, należy użyć `-Name` parametru zamiast `-VMScaleSetName`.

#### <a name="networking"></a>Networking
- Nie można utworzyć modułu równoważenia obciążenia z publicznym adresem IP, za pomocą portalu. Jako rozwiązanie alternatywne można utworzyć modułu równoważenia obciążenia za pomocą programu PowerShell.
- Podczas tworzenia modułu równoważenia obciążenia sieciowego, należy utworzyć regułę translatora adresów sieciowych adres. Jeśli nie, otrzymasz wystąpił błąd podczas próby dodania reguły NAT po utworzeniu usługi równoważenia obciążenia.
- W obszarze **sieci**, jeśli klikniesz przycisk **połączenia** do skonfigurowania połączenia sieci VPN, **do wirtualnymi** jest wymieniony jako typ połączenia to możliwe. Nie należy zaznaczać tej opcji. Obecnie tylko **lokacja lokacja (IPsec)** opcja jest obsługiwana.
- Nie można usunąć skojarzenie publicznego adresu IP z maszyną wirtualną (VM), po utworzeniu maszyny Wirtualnej i skojarzonych z tym adresem IP. Usuwanie skojarzeń pojawi się do pracy, ale poprzednio przypisanych publiczny adres IP pozostają skojarzone z oryginalna maszyna wirtualna. Dzieje się tak nawet w przypadku ponownego przypisywania adresów IP do nowej maszyny Wirtualnej (nazywane *wymiany wirtualnych adresów IP*). Wszystkie przyszłe próbuje nawiązać połączenie za pośrednictwem tego wyniku adresów IP w przypadku połączenia pierwotnie skojarzonego VM, a nie nowy. Obecnie tylko musi używać nowego publiczne adresy IP do tworzenia nowej maszyny Wirtualnej.
- Operatory stosu Azure może być niemożliwe do wdrożenia, usuwanie, modyfikowanie, sieciami wirtualnymi lub grup zabezpieczeń sieci. Ten problem występuje przede wszystkim prób kolejnych aktualizacji tego samego pakietu. Jest to spowodowane problemem pakietów za pomocą aktualizacji, który jest obecnie badanym.
- Wewnętrzny równoważenia obciążenia (ILB) nieprawidłowo obsługuje adresów MAC dla maszyn wirtualnych zaplecza, które dzieli wystąpień systemu Linux.
 
#### <a name="sqlmysql"></a>SQL/MySQL 
- Może potrwać do godziny dzierżawców można utworzyć bazy danych w nowym SQL lub MySQL jednostki SKU. 
- Tworzenie elementów bezpośrednio na SQL i MySQL serwerów, które nie są wykonywane przez dostawcę zasobów hosta nie jest obsługiwana i może spowodować niezgodne stanu.

#### <a name="app-service"></a>App Service
- Użytkownik musi zarejestrować dostawcy zasobów magazynu, przed utworzeniem ich pierwszej funkcji platformy Azure w ramach subskrypcji.
 
#### <a name="usage-and-billing"></a>Użycie i rozliczenia
- Publiczny danych pomiaru użycia adresów IP zawiera takie same *Data/godzina zdarzenia* wartość dla każdego rekordu zamiast *TimeDate* sygnatury pokazujący utworzenia rekordu. Obecnie nie można używać tych danych do wykonania dokładnego rozliczania użycie publicznego adresu IP.

#### <a name="identity"></a>Tożsamość

W usłudze Azure Active Directory Federation Services (ADFS) wdrożone w środowiskach **azurestack\azurestackadmin** konto nie jest już właściciela subskrypcji domyślny dostawca. Zamiast podczas logowania się na **portalu administracyjnego / punktu końcowego adminmanagement** z **azurestack\azurestackadmin**, można użyć **azurestack\cloudadmin** konta, dlatego Czy można zarządzać i korzystania z subskrypcji domyślny dostawca.

> [!IMPORTANT]
> Nawet **azurestack\cloudadmin** konta jest właścicielem subskrypcji dostawcy domyślne w środowiskach usług AD FS wdrożona, nie ma uprawnień do protokołu RDP na hoście. Nadal używać **azurestack\azurestackadmin** konta lub lokalnego konta administratora do logowania, dostęp i zarządzać hostem zgodnie z potrzebami.

## <a name="build-201711221"></a>Kompilacja 20171122.1

### <a name="new-features-and-fixes"></a>Nowe funkcje i poprawki

- Zobacz [nowe funkcje i poprawki](azure-stack-update-1711.md#new-features-and-fixes) sekcji 1711 stosu Azure aktualizacji informacje o wersji programu Azure stosu zintegrowanych systemów.

    > [!IMPORTANT]
    > Niektóre elementy na liście **nowe funkcje i poprawki** sekcji mają zastosowanie tylko do stosu Azure zintegrowanych systemów.

### <a name="known-issues"></a>Znane problemy
 
#### <a name="deployment"></a>Wdrożenie
- Należy określić serwer czasu za pomocą adresu IP podczas wdrażania.

#### <a name="infrastructure-management"></a>Zarządzanie infrastrukturą
- Nie należy włączać infrastruktura kopii zapasowej na **infrastruktura kopii zapasowej** bloku.
- Adres IP kontrolera zarządzania płytą główną i modelu nie są wyświetlane w ważne informacje węzła jednostki skalowania. To zachowanie jest oczekiwane w Azure stosu Development Kit.

#### <a name="portal"></a>Portal
- Może pojawić się pustego pulpitu nawigacyjnego w portalu. Aby odzyskać pulpitu nawigacyjnego, wybierz koło zębate ikonę w prawym górnym rogu portalu, a następnie wybierz **przywrócić ustawienia domyślne**.
- Po wyświetleniu właściwości grupy zasobów, **Przenieś** przycisk jest niedostępny. To zachowanie jest oczekiwane. Przeniesienie grup zasobów między subskrypcjami nie jest obecnie obsługiwane.
-  Na każdy przepływ pracy, gdzie wybierz subskrypcji, grupy zasobów lub lokalizacji w listy rozwijanej może wystąpić jeden lub więcej z następujących problemów:

   - Może pojawić się pusty wiersz na początku listy. Nadal można wybrać elementu zgodnie z oczekiwaniami.
   - Jeśli na liście elementów na liście rozwijanej jest krótki, nie można przeglądać nazwy elementu.
   - Jeśli masz wiele subskrypcji użytkownika listy rozwijanej grupy zasobów może być pusta. 

   Aby obejść problemy z ostatnich dwóch, możesz wpisać nazwę subskrypcji lub grupy zasobów (jeśli ją znasz), lub można użyć programu PowerShell.

- Zobaczysz **wymagana aktywacja** alert ostrzeżenia, zaleceniem można zarejestrować zestawu Azure stosu Development Kit. To zachowanie jest oczekiwane.
- Jeśli **składnika** kliknięciu łącza za pomocą dowolnego **rolę infrastruktury** alertów, powstałe w ten sposób **omówienie** bloku próbuje załadować środowisko i kończy się niepowodzeniem. Ponadto **omówienie** bloku jest nie upłynął limit czasu.
- Usunięcie użytkownika powoduje subskrypcje zasoby oddzielone. Jako obejście najpierw usuń zasoby użytkownika lub grupy zasobów całej, a następnie usuń subskrypcji użytkownika.
- Nie jest możliwe wyświetlić uprawnienia do subskrypcji przy użyciu portali stosu Azure. Jako rozwiązanie alternatywne można sprawdzić uprawnień za pomocą programu PowerShell.
 
#### <a name="marketplace"></a>Portal Marketplace
- Podczas dodawania elementów do stosu Azure marketplace przy użyciu **Dodaj z platformy Azure** opcji, nie wszystkie elementy mogą być widoczne do pobrania.
- Użytkownicy można przeglądać pełnego portalu marketplace bez subskrypcji i widoczne elementy administracyjne, takie jak plany i oferty. Te elementy są niefunkcjonalne dla użytkowników.
 
#### <a name="compute"></a>Wystąpienia obliczeniowe
- Użytkownicy skorzystać z opcji, aby utworzyć maszynę wirtualną z magazynu geograficznie nadmiarowego. Ta konfiguracja powoduje niepowodzenie tworzenia maszyny wirtualnej. 
- Można skonfigurować dostępność maszyn wirtualnych, ustaw tylko z jednej domeny błędów i jedną domenę aktualizacji.
- Brak nie doświadczenie marketplace, aby utworzyć zestawy skalowania maszyny wirtualnej. Można utworzyć skali ustawić za pomocą szablonu.
- Ustawienia skalowania dla zestawy skalowania maszyny wirtualnej nie są dostępne w portalu. Jako rozwiązanie alternatywne można zastosować [programu Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set). Z powodu różnic wersji programu PowerShell, należy użyć `-Name` parametru zamiast `-VMScaleSetName`.

#### <a name="networking"></a>Networking
- Nie można utworzyć modułu równoważenia obciążenia z publicznym adresem IP, za pomocą portalu. Jako rozwiązanie alternatywne można utworzyć modułu równoważenia obciążenia za pomocą programu PowerShell.
- Podczas tworzenia modułu równoważenia obciążenia sieciowego, należy utworzyć regułę translatora adresów sieciowych adres. Jeśli nie, otrzymasz wystąpił błąd podczas próby dodania reguły NAT po utworzeniu usługi równoważenia obciążenia.
- W obszarze **sieci**, jeśli klikniesz przycisk **połączenia** do skonfigurowania połączenia sieci VPN, **do wirtualnymi** jest wymieniony jako typ połączenia to możliwe. Nie należy zaznaczać tej opcji. Obecnie tylko **lokacja lokacja (IPsec)** opcja jest obsługiwana.
- Nie można usunąć skojarzenie publicznego adresu IP z maszyną wirtualną (VM), po utworzeniu maszyny Wirtualnej i skojarzonych z tym adresem IP. Usuwanie skojarzeń pojawi się do pracy, ale poprzednio przypisanych publiczny adres IP pozostają skojarzone z oryginalna maszyna wirtualna. Dzieje się tak nawet w przypadku ponownego przypisywania adresów IP do nowej maszyny Wirtualnej (nazywane *wymiany wirtualnych adresów IP*). Wszystkie przyszłe próbuje nawiązać połączenie za pośrednictwem tego wyniku adresów IP w przypadku połączenia pierwotnie skojarzonego VM, a nie nowy. Obecnie tylko musi używać nowego publiczne adresy IP do tworzenia nowej maszyny Wirtualnej.
- Operatory stosu Azure może być niemożliwe do wdrożenia, usuwanie, modyfikowanie, sieciami wirtualnymi lub grup zabezpieczeń sieci. Ten problem występuje przede wszystkim prób kolejnych aktualizacji tego samego pakietu. Jest to spowodowane problemem pakietów za pomocą aktualizacji, który jest obecnie badanym.
- Wewnętrzny równoważenia obciążenia (ILB) nieprawidłowo obsługuje adresów MAC dla maszyn wirtualnych zaplecza, które dzieli wystąpień systemu Linux.
 
#### <a name="sqlmysql"></a>SQL/MySQL 
- Może potrwać do godziny dzierżawców można utworzyć bazy danych w nowym SQL lub MySQL jednostki SKU. 
- Tworzenie elementów bezpośrednio na SQL i MySQL serwerów, które nie są wykonywane przez dostawcę zasobów hosta nie jest obsługiwana i może spowodować niezgodne stanu.

    > [!NOTE]
    > Zobacz poszczególne [SQL](https://docs.microsoft.com/azure/azure-stack/azure-stack-sql-resource-provider-deploy) i [MySQL](https://docs.microsoft.com/azure/azure-stack/azure-stack-mysql-resource-provider-deploy) artykuły, aby uzyskać wskazówki dotyczące zgodności wersji Instalatora.

#### <a name="app-service"></a>App Service
- Użytkownik musi zarejestrować dostawcy zasobów magazynu, przed utworzeniem ich pierwszej funkcji platformy Azure w ramach subskrypcji.
 
#### <a name="usage-and-billing"></a>Użycie i rozliczenia
- Publiczny danych pomiaru użycia adresów IP zawiera takie same *Data/godzina zdarzenia* wartość dla każdego rekordu zamiast *TimeDate* sygnatury pokazujący utworzenia rekordu. Obecnie nie można używać tych danych do wykonania dokładnego rozliczania użycie publicznego adresu IP.

#### <a name="identity"></a>Tożsamość

W usłudze Azure Active Directory Federation Services (ADFS) wdrożone w środowiskach **azurestack\azurestackadmin** konto nie jest już właściciela subskrypcji domyślny dostawca. Zamiast podczas logowania się na **portalu administracyjnego / punktu końcowego adminmanagement** z **azurestack\azurestackadmin**, można użyć **azurestack\cloudadmin** konta, dlatego Czy można zarządzać i korzystania z subskrypcji domyślny dostawca.

> [!IMPORTANT]
> Nawet **azurestack\cloudadmin** konta jest właścicielem subskrypcji dostawcy domyślne w środowiskach usług AD FS wdrożona, nie ma uprawnień do protokołu RDP na hoście. Nadal używać **azurestack\azurestackadmin** konta lub lokalnego konta administratora do logowania, dostęp i zarządzać hostem zgodnie z potrzebami.


## <a name="build-201710201"></a>Kompilacja 20171020.1

### <a name="improvements-and-fixes"></a>Ulepszeń i poprawek

Aby wyświetlić listę ulepszeń i poprawek w 20171020.1 kompilacji, zobacz [ulepszeń i poprawek](azure-stack-update-1710.md#improvements-and-fixes) sekcji 1710 informacje o wersji programu Azure stosu zintegrowanych systemów. Niektóre elementy wymienione w sekcji "dodatkową jakością ulepszeń i poprawek" mają zastosowanie tylko w zintegrowanych systemów.

Ponadto zostały wprowadzone następujące poprawki:
- Rozwiązano problem, w której dostawcy zasobów obliczeniowych wyświetlany stan nieznany.
- Rozwiązano problem, na którym przydziały mogą nie występować w portalu administratora po utworzeniu je i później spróbuj wyświetlić szczegóły planu.

### <a name="known-issues"></a>Znane problemy

#### <a name="powershell"></a>PowerShell
- Wersja modułu PowerShell AzureRM 1.2.11 zawiera listę fundamentalne zmiany. Aby uzyskać informacje dotyczące uaktualniania 1.2.10 wersji, zobacz [Przewodnik po migracji](https://aka.ms/azspowershellmigration).
 
#### <a name="deployment"></a>Wdrożenie
- Należy określić serwer czasu za pomocą adresu IP podczas wdrażania.

#### <a name="infrastructure-management"></a>Zarządzanie infrastrukturą
- Nie należy włączać infrastruktura kopii zapasowej na **infrastruktura kopii zapasowej** bloku.
- Adres IP kontrolera zarządzania płytą główną i modelu nie są wyświetlane w ważne informacje węzła jednostki skalowania. To zachowanie jest oczekiwane w Azure stosu Development Kit.

#### <a name="portal"></a>Portal
- Może pojawić się pustego pulpitu nawigacyjnego w portalu. Aby odzyskać pulpitu nawigacyjnego, wybierz koło zębate ikonę w prawym górnym rogu portalu, a następnie wybierz **przywrócić ustawienia domyślne**.
- Po wyświetleniu właściwości grupy zasobów, **Przenieś** przycisk jest niedostępny. To zachowanie jest oczekiwane. Przeniesienie grup zasobów między subskrypcjami nie jest obecnie obsługiwane.
-  Na każdy przepływ pracy, gdzie wybierz subskrypcji, grupy zasobów lub lokalizacji w listy rozwijanej może wystąpić jeden lub więcej z następujących problemów:

   - Może pojawić się pusty wiersz na początku listy. Nadal można wybrać elementu zgodnie z oczekiwaniami.
   - Jeśli na liście elementów na liście rozwijanej jest krótki, nie można przeglądać nazwy elementu.
   - Jeśli masz wiele subskrypcji użytkownika listy rozwijanej grupy zasobów może być pusta. 

   Aby obejść problemy z ostatnich dwóch, możesz wpisać nazwę subskrypcji lub grupy zasobów (jeśli ją znasz), lub można użyć programu PowerShell.

- Zobaczysz **wymagana aktywacja** alert ostrzeżenia, zaleceniem można zarejestrować zestawu Azure stosu Development Kit. To zachowanie jest oczekiwane.
- W **wymagana aktywacja** ostrzeżenie szczegóły alertu, nie kliknij łącze, aby **AzureBridge** składnika. Jeśli to zrobisz, **omówienie** bloku bez powodzenia próbuje załadować, a nie upłynął limit czasu.
- W portalu administratora może wystąpić **błąd podczas pobierania dzierżaw** błąd **powiadomienia** obszaru. Można bezpiecznie zignorować ten błąd.
- Usunięcie użytkownika powoduje subskrypcje zasoby oddzielone. Jako obejście najpierw usuń zasoby użytkownika lub grupy zasobów całej, a następnie usuń subskrypcji użytkownika.
- Nie jest możliwe wyświetlić uprawnienia do subskrypcji przy użyciu portali stosu Azure. Jako rozwiązanie alternatywne można sprawdzić uprawnień za pomocą programu PowerShell.
 
#### <a name="marketplace"></a>Portal Marketplace
- Podczas dodawania elementów do stosu Azure marketplace przy użyciu **Dodaj z platformy Azure** opcji, nie wszystkie elementy mogą być widoczne do pobrania.
- Użytkownicy można przeglądać pełnego portalu marketplace bez subskrypcji i widoczne elementy administracyjne, takie jak plany i oferty. Te elementy są niefunkcjonalne dla użytkowników.
 
#### <a name="compute"></a>Wystąpienia obliczeniowe
- Użytkownicy skorzystać z opcji, aby utworzyć maszynę wirtualną z magazynu geograficznie nadmiarowego. Ta konfiguracja powoduje niepowodzenie tworzenia maszyny wirtualnej. 
- Można skonfigurować dostępność maszyn wirtualnych, ustaw tylko z jednej domeny błędów i jedną domenę aktualizacji.
- Brak nie doświadczenie marketplace, aby utworzyć zestawy skalowania maszyny wirtualnej. Można utworzyć skali ustawić za pomocą szablonu.
- Ustawienia skalowania dla zestawy skalowania maszyny wirtualnej nie są dostępne w portalu. Jako rozwiązanie alternatywne można zastosować [programu Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set). Z powodu różnic wersji programu PowerShell, należy użyć `-Name` parametru zamiast `-VMScaleSetName`.

#### <a name="networking"></a>Networking
- Nie można utworzyć modułu równoważenia obciążenia z publicznym adresem IP, za pomocą portalu. Jako rozwiązanie alternatywne można utworzyć modułu równoważenia obciążenia za pomocą programu PowerShell.
- Podczas tworzenia modułu równoważenia obciążenia sieciowego, należy utworzyć regułę translatora adresów sieciowych adres. Jeśli nie, otrzymasz wystąpił błąd podczas próby dodania reguły NAT po utworzeniu usługi równoważenia obciążenia.
- W obszarze **sieci**, jeśli klikniesz przycisk **połączenia** do skonfigurowania połączenia sieci VPN, **do wirtualnymi** jest wymieniony jako typ połączenia to możliwe. Nie należy zaznaczać tej opcji. Obecnie tylko **lokacja lokacja (IPsec)** opcja jest obsługiwana.
- Nie można usunąć skojarzenie publicznego adresu IP z maszyną wirtualną (VM), po utworzeniu maszyny Wirtualnej i skojarzonych z tym adresem IP. Usuwanie skojarzeń pojawi się do pracy, ale poprzednio przypisanych publiczny adres IP pozostają skojarzone z oryginalna maszyna wirtualna. Dzieje się tak nawet w przypadku ponownego przypisywania adresów IP do nowej maszyny Wirtualnej (nazywane *wymiany wirtualnych adresów IP*). Wszystkie przyszłe próbuje nawiązać połączenie za pośrednictwem tego wyniku adresów IP w przypadku połączenia pierwotnie skojarzonego VM, a nie nowy. Obecnie tylko musi używać nowego publiczne adresy IP do tworzenia nowej maszyny Wirtualnej.
 
#### <a name="sqlmysql"></a>SQL/MySQL 
- Może potrwać do godziny dzierżawców można utworzyć bazy danych w nowym SQL lub MySQL jednostki SKU. 
- Tworzenie elementów bezpośrednio na SQL i MySQL serwerów, które nie są wykonywane przez dostawcę zasobów hosta nie jest obsługiwana i może spowodować niezgodne stanu.

#### <a name="app-service"></a>App Service
- Użytkownik musi zarejestrować dostawcy zasobów magazynu, przed utworzeniem ich pierwszej funkcji platformy Azure w ramach subskrypcji.
 
#### <a name="usage-and-billing"></a>Użycie i rozliczenia
- Publiczny danych pomiaru użycia adresów IP zawiera takie same *Data/godzina zdarzenia* wartość dla każdego rekordu zamiast *TimeDate* sygnatury pokazujący utworzenia rekordu. Obecnie nie można używać tych danych do wykonania dokładnego rozliczania użycie publicznego adresu IP.