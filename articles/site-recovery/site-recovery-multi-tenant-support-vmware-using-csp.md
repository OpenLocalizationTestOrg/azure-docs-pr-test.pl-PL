---
title: "Obsługa dzierżawy aaaMulti tooAzure replikacji maszyny Wirtualnej VMware (dostawcy usług Kryptograficznych programu) | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toodeploy usługi Azure Site Recovery w środowisku wielodostępnym tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych VMware tooAzure maszynach wirtualnych (VM) za pośrednictwem hello dostawcy usług Kryptograficznych programu przy użyciu hello portalu Azure"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Obsługa wielu dzierżawców w usłudze Azure Site Recovery replikowanie tooAzure maszyny wirtualne VMware za pośrednictwem dostawcy usług Kryptograficznych

Usługa Azure Site Recovery obsługuje środowiskach wielodostępnych subskrypcji dzierżawcy. Obsługuje ona również wielodostępność dla subskrypcji dzierżawcy, które są tworzone i zarządzane przez program Microsoft Cloud Solution Provider (CSP) hello. W tym artykule szczegółowo hello wskazówki dotyczące wdrażania i zarządzania nimi wielodostępne scenariusze VMware do platformy Azure. Obejmuje ona również tworzenie i zarządzanie subskrypcjami dzierżawy za pośrednictwem dostawcy usług Kryptograficznych.

