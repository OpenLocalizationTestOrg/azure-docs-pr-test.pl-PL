---
title: "najlepsze rozwiązania zabezpieczeń maszyny wirtualnej aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera szereg zabezpieczeń najlepsze rozwiązania w zakresie toobe używane w maszynach wirtualnych znajdujących się na platformie Azure."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Najlepsze rozwiązania dotyczące zabezpieczeń maszyny Wirtualnej Azure

W większości infrastruktury jako scenariuszy usługa (IaaS) [Azure maszynach wirtualnych (VM)](https://docs.microsoft.com/en-us/azure/virtual-machines/) są hello obciążenia głównego dla organizacji korzystających z chmury obliczeniowej. Ten fakt jest szczególnie widoczne w [scenariuszy hybrydowych](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) gdzie tooslowly chcesz, aby organizacje migracji obciążeń toohello chmury. W takich sytuacjach należy wykonać hello [zabezpieczeń Ogólne zagadnienia dotyczące IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)i stosowania zabezpieczeń najlepsze rozwiązania w zakresie tooall maszyn wirtualnych.

W tym artykule opisano różne wirtualna najlepszych rozwiązań dotyczących zabezpieczeń, każdy pochodzące z naszych klientów i własnej bezpośrednio z maszyną wirtualną.

najlepsze rozwiązania w zakresie Hello są oparte na konsensu opinii i pracować z bieżącej funkcji platformy Azure i zestawy funkcji. Ponieważ opinie i technologie mogą ulec zmianie, planujemy tooupdate ten artykuł regularnie tooreflect tych zmian.

Dla każdego ze względów hello opisano.

* Jakie hello najlepszym rozwiązaniem jest.
* Dlatego jest tooenable dobrze go.
* Jak można znaleźć tooenable go.
* Co może się zdarzyć, jeśli nie zostanie tooenable go.
* Możliwe alternatywy toohello najlepszym rozwiązaniem.

Artykuł Hello sprawdza hello następujących najlepszych rozwiązaniach dotyczących zabezpieczeń maszyny Wirtualnej:

* Maszyna wirtualna uwierzytelniania i kontroli dostępu
* Maszyna wirtualna dostępności i dostępu do sieci
* Ochrona danych przechowywanych na maszynach wirtualnych przez wymuszenie szyfrowania
* Zarządzanie aktualizacjami sieci maszyny Wirtualnej
* Zarządzanie strukturę bezpieczeństwa maszyny Wirtualnej
* Monitor wydajności maszyny Wirtualnej

## <a name="vm-authentication-and-access-control"></a>Maszyna wirtualna uwierzytelniania i kontroli dostępu

pierwszym krokiem Hello ochrony maszyny Wirtualnej jest tooensure, aby tylko autoryzowani użytkownicy są tooset stanie się nowych maszyn wirtualnych. Można użyć [zasady usługi Azure Resource Manager](../azure-resource-manager/resource-manager-policy.md) konwencje tooestablish dla zasobów w organizacji, tworzenie niestandardowych zasad i Zastosuj tooresources te zasady, takie jak [grup zasobów](../azure-resource-manager/resource-group-overview.md).

Maszyny wirtualne, które należy grupy zasobów tooa naturalnie dziedziczą jego zasadami. Mimo że firma Microsoft zaleca takie podejście toomanaging maszyn wirtualnych, możesz również kontroli dostępu tooindividual wirtualna zasady za pomocą [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md).

Po włączeniu zasady Resource Manager i dostęp do maszyny Wirtualnej toocontrol RBAC, można zwiększyć ogólne bezpieczeństwo maszyny Wirtualnej. Zaleca się konsolidowanie maszyn wirtualnych z hello cyklu życia tej samej do hello tej samej grupie zasobów. Za pomocą grup zasobów, można wdrożyć, monitorowania i rzutowanie rozliczeń kosztów zasobów. tooenable tooaccess użytkowników i konfigurowanie maszyn wirtualnych, użyj [najniższych uprawnień podejście](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). Podczas przypisywania uprawnień toousers plan i hello toouse następujące wbudowane role Azure:

- [Maszyny wirtualnej współautora](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): zarządzenie maszynami wirtualnymi, ale nie hello wirtualnych sieci lub magazynu toowhich konta są one połączone.
- [Klasycznym współautora maszyny wirtualnej](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): można zarządzać maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrażania, ale nie hello wirtualnych sieci lub magazynu konta toowhich hello maszyny wirtualne są połączone.
- [Menedżer zabezpieczeń](../active-directory/role-based-access-built-in-roles.md#security-manager): Zarządzanie składniki zabezpieczeń, zasady zabezpieczeń i maszyn wirtualnych.
- [DevTest Labs użytkownika](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): można przeglądać wszystko i połączyć, uruchom ponownie uruchom i zamknij maszyny wirtualne.

Nie udostępniaj kont i haseł innym administratorom, a nie ponownie użyć hasła w wielu kont użytkowników lub usług, szczególnie hasła związanych z mediami społecznościowymi lub innymi działaniami innych niż administracyjne. W idealnym przypadku należy użyć [usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooset szablony zapasową maszyn wirtualnych bezpieczne. Przy użyciu tej metody, można wzmocnienie wybrane opcje wdrażania oraz wymusi ustawienia zabezpieczeń w całym hello wdrożenia.

Organizacji, które nie wymusić kontrolę dostępu do danych dzięki wykorzystaniu możliwości, takich jak RBAC może być przyznania użytkownikom więcej uprawnień niż jest to konieczne. Dane toocertain dostępu użytkownika nieodpowiednie bezpośrednio może naruszyć tych danych.

## <a name="vm-availability-and-network-access"></a>Maszyna wirtualna dostępności i dostępu do sieci

Jeśli maszyna wirtualna jest uruchomiona kluczowe aplikacje wymagające wysokiej dostępności toohave, zdecydowanie zaleca się użycie wielu maszyn wirtualnych. Aby uzyskać większą dostępność, należy utworzyć co najmniej dwóch maszyn wirtualnych w hello [zestawu dostępności](../virtual-machines/windows/tutorial-availability-sets.md).

[Moduł równoważenia obciążenia Azure](../load-balancer/load-balancer-overview.md) wymaga również, że równoważeniem obciążenia maszyn wirtualnych należy toohello tego samego zestawu dostępności. Jeśli te maszyny wirtualne muszą być dostępne z hello Internet, należy skonfigurować [modułu równoważenia obciążenia internetowy](../load-balancer/load-balancer-internet-overview.md).

Jeśli maszyny wirtualne są uwidocznione toohello Internet, ważne jest, że [sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-networks-nsg.md). Ponieważ grupy NSG mogą być zastosowane toosubnets, można zminimalizować hello liczbę grup NSG przez grupowanie zasobów według podsieci i zastosowanie grup NSG toohello podsieci. Celem Hello jest toocreate warstwę izolacji sieci, co można zrobić, konfigurując prawidłowo hello [zabezpieczenia sieci](../best-practices-network-security.md) możliwości na platformie Azure.

Umożliwia także hello just in time (JIT) dostęp do maszyny Wirtualnej funkcji z Centrum zabezpieczeń Azure toocontrol, kto ma dostęp zdalny tooa określonej maszyny Wirtualnej i jak długo.

Organizacje, które nie Wymuszaj ograniczenia dostępu do sieci maszyn wirtualnych połączonych z tooInternet są udostępniane toosecurity zagrożeń, takich jak atak Siłowy protokołu RDP (Remote Desktop).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Ochrona danych przechowywanych na maszyn wirtualnych przez wymuszenie szyfrowania

[Szyfrowanie danych magazynowanych](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) jest obowiązkowy warstwę danych suwerenności prywatności, zgodności i danych. [Szyfrowanie dysków Azure](../security/azure-security-disk-encryption.md) umożliwia tooencrypt Administratorzy IT systemu Windows i dysków maszyny Wirtualnej systemu Linux IaaS. Szyfrowanie dysków łączy funkcji Windows BitLocker standardowych hello i hello Linux dm-crypt funkcji tooprovide szyfrowania woluminów hello systemu operacyjnego i dysków z danymi hello.

Można zastosować szyfrowanie dysków toohelp chronić Twoje dane toomeet wymagań organizacyjnych zabezpieczeń i zgodności. Organizacji należy wziąć pod uwagę przy użyciu szyfrowania toohelp ograniczyć dostęp do danych powiązanych toounauthorized ryzyka. Zalecamy również szyfrowania dysków, przed przystąpieniem do napisania toothem poufnych danych.

Można się tooencrypt Twojego tooprotect woluminów danych maszyny Wirtualnej w rest na koncie magazynu Azure. Zabezpieczenia przy użyciu kluczy szyfrowania hello i klucz tajny [usługi Azure Key Vault](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Organizacje, które nie wymuszania szyfrowania danych są bardziej narażona toodata-problemy z integralnością. Na przykład złośliwe lub nieautoryzowanym użytkownikom może kradzieży danych, którego bezpieczeństwo zostało naruszone konta lub uzyskania kodowanych w ClearFormat toodata nieautoryzowanego dostępu. Oprócz pobierania na ryzyko, toocomply z przepisów branżowych firmy musi udowodnić, że są one wykonywania starannością, oraz za pomocą poprawnych zabezpieczeń kontrolki tooenhance ich bezpieczeństwo danych.

Zobacz toolearn więcej informacji na temat szyfrowania dysku [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Zarządzanie aktualizacjami sieci maszyny Wirtualnej

Ponieważ maszynach wirtualnych platformy Azure, podobnie jak wszystkie lokalnych maszyn wirtualnych, są przeznaczone toobe zarządzana przez użytkownika, Azure nie push toothem aktualizacje systemu Windows. Jesteś, jednak zaleca tooleave hello automatycznej aktualizacji systemu Windows ustawienie jest włączone. Innym rozwiązaniem jest toodeploy [systemu Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) lub innego produktu odpowiednie zarządzanie aktualizacjami w innej maszyny Wirtualnej lub lokalnymi. Zarówno program WSUS i usługi Windows Update aktualizował maszyny wirtualne. Zalecamy również użycie skanowania tooverify produktu, który wszystkich maszyn wirtualnych IaaS są uruchomione toodate.

Podstawowe obrazy dostarczany przez platformę Azure są regularnie zaktualizowane tooinclude hello najnowszej zaokrąglone aktualizacji systemu Windows. Jednak nie ma żadnej gwarancji, że obrazy hello będzie bieżący w czasie wdrażania. Następujące wersje publicznego niewielkie opóźnienie (of nie więcej niż kilka tygodni) może być możliwe. Wyszukiwanie i instalowanie wszystkich aktualizacji systemu Windows powinna być hello pierwszym krokiem przy każdym wdrożeniu. To jest miara jest szczególnie ważne tooapply podczas wdrażania obrazów, które pochodzą od Ciebie i własnej biblioteki. Obrazy, które są dostarczane jako część hello Azure Marketplace są automatycznie aktualizowane domyślnie.

Organizacje, które nie wymuszają zasady aktualizacji oprogramowania są bardziej narażonych toothreats, które wykorzystują luki w zabezpieczeniach znane, wcześniej stałym. Oprócz tych zagrożeń toocomply z przepisy branżowe dotyczące ryzyka firmy musi udowodnić, że są one wykonywania starannością, oraz za pomocą poprawnych zabezpieczeń formantów toohelp zapewnienia bezpieczeństwa hello ich obciążenie znajduje się w chmurze hello.

Jest ważne tooemphasize, który najlepsze rozwiązania dotyczące tradycyjnymi centrami danych aktualizacji oprogramowania i IaaS platformy Azure ma wiele podobieństw. Dlatego zaleca się dokonanie oceny Twojej bieżącej oprogramowania aktualizacji zasad tooinclude maszyn wirtualnych.

## <a name="manage-your-vm-security-posture"></a>Zarządzanie strukturę bezpieczeństwa maszyny Wirtualnej

Rozwijającymi się zagrożeniami przez i ochrony maszyn wirtualnych wymaga bogate możliwości monitorowania, które może szybko wykrywać zagrożenia, uniemożliwić nieautoryzowany dostęp do zasobów tooyour Wyzwalanie alertów i redukować liczbę fałszywych alarmów. stan zabezpieczeń Hello obciążenia pracą obejmuje wszystkie aspekty zabezpieczeń hello maszyny Wirtualnej, z dostępu do aktualizacji toosecure sieci.

stan zabezpieczeń hello toomonitor Twojego [Windows](../security-center/security-center-virtual-machine.md) i [maszyn wirtualnych systemu Linux](../security-center/security-center-linux-virtual-machine.md), użyj [Centrum zabezpieczeń Azure](../security-center/security-center-intro.md). W Centrum zabezpieczeń Azure można chronić maszyny wirtualne dzięki wykorzystaniu hello następujące możliwości:

* Zastosuj ustawienia zabezpieczeń systemu operacyjnego przy użyciu reguł zalecanych konfiguracji
* Identyfikowanie i Pobierz system zabezpieczeń i aktualizacje krytyczne, które mogą być brakujące
* Wdrażanie zaleceń ochrony przed złośliwym kodem punktu końcowego
* Sprawdź poprawność szyfrowania dysków
* Oceniania i korygowania luk w zabezpieczeniach
* Wykrywania zagrożeń

Centrum zabezpieczeń aktywnie można monitorować w przypadku zagrożeń i potencjalne zagrożenia są widoczne w obszarze **alerty zabezpieczeń**. Skorelowane zagrożenia są agregowane w jednym widoku o nazwie **naruszające**.

toounderstand jak Centrum zabezpieczeń może ułatwić zidentyfikowanie potencjalnych zagrożeń w maszyn wirtualnych znajdujących się na platformie Azure, obejrzyj powitania po wideo:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Organizacje, które nie wymuszają postawie silne zabezpieczenie ich maszyn wirtualnych pozostają bez "świadomości" potencjalnych prób przez nieautoryzowanych użytkowników toocircumvent ustanowić zabezpieczeń formanty.

## <a name="monitor-vm-performance"></a>Monitor wydajności maszyny Wirtualnej

Nadużycia zasobu może to stanowić problem, gdy maszyna wirtualna procesów zużywać więcej zasobów niż powinni. Problemy z wydajnością z maszyny Wirtualnej może prowadzić przerw w działaniu tooservice, który narusza zasady zabezpieczeń hello dostępności. Z tego powodu konieczne toomonitor dostęp maszyny Wirtualnej nie jest tylko rozbudowy, gdy występuje problem, ale również aktywnego względem linii bazowej wydajności mierzony podczas normalnego działania.

Analizując [pliki dzienników diagnostycznych platformy Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), możesz monitorować zasobów maszyny Wirtualnej i zidentyfikuj potencjalne problemy, które mogą negatywnie wpłynąć na wydajność i dostępność. Witaj rozszerzenia diagnostyki Azure udostępnia możliwości monitorowania i diagnostyki na maszynach wirtualnych z systemem Windows. Te funkcje można włączyć w tym rozszerzenia hello jako część hello [szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

Można również użyć [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain wgląd w kondycję Twojego zasobów.

Organizacje, które nie monitorować wydajność maszyny Wirtualnej są toodetermine, czy niektóre zmiany we wzorcach wydajności są prawidłowe lub nieprawidłowe. Jeśli hello wirtualna zużywa więcej zasobów niż zwykle, takie anomalii może wskazywać potencjalny atak z zewnętrznego zasobu lub ze złamanymi zabezpieczeniami procesu uruchomionego w hello maszyny Wirtualnej.