W tych wskazówkach pobiera silnie z hello istniejąca dokumentacja dotycząca replikowanie tooAzure maszyny wirtualne VMware. Aby uzyskać więcej informacji, zobacz [tooAzure maszyny wirtualne VMware replikacji z usługą Site Recovery](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Środowiska z wieloma dzierżawcami
Istnieją trzy główne modele wielodostępne:

* **Hosting usług dostawcy (HSP) udostępnionych**: hello partnera jest właścicielem hello infrastruktury fizycznej i korzysta z zasobów udostępnionych (vCenter, centrów danych, magazynu fizycznego itd.) toohost maszyn wirtualnych wielu dzierżawców w hello tej samej infrastrukturze. Hello partner można zapewnić odzyskiwania po awarii management jako usługa zarządzana lub hello dzierżawcy mogą być właścicielami odzyskiwania po awarii, jako rozwiązanie samoobsługi.

* **Dostawcy usług hostingu w wersji dedykowanej**: hello partnera, który jest właścicielem hello infrastruktury fizycznej, ale używa zasobów dedykowanych (wiele Vcenter, datastores fizycznych i tak dalej) toohost maszyn wirtualnych każdego dzierżawcy w osobnej infrastruktury. Hello partner można zapewnić odzyskiwania po awarii management jako usługa zarządzana lub hello dzierżawy może posiadać go jako rozwiązaniem samoobsługi.

* **Zarządzane usługi dostawcy (MSP)**: hello infrastruktury fizycznej hostujący maszyny wirtualne hello jest właścicielem powitania klienta i hello partnera umożliwia włączenie odzyskiwania po awarii i zarządzania.

## <a name="shared-hosting-multi-tenant-guidance"></a>Hosting udostępnione wskazówki wieloma dzierżawcami
W tej sekcji omówiono hello udostępnionych hosting scenariusz szczegółowo. Hello innych dwa scenariusze są podzbiorami hello udostępnionych hosting scenariusza i używają hello te same zasady. różnice Hello są opisane na końcu hello hello udostępnionych hosting wskazówki.

Witaj podstawowe wymagania w przypadku wielu dzierżawców jest tooisolate hello różnych dzierżaw. Jeden dzierżawy nie może być tooobserve stanie co hosted innego dzierżawcę. W środowisku zarządzana przez partnera to wymaganie nie jest równie ważne, ponieważ jest on w środowisku samoobsługi, którym może mieć kluczowe znaczenie. We wskazówkach tych założono, że izolacji dzierżawców, jest wymagana.

Architektura Hello są prezentowane w powitania po diagramu:

![Udostępniony HSP z jednego vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Hosting udostępnionych scenariusza z jednym vCenter**

Jak pokazano w hello poprzedzających diagramu, każdy klient ma na serwerze zarządzania oddzielne. Tej konfiguracji dzierżawy limity dostępu tootenant specyficzne dla maszyn wirtualnych i umożliwia izolacji dzierżawców. Scenariusz replikacji maszyn wirtualnych VMware używa hello konfiguracji serwera toomanage kont toodiscover maszyn wirtualnych i zainstaluj agentów. Firma Microsoft wykonaj hello te same zasady w środowiskach wielodostępnych o dodanie hello ograniczenie odnajdywania maszyny Wirtualnej przy użyciu oprogramowania vCenter kontroli dostępu.

wymaganie izolacji danych Hello wymaga tootenants niejawne pozostają wszystkie informacje poufne infrastruktury (na przykład poświadczenia dostępu). Z tego powodu zaleca się pozostawienie wszystkie składniki serwera zarządzania hello pod kontrolą wyłącznego hello hello partnera. składniki serwera zarządzania Hello są:
* Serwer konfiguracji (CS)
* Serwer przetwarzania (PS)
* Główny serwer docelowy (MT) 

PS skalowalnego w poziomie jest również pod kontrolą hello partnera.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Każdy CS w scenariuszu wielodostępne hello używa dwóch kont

- **konto dostępu do vCenter**: korzystać z tej dzierżawy toodiscover konta maszyn wirtualnych. Ma uprawnienia dostępu vCenter przypisane tooit (zgodnie z opisem w następnej sekcji hello). toohelp uniknąć przypadkowego dostępu przecieki, zaleca się, że partnerów wprowadź te same poświadczenia hello narzędzia konfiguracji.

- **Konto dostępu do maszyny wirtualnej**: Użyj tego konta tooinstall hello mobilności agenta hello dzierżawcy maszyn wirtualnych za pomocą wypychania automatycznego. Zazwyczaj jest kontem domeny, czy dzierżawcy może zawierać partnera tooa także, czy też partnera hello może zarządzać bezpośrednio. Jeśli dzierżawcy nie mają szczegóły hello tooshare bezpośrednio z partnerem hello, użytkownik może dozwolone, tooenter hello poświadczeń do ograniczonej czasowo dostępu toohello CS lub przy pomocy partnera hello agentów mobilności ręcznie zainstalować.

### <a name="requirements-for-a-vcenter-access-account"></a>Wymagania dotyczące konta dostępu do vCenter

Jak wspomniano w powyższej sekcji hello, należy skonfigurować hello CS przy użyciu konta mającego tooit specjalne przypisanej roli. Przypisanie roli Hello musi być zastosowany toohello konta dostępu do vCenter dla każdego obiektu vCenter, a nie propagowane toohello obiektów podrzędnych. Ta konfiguracja zapewnia izolacji dzierżawców, ponieważ propagacja dostępu może spowodować przypadkowe uzyskiwanie dostępu do obiektów tooother.

![Witaj opcją obiektów tooChild propagowany](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

alternatywne Hello jest tooassign hello jest konto użytkownika i roli hello obiektu centrum danych i propagować je toohello obiektów podrzędnych. Następnie przyznać hello *dostępu* roli do wszystkich obiektów (np. maszyny wirtualne z innymi dzierżawcami) powinna być tooa niedostępne konkretnym dzierżawy. Ta konfiguracja jest skomplikowane i udostępnia ona kontroli dostępu przypadkowe, ponieważ każdy nowy obiekt podrzędny automatycznie udzielono dostępu, który jest odziedziczone z nadrzędnego hello. Dlatego zaleca się, że używasz hello pierwszym sposobem.

procedury dostępu do konta vCenter Hello jest następujący:

1. Utwórz nową rolę w klonowania hello wstępnie zdefiniowanych *tylko do odczytu* roli, a następnie nadaj nazwę wygodny (na przykład Azure_Site_Recovery, jak pokazano w tym przykładzie).

2. Przypisz następujące uprawnienia roli toothis hello:

    * **Magazyn danych**: przydzielić miejsca, Magazyn danych przeglądania, operacje na plikach niskiego poziomu, usuń plik, pliki aktualizacji maszyny wirtualnej

    * **Sieci**: przypisywanie sieci

    * **Zasób**: przypisanie maszyny Wirtualnej tooresource puli migracji wyłączony z maszyny Wirtualnej, migracji wyłączyć na maszynie Wirtualnej

    * **Zadania**: Tworzenie zadania, zadania aktualizacji

    * **Maszyna wirtualna**: 
        * Konfiguracja > wszystkie
        * Interakcja > odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj dysków CD, konfigurowanie dyskietka, wyłącz zasilanie, zainstaluj narzędzia VMware
        * Spis > Utwórz na podstawie istniejących, Utwórz nowy, zarejestruj, wyrejestrować
        * Inicjowanie obsługi administracyjnej > Zezwalaj na pobieranie maszyny wirtualnej, przekazywanie plików maszyny wirtualnej Zezwalaj
        * Zarządzanie migawkami > Usuń migawki

    ![okno dialogowe Edytuj rolę Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Przypisz konto dostępu do poziomów toohello vCenter (używane w dzierżawie powitalnych CS) dla różnych obiektów, w następujący sposób:

>| Obiekt | Rola | Uwagi |
>| --- | --- | --- |
>| vCenter | Tylko do odczytu | Wymagany tylko vCenter tooallow dostępu do różnych obiektów zarządzania. To uprawnienie można usunąć konta hello nigdy nie będzie toobe dostarczona tooa dzierżawy lub używane dla wszystkich operacji zarządzania na powitania vCenter. |
>| Centrum danych | Azure_Site_Recovery |  |
>| Hosta i hostów klastra. | Azure_Site_Recovery | Ponownie zapewnia, że dostęp jest na poziomie obiektu hello, dzięki czemu dostępne tylko hosty muszą dzierżawione maszyny wirtualne przed trybu failover i po powrotu po awarii. |
>| Magazyn danych i magazynu danych klastra | Azure_Site_Recovery | Taka sama jak poprzedzających. |
>| Sieć | Azure_Site_Recovery |  |
>| Serwer zarządzania | Azure_Site_Recovery | Zawiera składniki tooall dostępu (CS PS i MT), jeśli są poza hello CS maszyny. |
>| Maszyny wirtualne dzierżawcy | Azure_Site_Recovery | Zapewnia, że dowolnej dzierżawy nowych maszyn wirtualnych dzierżawcy określonego także uzyskać dostęp, lub nie będzie wykrywalny przez hello portalu Azure. |

dostęp do konta vCenter Hello jest teraz ukończona. Ten krok w wykonywaniu operacje hello minimalne uprawnienia wymagane toocomplete powrotu po awarii. Można również używać tych uprawnień dostępu z istniejących zasad. Tylko zmodyfikować istniejące uprawnienia zestaw tooinclude uprawnień roli w kroku 2, szczegółowe wcześniej.

toorestrict operacji odzyskiwania po awarii do stanu trybu failover hello (czyli bez możliwości powrotu po awarii), wykonaj hello powyższej procedury z powodu wyjątku: zamiast przypisywać hello *Azure_Site_Recovery* roli konto dostępu do vCenter toohello, przypisz tylko *tylko do odczytu* konta toothat roli. Ten zestaw uprawnień pozwala na replikację maszyny Wirtualnej i trybu failover, a nie zezwala na powrót po awarii. Wszystkie inne elementy w hello poprzedzających procesu pozostaje niezmieniona. tooensure odizolowania dzierżawców i Ogranicz odnajdywanie maszyny Wirtualnej, co uprawnień na poziomie toochild tylko i nie propagowany obiekty hello jest przypisany.

## <a name="other-multi-tenant-environments"></a>Innych środowiskach wielodostępnych

Witaj w powyższej sekcji opisano sposób tooset środowiska wielodostępne udostępnionego rozwiązania hostingu. Witaj dwie główne są inne rozwiązania dedykowanych hosting i zarządzana usługa. Architektura Hello tych rozwiązań jest opisana w hello następujące sekcje.

### <a name="dedicated-hosting-solution"></a>Dedykowane rozwiązania do hostingu

Jak pokazano na powitania po diagramu, architektury różnica dedykowane rozwiązania hostingu hello jest czy infrastruktury każdego dzierżawcy jest skonfigurowany dla tej dzierżawy tylko. Ponieważ dzierżaw są izolowane za pomocą osobnych Vcenter, dostawcy hostingu hello nadal należy wykonać kroki dostawcy usług Kryptograficznych hello przewidzianych udostępniona Usługa hostingu, ale nie jest konieczne tooworry o izolacji dzierżawców. Instalator dostawcy usług Kryptograficznych pozostaje niezmieniona.

![Architektura udostępnione hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Dedykowany hostingu scenariusza z wieloma Vcenter**

### <a name="managed-service-solution"></a>Usługi zarządzane przez rozwiązanie

Hello przedstawiono na poniższym diagramie, hello architektury różnica w rozwiązaniu zarządzanych usług jest infrastruktury każdego dzierżawcy jest również fizycznie oddzielona od innych dzierżaw infrastruktury. W tym scenariuszu zwykle występuje, gdy dzierżawcy hello jest właścicielem hello infrastruktury i chce rozwiązanie odzyskiwania po awarii toomanage dostawcy. Ponownie ponieważ dzierżaw są fizycznie izolowane za pośrednictwem różnych infrastruktur, partnera hello wymaga kroki dostawcy usług Kryptograficznych hello toofollow przewidzianych udostępniona Usługa hostingu, ale nie jest konieczne tooworry o izolacji dzierżawców. Inicjowanie obsługi administracyjnej dostawcy usług Kryptograficznych pozostaje niezmieniona.

![Architektura udostępnione hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Zarządzane usługi scenariusza z wieloma Vcenter**

## <a name="csp-program-overview"></a>Omówienie programu dostawcy usług Kryptograficznych
Witaj [dostawcy usług Kryptograficznych programu](https://partner.microsoft.com/en-US/cloud-solution-provider) zaznajomić razem lepiej scenariuszy, które oferują partnerów wszystkich usług chmurowych firmy Microsoft, w tym usługi Office 365, Enterprise Mobility Suite i Microsoft Azure. Z dostawcy usług Kryptograficznych naszych partnerów właścicielem hello end-to-end relacji z klientami i stają się punkt kontaktu hello podstawowej relacji. Partnerzy można wdrożyć subskrypcji platformy Azure dla klientów i połączyć hello subskrypcji z własnych wartości dodanej, dostosowane oferty.

Z usługą Azure Site Recovery partnerów zarządzać hello kompletne rozwiązanie odzyskiwania po awarii dla klientów bezpośrednio za pośrednictwem dostawcy usług Kryptograficznych. Lub użyj tooset dostawcy usług Kryptograficznych w górę środowisk usługi Site Recovery i umożliwić klientom zarządzanie potrzeb odzyskiwania po awarii w sposób samoobsługi. W obu przypadkach partnerzy to hello łączności między odzyskiwania lokacji i klientów. Partnerzy usługi powitania klienta relacji i obciążania klientów do użycia usługi Site Recovery.

## <a name="create-and-manage-tenant-accounts"></a>Tworzenie i zarządzanie kontami dzierżawy

### <a name="step-0-prerequisite-check"></a>Krok 0: Sprawdzanie wymagań wstępnych

Witaj wymagania wstępne maszyny Wirtualnej są hello taki sam, jak opisano w hello [dokumentacji usługi Azure Site Recovery](site-recovery-vmware-to-azure.md). Dodanie toothose wymagań wstępnych możesz powinny mieć hello kontroli dostępu wymienione wcześniej w miejscu przed przystąpieniem do zarządzania dzierżawy za pośrednictwem dostawcy usług Kryptograficznych. Dla każdego dzierżawcy Utwórz oddzielne serwerem, który może komunikować się z dzierżawą hello maszyn wirtualnych i vCenter partnera. Tylko hello partner ma serwer toothis praw dostępu.

### <a name="step-1-create-a-tenant-account"></a>Krok 1: Tworzenie konta dzierżawy

1. Za pomocą [Microsoft Partner Center](https://partnercenter.microsoft.com/), zaloguj się na koncie dostawcy usług Kryptograficznych tooyour. 
 
2. Na powitania **pulpitu nawigacyjnego** menu, wybierz opcję **klientów**.

    ![łącze klientów Centrum partnerskiego firmy Microsoft Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Na stronie powitania, którego kliknięcie spowoduje otwarcie kliknij hello **klienta Dodaj** przycisku.

    ![przycisk Dodaj klienta Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Na powitania **nowego klienta** , wypełnij szczegółowe informacje dotyczące konta hello hello dzierżawcy, a następnie kliknij przycisk **dalej: subskrypcji**.

    ![Strona informacje o koncie Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Na stronie Wybór subskrypcje hello zaznacz hello **Microsoft Azure** pole wyboru. Można dodać inne subskrypcje teraz lub w dowolnym momencie.

    ![pole wyboru subskrypcji Microsoft Azure Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Na powitania **przeglądu** potwierdzić hello szczegóły dzierżawy, a następnie kliknij przycisk **przesyłania**.

    ![Strona przeglądu Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Po utworzeniu konta dzierżawy hello, zostanie wyświetlona strona potwierdzenia, wyświetlanie szczegółów hello hello domyślne konto i hello hasła dla tej subskrypcji. 

7. Zapisz informacje hello i Zmień hasło hello później w razie potrzeby za pośrednictwem hello Azure portalu strony logowania.  
 
    Te informacje można udostępniać dzierżawy hello jest lub można tworzyć i udostępniać oddzielne konto, jeśli jest to konieczne.

### <a name="step-2-access-hello-tenant-account"></a>Krok 2: Dostęp do konta dzierżawy hello

Dostępne subskrypcji dzierżawy hello za pośrednictwem hello pulpit nawigacyjny Centrum partnerskiego firmy Microsoft, zgodnie z opisem w "krok 1: utworzenie konta dzierżawy." 

1. Przejdź toohello **klientów** strony, a następnie kliknij nazwę hello hello konta dzierżawy.

2. Na powitania **subskrypcje** strony hello konta dzierżawy, można monitorować hello istniejącego konta subskrypcji i dodawać więcej subskrypcji, zgodnie z wymaganiami. Wybierz toomanage hello dzierżawy operacji odzyskiwania po awarii, **wszystkie zasoby (Azure portal)**.

    ![Wszystkie zasoby Hello link](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Kliknięcie przycisku **wszystkie zasoby** udziela dostępu dzierżawcy toohello subskrypcji platformy Azure. Dostęp można sprawdzić, klikając łącze usługi Azure Active Directory hello na powitania górnego prawego hello portalu Azure.

    ![Azure Active Directory łącza](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

Można teraz wykonywać wszystkie operacje usługi site recovery dla dzierżawcy hello za pośrednictwem hello portalu Azure i zarządzać hello operacji odzyskiwania po awarii. tooaccess hello subskrypcji dzierżawy za pośrednictwem dostawcy usług Kryptograficznych dla odzyskiwania po awarii zarządzanych hello wykonaj opisane wcześniej procesu.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Krok 3: Wdrażanie subskrypcji dzierżawy toohello zasobów
1. Na powitania portalu Azure Utwórz grupę zasobów, a następnie wdrożyć na proces zwykle hello magazynu usług odzyskiwania. 
 
2. Pobierz klucz rejestracji magazynu hello.

3. Zarejestruj CS hello hello dzierżawcy przy użyciu klucza rejestracji magazynu hello.

4. Wprowadź poświadczenia hello hello dwa konta dostępu do: maszyny Wirtualnej i vCenter konto dostępu do uzyskania dostępu do konta.

    ![Kont serwera configuration Manager](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Krok 4: Magazyn usług odzyskiwania toohello infrastruktura usługi Site Recovery rejestru i
1. W portalu Azure na hello magazynu, który został utworzony wcześniej hello, zarejestruj hello vCenter server toohello CS, który został zarejestrowany w "krok 3: Wdrażanie subskrypcji dzierżawy toohello zasobów." W tym celu należy użyć konta dostępu do hello vCenter.
2. Zakończ proces "Przygotowanie infrastruktury" hello Site Recovery na powitania zwykle proces.
3. maszyny wirtualne Hello są teraz gotowe toobe replikowane. Sprawdź, czy tylko hello maszyn wirtualnych dzierżawcy są wyświetlane na powitania **wybierz maszyny wirtualne** bloku w obszarze hello **replikować** opcji.

    ![Listy maszyn wirtualnych dzierżawcy na powitania bloku wybierz maszyny wirtualne](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Krok 5: Przypisz dzierżawy dostępu toohello subskrypcji

Do odzyskiwania awaryjnego samoobsługi, zapewnia toohello dzierżawcy hello szczegóły konta, jak wspomniano w kroku 6 hello "krok 1: utworzenie konta dzierżawy" sekcji. Tę akcję można wykonać po partnera hello konfiguruje hello infrastruktury odzyskiwania po awarii. Czy hello typu odzyskiwania po awarii jest zarządzane lub samoobsługi, partnerzy muszą uzyskać dostęp do subskrypcji dzierżawcy za pośrednictwem portalu dostawcy usług Kryptograficznych hello. Konfigurowanie magazynu należących do partnera hello, a zarejestrować subskrypcji dzierżawcy toohello infrastruktury.

Partnerzy także dodać nową subskrypcję dzierżawy toohello użytkownika za pośrednictwem portalu dostawcy usług Kryptograficznych hello hello następujący:

1. Przejdź na stronę subskrypcji dzierżawcy toohello dostawcy usług Kryptograficznych, a następnie wybierz hello **użytkownicy i licencje** opcji.

    ![Witaj stronę subskrypcji dzierżawcy dostawcy usług Kryptograficznych](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    Teraz można utworzyć nowego użytkownika, wprowadzając odpowiednie dane hello i wybierając uprawnienia lub przekazując hello listy użytkowników w pliku CSV.

2. Po utworzeniu nowego użytkownika, przejdź wstecz toohello Azure portalu, a następnie na powitania **subskrypcji** bloku, wybierz hello odpowiednich subskrypcji.

3. W bloku hello, który zostanie otwarty, wybierz **kontroli dostępu (IAM)**, a następnie kliknij przycisk **Dodaj** tooadd użytkownika z poziomu dostępu odpowiednich hello.      
    Hello użytkowników, które zostały utworzone za pośrednictwem portalu dostawcy usług Kryptograficznych hello są automatycznie wyświetlane w bloku hello, który zostanie otwarty po kliknięciu poziom dostępu.

    ![Dodawanie użytkownika](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Dla większości operacji zarządzania, hello *współautora* roli jest wystarczająca. Użytkownicy z poziomu tego dostępu może robić wszystko to w przypadku subskrypcji, z wyjątkiem zmiana poziomów dostępu (dla którego *właściciela*— wymagany jest dostęp do poziomu). Można również dostosować hello poziomów dostępu zgodnie z wymaganiami.
