---
title: aaaGovernance na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub przedsiębiorstwa."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Zarządzanie w systemie Azure

Wiemy, że zabezpieczeń jest jednego zadania w chmurze hello i jak ważne jest aby znaleźć dokładne i aktualne informacje na temat zabezpieczeń platformy Azure. Jednym z hello najlepsze toouse powodów Azure dla usług i aplikacji jest tootake zaletą jego szerokiej gamy narzędzi zabezpieczeń i możliwości. Te narzędzia i funkcje dzięki możliwości toocreate bezpiecznych rozwiązań na powitania bezpiecznej platformie Azure.

toohelp, który lepiej zrozumieć tablicy hello formantów ładu zaimplementowana w systemie Microsoft Azure z obu powitania klienta i perspektyw operacji firmy Microsoft, w tym artykule "Zarządzanie w Azure", jest zapisywany zapewniający kompleksowe przyjrzeć się hello Zarządzanie funkcji dostępnych w systemie Microsoft Azure.

## <a name="azure-platform"></a>Platforma Azure

Azure to platforma usługi chmury publicznej, która obsługuje szeroki wybór systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń. Kontenery systemu Linux można uruchamiać z integracji dokerskie; Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js; Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń. Usługi w chmurze publicznej Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas tworzenia lub migracji zasobów informatycznych do dostawcy usług chmury publicznej, są zależne tooprotect możliwości w organizacji, aplikacji i danych za pomocą usługi hello i formanty hello zapewniają toomanage hello bezpieczeństwa sieci opartej na chmurze zasoby.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą spełnić ich wymagań dotyczących zabezpieczeń. Ponadto Azure udostępnia wiele opcji zabezpieczeń i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożenia w organizacji.

Ten dokument pomaga zrozumieć, jak możliwości zarządzania Azure można spełnić te wymagania.

## <a name="abstract"></a>Abstrakcyjny

Zarządzanie chmury Microsoft Azure oferuje zintegrowane inspekcji i konsultingowe podejście do sprawdzenia i udzielanie porad organizacji na ich użycie hello platformy Azure. Ładu chmury Microsoft Azure odnosi się procesów decyzyjnych toohello, kryteriów i zasadami zaangażowane w hello planowania, architektura, nabycia, wdrażania, działania i zarządzania chmury obliczeniowej.

toocreate plan ładu chmury Microsoft Azure, należy tootake omówiono hello osób, procesów i technologii obecnie w miejscu, a następnie struktur kompilacji, które ułatwiają IT tooconsistently obsługuje potrzeb biznesowych, zapewniając zakończenia Użytkownicy z hello elastyczność toouse hello zaawansowanych funkcji programu Microsoft Azure.

W tym dokumencie opisano, jak można uzyskać z podwyższonym poziomem uprawnień poziom zarządzania zasobami IT na platformie Microsoft Azure. W tym dokumencie pomogą zrozumieć funkcje zabezpieczeń i zarządzania hello wbudowane tooMicrosoft Azure.

Hello poniżej przedstawiono główne hello ładu problemów omówione w tym dokumencie:

- Implementacja zasad, procesów i procedur zgodnie z harmonogramem cele organizacji.

- Bezpieczeństwo i ciągłe zgodności ze standardami w organizacji

- Monitorowanie i alerty

## <a name="implementation-of-policies-processes-and-procedures"></a>Stosowania zasad, procesów i procedur 

Zarządzania nawiązał role i obowiązki toooversee stosowania zasad zabezpieczeń informacji hello i ciągłości w obrębie platformy Azure. Interfejs Microsoft Azure management jest odpowiedzialny za nadzór nad zabezpieczeń i ciągłości rozwiązań w ramach ich odpowiednich zespołów (takie jak stron trzecich) i ułatwienie przestrzegania zasad zabezpieczeń, procesów i standardów.

Poniżej przedstawiono czynniki hello ewoluował:

- Aprowizacja kont

- Formanty subskrypcji

- Kontroli dostępu na podstawie roli

- Zarządzanie zasobami

- Śledzenie zasobów

- Kontrola krytyczne zasobów

- Dostępu do interfejsu API tooBilling informacji

- Formanty sieci

## <a name="account-provisioning"></a>Aprowizacja kont

Definiowanie konta hierarchii jest ważny krok toouse i struktura usług platformy Azure w obrębie firmy i strukturę zarządu hello core. W przypadku klientów z umową enterprise hello klienci dalsze można podzielić hello środowiska do działów, kont, a na końcu subskrypcji.

![Aprowizacja kont](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Jeśli nie ma umowy enterprise agreement, rozważ użycie [Azure tagi](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) w hierarchii toodefine poziomu subskrypcji. Subskrypcja platformy Azure to podstawowa jednostka hello, gdzie znajdują się wszystkie zasoby. Definiuje również kilka ograniczeń w obrębie platformy Azure, takich jak liczba rdzeni, zasoby itd. Subskrypcje mogą zawierać [grup zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), które zawierają zasoby. [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) zasady stosowane na te trzy poziomy.

Co przedsiębiorstwa jest inna i hello hierarchii przy użyciu tagów Azure w przypadku klientów z systemem innym niż enterprise umożliwia dużą swobodę w sposób organizowania Azure w ramach hello firmy. Przed wdrożeniem zasobów na platformie Microsoft Azure, możesz hierarchii i zrozumieć wpływ hello na rozliczenia, dostęp do zasobów i złożoności.

## <a name="subscription-controls"></a>Formanty subskrypcji

Subskrypcji kontroluje sposób zgłoszone i rozliczane użycia zasobów. Subskrypcje można skonfigurować oddzielne rozliczeń i płatności. Wymienione wcześniej w jednym konta Azure firma Microsoft może mieć wiele subskrypcji. Subskrypcje mogą być używane toodetermine hello zasobów platformy Azure użycie wielu działów w firmie.

Na przykład, jeśli firma ma IT, działów HR i marketingu i działów te mają różnych projektów uruchomiona. Na podstawie hello użycia zasobów platformy Azure, takich jak maszyn wirtualnych przez każdy dział one może rozliczony odpowiednio. To firma Microsoft może kontrolować każdego działu finansów hello.

Subskrypcje platformy Azure nawiązać trzy parametry:

- Identyfikator unikatowy subskrybenta

- Lokalizacja rozliczeń

- Zbiór dostępnych zasobów

Osoba, która będzie obejmować jeden identyfikator konta Microsoft, karta kredytowa numer i hello pełny pakiet Azure usług — mimo że Microsoft wymusza ograniczenia użycia, w zależności od typu subskrypcji hello.

Hierarchie Azure rejestracji zdefiniuj struktury usług w ramach umowy Enterprise Agreement. Witaj Enterprise Portal umożliwia klientom toodivide dostęp do tooAzure zasobów skojarzonych z umowy Enterprise Agreement, oparte na hierarchii elastyczne dostosowywalne tooan unikatowy potrzeb organizacji. wzorzec hierarchii Hello powinna być zgodna zarządzania i geograficzne struktury organizacji tak, aby hello skojarzone rozliczeń i dostęp do zasobów może być dokładnie rejestrowana.

Hello trzech wzorców wysokiego poziomu są jednostki funkcjonalności, biznesowe i geograficzne, korzystanie z działów jako konstrukcję administracyjne dla konta grupy. W ramach każdego działu kont można przypisać subskrypcji, których tworzenie silosów rozliczeń i kilka ograniczeń klucza na platformie Azure (np. liczbę maszyn wirtualnych, kont magazynu, itp.).

![Formanty subskrypcji](./media/governance-in-azure/security-governance-in-azure-fig2.png)


W przypadku organizacji z umową Enterprise subskrypcji platformy Azure, wykonaj czterech poziomu hierarchii:

- administrator przedsiębiorstwa rejestracji

- administratorem działu

- Właściciel konta

- Administrator usługi

Ta hierarchia reguluje hello poniżej:

- Relacja rozliczeń

- Administracja konta

- Rola tooartifacts kontroli dostępu na podstawie (RBAC)

- Granice/limity

- Granice

  - Użycie i rozliczenia (oparte na numery oferta karta szybkość)

  - Limity

  - Virtual Network

- Dołączony too1 AAD (1 AAD być skojarzone z wielu subskrypcji)

- Konto rejestracji enterprise skojarzone tooan

## <a name="role-based-access-controls"></a>Kontrola dostępu oparta na rolach

Gdy Azure pierwotnie został wydany, dostęp do formantów tooa subskrypcji zostały podstawowe: administratorem ani Współadministratorem. Dostęp do subskrypcji tooa hello klasycznego modelu niejawnego dostępu tooall hello zasobów w portalu hello. Ten brak szczegółową kontrolę przeprowadzony toohello mnożenie tooprovide subskrypcje poziom kontroli dostępu uzasadnione rejestracji Azure.

![Kontrola dostępu oparta na rolach](./media/governance-in-azure/security-governance-in-azure-fig3.png)

Mnożenie tej subskrypcji nie jest już potrzebne. Przy użyciu kontroli dostępu opartej na rolach można przypisywać użytkowników ról toostandard (na przykład typowe "czytnika" i "writer" typy ról). Można również zdefiniować role niestandardowe.

[Azure opartej na rolach kontroli dostępu (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Przy użyciu funkcji RBAC, można udzielić tylko hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań. Nastawionych zabezpieczeń skoncentrować się nadanie uprawnień dokładne hello potrzebnych im pracowników. Za dużo uprawnienia ujawnia tooattackers konta. Za mało uprawnienia oznacza, że pracownicy nie można pobrać ich pracować wydajnie. Azure opartej na rolach kontroli dostępu (RBAC) pomaga rozwiązać ten problem, oferując precyzyjne zarządzanie dostępem dla platformy Azure. RBAC ułatwia toosegregate opłat w ramach Twojego zespołu i przyznać tylko hello ilość toousers dostępu, że powinni tooperform swoich zadań. Zamiast nadanie każdy nieograniczonych uprawnień w Twojej subskrypcji platformy Azure lub zasobów, można zezwolić tylko pewne akcje.

Na przykład użyj RBAC toolet jednego pracownika zarządzania maszynami wirtualnymi w ramach subskrypcji, podczas gdy inny można zarządzać baz danych SQL w ramach hello takie same subskrypcji.

Azure RBAC ma trzy podstawowe role dotyczące typów zasobów tooall:

- **Właściciel** ma pełny dostęp tooall zasobów, w tym hello toodelegate prawo dostępu tooothers.

- **Współautor** można tworzyć i zarządzania wszystkimi typami zasobów platformy Azure, ale nie może udzielić dostępu tooothers.

- **Czytnik** można wyświetlić istniejących zasobów platformy Azure.

Zezwalaj na zarządzanie określonych zasobów platformy Azure Hello pozostałe role RBAC hello na platformie Azure. Na przykład hello roli współautora maszyny wirtualnej umożliwia hello toocreate użytkowników i zarządzania maszynami wirtualnymi. Nie daje im sieci wirtualnej toohello dostępu lub łączy się z podsieci hello, która hello maszyny wirtualnej.

[Wbudowane role RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) list hello ról dostępnej na platformie Azure. Określa operacje hello i że każdy wbudowana rola przyznaje toousers zakresu.

Udziel dostępu przypisując hello odpowiednie RBAC roli toousers, grup i aplikacji w określonego zakresu. Witaj zakres przypisania roli może być pojedynczego zasobu, grupy zasobów lub subskrypcji. Rola przypisana w zakresie nadrzędnej również udziela dostępu toohello dzieci w nim zawarte.

Na przykład użytkownika z grupy zasobów tooa dostępu może zarządzać wszystkie zasoby hello, który zawiera, takie jak witryny sieci Web, maszyn wirtualnych i podsieci.

Azure RBAC tylko operacje zarządzania obsługuje hello zasobów platformy Azure w hello portalu Azure i interfejsów API usługi Azure Resource Manager. Nie można go autoryzacji wszystkie operacje poziomu danych zasobów platformy Azure. Można na przykład ktoś toomanage kont magazynu, ale nie toohello obiektów blob lub tabel w ramach konta magazynu nie może autoryzować. Podobnie bazy danych SQL mogą być zarządzane, ale nie hello tabel znajdujące się w nim.

Jeśli chcesz uzyskać więcej szczegółowych informacji na temat sposobu, w jaki RBAC ułatwia zarządzanie dostępem, zobacz [Co to jest kontrola dostępu oparta na rolach](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).

Możesz również [utworzyć niestandardową rolę](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) based kontroli dostępu (RBAC), jeśli żadna hello wbudowanych ról nie spełnia określonych dostęp wymaga. Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure interfejsu wiersza polecenia (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli)i hello [interfejsu API REST](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Podobnie jak wbudowane role można przypisywać role niestandardowe toousers, grup i aplikacji w subskrypcji, grupy zasobów i zakresy zasobów.

W ramach każdej subskrypcji można przyznać się too2000 przypisań ról.

## <a name="resource-management"></a>Zarządzanie zasobami

Dostarczana przez platformę Azure pierwotnie tylko hello klasycznego modelu wdrażania. W tym modelu każdy zasób istniał niezależnie; nie było możliwości wykonania toogroup ze sobą powiązane zasoby. Zamiast tego miał toomanually śledzenie zasobów, które składają się rozwiązania lub aplikacji i Zapamiętaj toomanage w skoordynowany sposób podejście.

toodeploy rozwiązania, trzeba było tooeither tworzenie każdego zasobu indywidualnie za pośrednictwem portalu klasycznego hello lub utworzyć skrypt, który wdrożony wszystkie zasoby hello w odpowiedniej kolejności hello. toodelete rozwiązania, trzeba było toodelete każdego zasobu pojedynczo. Nie można zastosować i zaktualizuj zasady kontroli dostępu dla powiązanych zasobów. Ponadto nie można zastosować tagi tooresources toolabel je za pomocą warunków, które ułatwiają monitorowanie zasobów i Zarządzanie rozliczeniami.

W 2014 r. Azure wprowadzono Menedżera zasobów dodane koncepcji hello grupy zasobów. Grupa zasobów to kontener dla zasobów, które mają wspólne cyklu życia. model wdrażania Hello Resource Manager zapewnia kilka korzyści:

- Można wdrażania, zarządzania i monitorowania wszystkich usług hello do rozwiązania jako grupę, a nie pojedynczo obsługi tych usług.

- Można wielokrotnie wdrażania rozwiązania przez cały cykl życia i mieć pewność, zasoby są wdrażane w spójnym stanie.

- Dostęp do zasobów tooall formant można zastosować w grupie zasobów, a te zasady są stosowane automatycznie, gdy dodawane są nowe zasoby, grupy zasobów toohello.

- Możliwość dodawania tagów tooresources toologically organizowanie wszystkie zasoby hello w ramach subskrypcji.

- Infrastruktura hello toodefine JavaScript Object Notation (JSON) można użyć dla rozwiązania. Plik JSON Hello jest nazywany szablonem usługi Resource Manager.

- Można zdefiniować hello zależności między zasobami w celu wdrażania ich w odpowiedniej kolejności hello.

![Zarządzanie zasobami](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Menedżer zasobów umożliwia tooput zasobów w łatwy do rozpoznania grupy zarządzania, koligacji rozliczeń lub fizycznych. Jak wspomniano wcześniej, platforma Azure ma dwa modele wdrażania. W starszych hello [klasycznego modelu](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), hello podstawową jednostką zarządzania został hello subskrypcji. Był trudny toobreak dół zasobów w ramach subskrypcji, które spowodowało utworzenie toohello dużą liczbę subskrypcji. Z modelu Resource Manager hello widzieliśmy wprowadzenie hello grup zasobów.

Grupa zasobów jest kontenerem, który zawiera powiązane zasoby Azure rozwiązania. [Grupa zasobów Hello](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) mogą obejmować wszystkie zasoby hello hello rozwiązania lub tylko tych zasobów, które mają toomanage jako grupa. Możesz zdecydować, jak zasoby tooallocate tooresource grupy oparte na to, co sprawia, że hello najbardziej odpowiednie dla Twojej organizacji.

Aby uzyskać zalecenia dotyczące szablonów, zobacz [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) (Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager).

Usługa Azure Resource Manager analizuje zależności tooensure zasoby są tworzone we właściwej kolejności hello. Jeśli jeden zasób opiera się na wartości z innego zasobu (na przykład maszyna wirtualna wymagająca konta magazynu na potrzeby dysków), ustawiana jest zależność.

>[!Note]
>Aby uzyskać więcej informacji, zobacz [Defining dependencies in Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies) (Definiowanie zależności w szablonach usługi Azure Resource Manager).

Umożliwia także szablonu hello infrastruktury toohello aktualizacji. Można na przykład dodać rozwiązanie tooyour zasobów i dodać reguły konfiguracji hello zasobów, które są już wdrożone. Jeśli szablon hello określa tworzenie zasobu, ale ten zasób już istnieje, usługi Azure Resource Manager przeprowadzi aktualizację, zamiast tworzyć nowy zasób. Azure Resource Manager aktualizacje hello istniejących zasobów toohello sam stan, ponieważ byłaby nowego.

Resource Manager zapewnia rozszerzenia dla scenariuszy, gdy potrzebne są dodatkowe operacje, takie jak instalowanie oprogramowania, które nie są uwzględnione w Instalatorze hello.

## <a name="resource-tracking"></a>Śledzenie zasobów

Jak użytkownicy w Twojej organizacji Dodaj subskrypcję toohello zasobów, staje się coraz bardziej ważne tooassociate zasoby z hello odpowiednie dział, klientów i środowisko. Możesz dołączyć tooresources metadanych za pomocą tagów. Możesz użyć [tagi](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide informacji na temat zasobów hello lub hello właściciela. Znaczniki umożliwiają toonot tylko agregacji i grupy zasobów na kilka sposobów, ale użyć tych danych na potrzeby hello obciążenia zwrotnego.

Używaj tagów po złożonych kolekcji grup zasobów i zasobów oraz muszą toovisualize tych zasobów w hello sposób hello większości tooyou znaczeniu. Na przykład znakować zasoby, które pełnią podobną rolę w organizacji lub należą toohello samego działu.

Bez tagów, użytkownicy w organizacji można utworzyć wiele zasobów, które mogą być trudne toolater identyfikowania i zarządzania nim. Na przykład możesz toodelete wszystkie zasoby hello w projekcie. Jeśli te zasoby nie są oznaczone dla projektu hello, użytkownik musi je znaleźć ręcznie. Tagowanie może być istotnym sposobem tooreduce niepotrzebnych kosztów w ramach subskrypcji.

Zasoby nie są tooreside w hello tego samego zasobu grupy tooshare tag. Możesz utworzyć własne tooensure taksonomii tag, że wszyscy użytkownicy w organizacji używać typowych tagów zamiast użytkowników przypadkowo stosowania nieco inne tagów (na przykład "Wydział" zamiast "dział").

Zasady zasobów Włącz toocreate standardowe reguły dla Twojej organizacji. Można utworzyć zasad, które upewnij się, że zasoby są oznaczane hello odpowiednie wartości.

> [!Note]
> Aby uzyskać więcej informacji, zobacz [stosowania zasad zasobów dla tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

Można również wyświetlić oznakowanych zasobów za pomocą hello portalu Azure.

Witaj [raport użycia](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) dla Twoja subskrypcja obejmuje tag nazwy i wartości, co pozwala toobreak limit koszty według znaczników.

> [!Note]
> Aby uzyskać więcej informacji na temat tagów, zobacz [używanie tagów tooorganize zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Witaj następujące ograniczenia mają zastosowanie tootags:

- Każdy zasób lub grupa zasobów może mieć co najwyżej 15 pary klucz wartość tagu. To ograniczenie dotyczy tylko grupy zasobów toohello tootags bezpośrednio stosowane lub zasobu. Grupa zasobów może zawierać wiele zasobów, że mieć 15 pary klucz wartość tagu.

- Nazwa tagu Hello jest ograniczona too512 znaków.

- Wartość tagu Hello jest ograniczona too256 znaków.

- Grupa zasobów toohello znaczniki zastosowane nie są dziedziczone przez hello zasobów w danej grupie zasobów.

Jeśli masz więcej niż 15 wartości potrzebnych tooassociate z zasobem, użyj ciągu JSON hello wartości tagu. Witaj ciągu JSON może zawierać wiele wartości, które są stosowane tooa jeden tag klucza.

### <a name="tags-and-billing"></a>Znaczniki i rozliczeń

Tagi włączyć możesz toogroup danych rozliczeń. Na przykład jeśli używasz wielu maszyn wirtualnych w różnych organizacjach użycie hello tagi toogroup przez Centrum kosztów. Umożliwia także koszty toocategorize tagi przez środowisko uruchomieniowe; takie jak hello rozliczeń użycia dla maszyn wirtualnych w środowisku produkcyjnym.

Można pobrać informacji na temat tagów za pośrednictwem hello [użycia zasobów platformy Azure i interfejsów API RateCard](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) lub pliku wartości rozdzielanych przecinkami (CSV) użycia hello. Pobieranie pliku użycia hello z hello [portalu konta usługi Azure](https://account.windowsazure.com/) lub [EA portal](https://ea.azure.com/).

>[!Note]
> Aby uzyskać więcej informacji o dostęp programistyczny toobilling informacji, zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Dla operacji interfejsu API REST, zobacz [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Po pobraniu hello użycia woluminów CSV dla usług, które obsługują tagów z rozliczeniami tagi hello pojawiają się w kolumnie tagi hello.

## <a name="critical-resource-controls"></a>Formanty krytycznego zasobu

Jak organizacji dodaje core services toohello subskrypcji, staje się coraz bardziej ważne tooensure, czy te usługi są dostępne tooavoid firm przerw w działaniu. [Blokowania zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) pozwalają operacji toorestrict zasobów wysokiej wartości, których modyfikowania lub usuwania ich miałoby znaczący wpływ na aplikacje lub infrastruktury chmury. Możesz zastosować blokad tooa subskrypcji, grupy zasobów lub zasobów. Zazwyczaj należy zastosować blokad toofoundational zasoby, takie jak sieci wirtualnych, bramy i kont magazynu.

Blokowania zasobów obsługuje obecnie dwie wartości: CanNotDelete i tylko do odczytu. CanNotDelete oznacza, że użytkownikom (hello odpowiednie prawa) można nadal odczytywać lub zmodyfikuj zasobu, ale nie można go usunąć. Tylko do odczytu oznacza, że autoryzowani użytkownicy nie można usunąć ani zmodyfikować zasobu.

Menedżer zasobów blokad zastosować tylko toooperations to zrobić w płaszczyźnie zarządzania hello, która składa się z operacji wysłany<https://management.azure.com>. hello blokad nie ograniczają jak zasoby wykonywanie własnych funkcji. Zmiany zasobu jest ograniczony, ale operacje zasobów nie są ograniczone. Na przykład blokady w bazie danych SQL tylko do odczytu uniemożliwia usuwanie lub modyfikowanie hello bazy danych, ale nie uniemożliwiać tworzenie, aktualizowanie lub usuwanie danych hello bazy danych.

Stosowanie **tylko do odczytu** może prowadzić toounexpected wyników, ponieważ niektóre operacje, które się wydawać odczytu operacje wymagają dodatkowych czynności. Na przykład wprowadzenie **tylko do odczytu** blokady na koncie magazynu uniemożliwia wyświetlanie kluczy hello wszystkich użytkowników. Lista Hello operacji kluczy jest obsługiwana za pomocą żądania POST, ponieważ hello zwrócił się, że klucze są dostępne do zapisu.

![Formanty krytycznego zasobu](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Innym przykładem wprowadzenie blokady tylko do odczytu na zasób usługi aplikacji — uniemożliwia Eksploratora serwera w usłudze Visual Studio wyświetlanie plików hello zasobu, ponieważ interakcji wymaga dostępu do zapisu.

W przeciwieństwie do kontroli dostępu opartej na rolach możesz użyć tooapply blokady zarządzania ograniczenie we wszystkich użytkowników i ról. toolearn o ustawianiu uprawnień dla użytkowników i ról, zobacz [kontroli dostępu opartej na roli Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Po zastosowaniu blokady w zakresie nadrzędnym, wszystkie zasoby w tym zakresie dziedziczą hello tego samego blokady. Nawet zasoby, które później zostaną dodane Dziedzicz blokady hello hello nadrzędnej. Witaj najbardziej restrykcyjne blokady w dziedziczeniu hello pierwszeństwo.

toocreate lub usunięcia blokady zarządzania, musi mieć dostęp tooMicrosoft.Authorization/ _lub Microsoft.Authorization/locks/_ akcje. Witaj wbudowanych ról, tylko **właściciela** i **Administrator dostępu użytkowników** otrzymują te akcje.

## <a name="api-access-toobilling-information"></a>Informacje o toobilling dostępu interfejsu API

Za pomocą interfejsów API usługi Azure rozliczeń toopull danych użycia i zasobów do narzędziami analizy danych preferowany. Hello użycia zasobów platformy Azure i interfejsów API RateCard może pomóc dokładnie przewidzieć i zarządzanie nimi kosztów. Witaj interfejsy API są zaimplementowane jako dostawca zasobów i część hello interfejsów API udostępnianych przez hello Azure Resource Manager.

### <a name="azure-resource-usage-api-preview"></a>Użycie zasobów platformy Azure, interfejsu API (wersja zapoznawcza)

Użyj hello Azure [API użycia zasobów](https://msdn.microsoft.com/library/azure/mt219003) tooget danych szacowany wykorzystania platformy Azure. obejmuje Hello interfejsu API:

- **Azure kontroli dostępu opartej na rolach** — Konfigurowanie dostępu zasad na powitania [portalu Azure](https://portal.azure.com/) lub za pomocą [poleceń cmdlet programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) toospecify użytkowników lub aplikacji, które mogą uzyskać dostęp dane użycia toohello subskrypcji. Obiekty wywołujące należy użyć standardowego tokeny usługi Azure Active Directory do uwierzytelniania. Dodaj hello wywołującego tooeither hello czytnika rozliczeń, czytelnika, właścicielem lub współautorem roli tooget toohello dane użycia dostępu dla określonej subskrypcji platformy Azure.

- **Co godzinę lub agregacje codzienne** — wywołań można określić, czy chcą ich danych użycia usługi Azure co godzinę pakiety w ramach Agreement lub pakiety codziennie w ramach Agreement. Domyślnie Hello jest codziennie.

- **Wystąpienie metadanych (w tym tagi zasobów)** — Pobierz szczegóły na poziomie wystąpienia takich jak hello identyfikatora uri zasobu w pełni kwalifikowana (/subscriptions/ {identyfikator subskrypcji} /..), hello informacji o grupie zasobów i tagi zasobów. Te metadane pomaga w sposób niejednoznaczny i programowo przydzielenie użycia tagów hello, przypadków użycia, takich jak między ładowania.

- **Metadane zasobu** — szczegóły zasobów, takie jak nazwa licznika hello, kategoria licznika podkategorii miernika, jednostki i region zapewniają wywołującego hello lepiej zrozumieć co został wykorzystany. Naszym celem jest również terminologii metadanych zasobów tooalign hello portalu Azure, Azure użycia woluminów CSV, EA CSV, rozliczeń i inne środowiska publicznych toolet korelowania danych na środowiska.

- **Użycia dla wszystkich oferują typy** — danych użycia jest dostępna dla wszystkich oferują typy jak płatność za rzeczywiste użycie, MSDN, zobowiązania pieniężnego, środki pieniężne i atrybutów Rozszerzonych.

**Zasobów platformy Azure RateCard interfejsu API (wersja zapoznawcza)**

Użyj hello interfejsu API usługi Azure Resource RateCard tooget hello listę dostępnych zasobów platformy Azure i szacowane ceny dla każdego. obejmuje Hello interfejsu API:

- **Kontrola dostępu oparta na rolach Azure** — Konfigurowanie zasad dostępu na powitania portalu Azure lub za pośrednictwem toospecify poleceń cmdlet programu Azure PowerShell, który użytkowników lub aplikacji można uzyskać dostęp do danych RateCard toohello. Obiekty wywołujące należy użyć standardowego tokeny usługi Azure Active Directory do uwierzytelniania. Dodaj hello wywołującego tooeither hello czytnika, właścicielem lub współautorem roli tooget toohello dane użycia dostępu dla określonej subskrypcji platformy Azure.

- **(Nie obsługiwany EA) oferuje obsługę płatność za rzeczywiste użycie, MSDN, zobowiązań i środki pieniężne** — ten interfejs API zawiera informacje o szybkości poziomu oferty Azure. obiekt wywołujący Hello tego interfejsu API musi upłynąć w szczegóły zasobu tooget hello oferta informacji i szybkości. Jesteśmy stawki EA tooprovide aktualnie nie, ponieważ EA oferty zostały dostosowane stawki dla rejestracji. Oto niektóre scenariusze hello, które są możliwe z kombinacją hello hello użycia i hello RateCard interfejsów API:

- **Azure spędzają w miesiącu hello** -miesiącach hello spędzają na użycie hello kombinację hello użycia i interfejsów API RateCard tooget lepsze wgląd w chmurze. Można analizować hello co godzinę i oszacowania zasobników codziennego użycia i opłat.

- **Konfigurowanie alertów** — hello użycia i hello tooget RateCard interfejsów API Szacowane użycie w chmurze i opłat, skonfigurować alerty oparte na zasobach lub pieniężne na podstawie.

- **Przewidywanie rachunku** — Get szacowane zużycie i w chmurze spędzają i zastosować machine learning toopredict algorytmy faktury jakie hello byłoby na końcu hello hello cyklu rozliczeniowym.

- **Wstępne zużycia koszt analizy** — Użyj toopredict RateCard API hello ile rachunku byłby przez użycie oczekiwanej w przypadku przenoszenia tooAzure Twojego obciążeń. Jeśli masz istniejące obciążenia w innych chmur lub chmur prywatnych, możesz mapować użycie z hello Azure stawki tooget spędzają lepiej oszacować platformy Azure. Dzięki temu szacowania hello toopivot możliwości oferowanych i porównania pomiędzy typami inną ofertę hello poza płatność za rzeczywiste użycie, takie jak zobowiązań i środki pieniężne. Witaj interfejsu API umożliwia także hello możliwości toosee koszt różnice według regionu i pozwala toodo toohelp analizy warunkowej kosztów, wprowadzeniu decyzji dotyczących wdrożenia.

- **Analizy warunkowej** — można określić, czy jest ono więcej obciążeń ekonomicznego toorun w innym regionie lub w innej konfiguracji hello zasobów platformy Azure. Zasobów platformy Azure, które koszty mogą się różnić oparte na powitania region platformy Azure, którego używasz.

- Można również określić, czy innego typu oferty Azure zapewnia większą szybkość na zasobów platformy Azure.

## <a name="networking-controls"></a>Formanty sieci

Tooresources dostępu może być (w ramach sieci hello corporation) wewnętrznych lub zewnętrznych (za pośrednictwem Internetu hello). Przez użytkowników w organizacji zasobów put tooinadvertently w miejscu niewłaściwy hello i potencjalnie je otworzyć toomalicious dostępu. Jak lokalnie / urządzeń, przedsiębiorstwa należy dodać odpowiednie formanty tooensure czy użytkownicy Azure decyzje hello prawo.

![Formanty sieci](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Zarządzanie subskrypcją nazywamy zasobów podstawowych, które zapewniają podstawowy kontrolę dostępu. Witaj core — zasoby obejmują:

### <a name="network-connectivity"></a>Połączenie sieciowe

[Sieci wirtualne](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) obiektów kontenera podsieci. Chociaż nie niezbędne, często jest używana podczas łączenia zasobów firmowych toointernal aplikacji. Witaj umożliwia usługi sieci wirtualnej platformy Azure możesz toosecurely Uzyskuj dostęp do zasobów platformy Azure tooeach innych sieci wirtualnych (sieci wirtualne).

Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej. Można również połączyć sieć lokalną tooyour sieci wirtualnych.

Poniżej przedstawiono funkcje dla sieci wirtualnych Azure:

- **Izolacja**: sieci wirtualne są odizolowane od siebie. Można utworzyć oddzielne sieci wirtualnych do tworzenia, testowania i produkcji tego hello Użyj tego samego bloków adresów CIDR. Z drugiej strony możesz utworzyć wiele sieci wirtualnych, użyj innego bloków adresów CIDR i połączyć ze sobą sieci. Sieć wirtualną można podzielić na wiele podsieci. Platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień roli usługi w chmurze połączone tooa sieci wirtualnej. Opcjonalnie można skonfigurować toouse sieci wirtualnej własne serwery DNS, zamiast rozpoznawania nazw wewnętrznych platformy Azure.

- **Połączenie z Internetem**: toohello Internet, domyślnie dostęp do wszystkich maszyn wirtualnych Azure (VM) i usługi w chmurze wystąpień roli ma tooa połączonych sieci wirtualnej. Można również włączyć dostęp do przychodzących toospecific zasobów, zgodnie z potrzebami.

- **Łączność zasobów platformy Azure**: zasobów platformy Azure, takich jak usługi w chmurze i maszyn wirtualnych może być połączone toohello tej samej sieci wirtualnej. Witaj zasobów mogą się łączyć tooeach innych używania prywatnych adresów IP, nawet jeśli znajdują się w różnych podsieciach. Platforma Azure udostępnia domyślny routing między podsieciami, sieci wirtualnych i sieci lokalnej, dlatego nie masz tooconfigure i Zarządzaj trasami.

- **Łączność sieci wirtualnej**: sieci wirtualnych może być połączone tooeach innych, włączanie zasoby podłączone tooany toocommunicate sieci wirtualnej z dowolnego zasobu w innych sieci wirtualnej.

- **Połączenie lokalne**: sieci wirtualnych może być sieci lokalnych tooon połączonych za pośrednictwem sieci prywatnej połączeń między siecią a Azure lub za pośrednictwem połączenia sieci VPN typu lokacja lokacja za pośrednictwem hello Internet.

- **Filtrowanie ruchu**: ruchu sieciowego wystąpień roli maszyny Wirtualnej i usługi w chmurze można użyć do filtrowania ruchu przychodzącego i wychodzącego przez źródłowy adres IP i port docelowy adres IP i portu i protokołu.

- **Routing**: Opcjonalnie można zastąpić domyślne Azure routingu, konfigurowanie własnego trasy lub użyj trasy protokołu BGP za pośrednictwem bramy sieci.

## <a name="network-access-controls"></a>Kontrolę dostępu do sieci

[Sieciowe grupy zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) są takie jak zapory i reguł dla jak zasobu można "rozmawiać" hello sieci. Zapewniają szczegółową kontrolę nad jak / hello na takie same Jeśli podsieci (lub maszyny wirtualnej) można połączyć toohello Internet lub innych podsieci w sieci wirtualnej.

Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które Zezwalaj lub Odmów tooresources ruchu sieciowego połączone sieci wirtualne tooAzure (VNet). Grupy NSG mogą być skojarzone toosubnets, poszczególnych maszyn wirtualnych (klasyczne) lub interfejsów sieciowych poszczególnych (NIC) dołączony tooVMs (Resource Manager).

Gdy grupa NSG jest skojarzona tooa podsieci, mają zastosowanie reguły hello tooall zasobów połączonych toohello podsieci. Dodatkowo można ograniczyć ruch również skojarzyć tooa NSG maszyny Wirtualnej lub karty sieciowej.

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Bezpieczeństwo i ciągłe zgodności ze standardami w organizacji

Każda firma ma różnych potrzeb, a każda firma będzie czerpanie różne korzyści z rozwiązań w chmurze. Klienci wszelkiego rodzaju występuje nadal, hello tego samego podstawowego problemów dotyczących przenoszenia toohello chmury. Mają tooretain kontrolę nad ich danymi i chcą tego toobe dane przechowywane bezpieczeństwo i prywatność, wszystkie zachowując przezroczystość i zgodności.

Klienci szukają od dostawców w chmurze jest:

- **Zabezpieczanie danych** podczas potwierdzeniem zapewniają chmury hello zwiększyć bezpieczeństwo danych i kontrolę administracyjną, liderów IT nadal dotyczy czy Migrowanie chmury toohello pozostawi je bardziej narażony toohackers niż bieżący rozwiązania wewnętrznych.

- **Zachowaj naszych danych** usługi w chmurze prywatnej podnieść wyzwania unikatowy prywatności dla firm. Jak firmy wyglądu toosave chmury toohello na koszty infrastruktury i zwiększyć ich elastyczność, one również martwić się o utracie kontroli nad którym są przechowywane ich dane, kto uzyskuje dostęp do jego i jak jest używany.

- **Przekaż nam kontroli** nawet mogą korzystać z toodeploy chmury hello więcej rozwiązań innowacyjnych, firm są bardzo dane o utracie kontroli nad ich danych. ostatnie ujawnienia Hello agencji rządowych dostęp do danych klienta za pośrednictwem oznacza, że zarówno prawne i bardzo prawnych, upewnij niektórych dyrektorzy działu informatyki ostrożność przechowywanie danych w chmurze hello.

- **Podwyższ poziom przezroczystości** zabezpieczeń, prywatności i kontroli są decydenci toobusiness ważne, mają również możliwość hello tooindependently sprawdzić, jak ich przechowywanych danych, uzyskuje się dostęp i zabezpieczonych.

- **Obsługa zgodności** jako firm rozwinąć ich korzystanie z technologii chmury, hello złożoność i zakres norm i przepisów nadal tooevolve. Firmy muszą tooknow ich standardów zgodności zostaną spełnione i że zgodności rozpoczyna się jako przepisy dotyczące zmian w czasie.

## <a name="security-configuration-monitoring-and-alerting"></a>Konfiguracja zabezpieczeń, monitorowanie i alerty

Subskrybenci platformy Azure mogą zarządzać środowiskami chmury przy użyciu wielu urządzeń, łącznie ze stacjami roboczymi do zarządzania, komputerami deweloperów, a nawet urządzeniami uprzywilejowanych użytkowników końcowych, którzy mają uprawnienia specyficzne dla zadania. W niektórych przypadkach funkcje administracyjne są wykonywane za pośrednictwem konsoli opartych na sieci web, takich jak hello portalu Azure. W innych przypadkach mogą istnieć tooAzure bezpośrednich połączeń z systemów lokalnych za pośrednictwem wirtualnej sieci prywatnej (VPN), usług terminalowych, protokołów aplikacji klienckich lub (programowo) hello Azure Service Management API (SMAPI). Ponadto punkty końcowe klienta mogą być przyłączone do domeny lub odizolowane i niezarządzane (np. tablety lub smartfony).

Mimo że wiele możliwości dostępu i zarządzania zapewniają bogaty zestaw opcji, jednak można dodać znaczące zagrożenie tooa chmury wdrażania. Może być trudne toomanage, śledzenie i inspekcję czynności administracyjnych. To zróżnicowanie może również wprowadzać zagrożenia bezpieczeństwa związane z nieuregulowanym dostępem punkty końcowe tooclient, które są używane do zarządzania usługami w chmurze. Użycie ogólnych lub osobistych stacji roboczych do opracowywania infrastruktury i zarządzania nią powoduje, że zagrożenia mogą nadchodzić z nieprzewidywalnych kierunków, na przykład podczas przeglądania sieci Web (na przykład ataki za pośrednictwem używanych witryn) lub korzystania z poczty e-mail (na przykład techniki socjotechniczne i wyłudzanie informacji).

Monitorowanie, rejestrowanie i inspekcja stanowią podstawę dla śledzenia i zrozumienia czynności administracyjnych, ale może nie zawsze być możliwe tooaudit wszystkich akcji w ukończyć szczegółów powodu toohello ilość generowanych danych. Inspekcja skuteczności zasad zarządzania hello hello jest jednak najlepszym rozwiązaniem.

Zarządzanie zabezpieczeń platformy Azure z toocontrol obiektów zasad grupy usługi AD DS systemu Windows w przypadku wszystkich administratorów hello interfejsów, takich jak udostępnianie plików. Uwzględnij stacje robocze używane do zarządzania w procesach inspekcji, monitorowania i rejestrowania. Śledź dostęp i używanie przez wszystkich administratorów i deweloperów.

### <a name="azure-security-center"></a>Centrum zabezpieczeń Azure

Witaj [Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) udostępnia centralną widok hello stan zabezpieczeń zasobów w subskrypcji hello i zawiera zalecenia, które ułatwiają ochronę zasobów ze złamanymi zabezpieczeniami. Bardziej szczegółowe zasady (na przykład stosowania zasad toospecific grupy zasobów, które umożliwia hello enterprise tootailor ich ryzyko toohello zbierane są one adresowania) można ją włączyć.

![Azure Security Center](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Centrum zabezpieczeń zapewnia zabezpieczenia zintegrowane monitorowanie i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które mogłyby w przeciwnym razie pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań zabezpieczających. Po włączeniu [zasady zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-policies) dla zasobów subskrypcji Centrum zabezpieczeń analizuje zabezpieczenia hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach. Informacje o konfiguracji sieci są dostępne natychmiast.

Centrum zabezpieczeń Azure reprezentuje kombinację najlepszych rozwiązań analizy i zabezpieczeń Zarządzanie zasadami dla wszystkich zasobów w ramach subskrypcji platformy Azure. To narzędzie toouse wydajne i łatwe umożliwia zespoły zabezpieczeń i tooprevent oficerów ryzyka, wykrywanie i odpowiadać zagrożenia toosecurity automatycznie zbiera i analizuje dane dotyczące zabezpieczeń z zasobów platformy Azure, hello sieci i rozwiązań partnerskich, takich jak programy chroniące przed złośliwym oprogramowaniem i zapory.

Ponadto Centrum zabezpieczeń Azure stosuje zaawansowane metody analizy, w tym uczenie maszynowe i analizę behawioralną podczas korzystania z globalnej analizy zagrożeń z Microsoft produktów i usług, hello Microsoft cyfrowego ds. przestępstw jednostki (DCU), hello firmy Microsoft Zabezpieczenia odpowiedzi Center (MSRC) i zewnętrznych źródeł danych. [Zarządzanie zabezpieczeń](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) można zastosować szeroko na poziomie subskrypcji hello lub zawęzić toospecific, tooindividual szczegółowe wymagania stosowane zasobów za pośrednictwem definicji zasad.

Na koniec Centrum zabezpieczeń Azure analizuje kondycja zabezpieczeń zasobów na podstawie tych zasad i używa interesującego pulpity nawigacyjne to tooprovide i alerty dla zdarzenia, takie jak wykrywania złośliwego oprogramowania lub złośliwe połączenia IP prób.

>[!Note]
> Aby uzyskać więcej informacji o tym, jak tooapply zalecenia, przeczytaj [wdrażanie zaleceń dotyczących zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Centrum zabezpieczeń zbiera dane z Twojego tooassess maszyn wirtualnych stanu zabezpieczeń, podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. Jeśli najpierw przejść do Centrum zabezpieczeń zbieranie danych jest włączone na wszystkich maszynach wirtualnych w ramach subskrypcji. Zbieranie danych jest zalecane, ale użytkownik może zrezygnować przez [wyłączanie zbierania danych](https://docs.microsoft.com/azure/security-center/security-center-faq) w hello zasadami Centrum zabezpieczeń.

Wreszcie Centrum zabezpieczeń Azure jest otwartej platformie, która umożliwia partnerom firmy Microsoft i niezależnych dostawców toocreate oprogramowanie podłączane do Centrum zabezpieczeń Azure tooenhance jego możliwości.

Centrum zabezpieczeń Azure monitoruje hello następujących zasobów platformy Azure:

- Maszynach wirtualnych (VM) (w tym usługi w chmurze)

- Sieci wirtualne platformy Azure

- Usługi SQL Azure

- Partnerskich rozwiązań zintegrowanych z subskrypcją platformy Azure, takich jak Zapora aplikacji sieci web na maszynach wirtualnych i na [środowiska usługi aplikacji](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

Witaj OMS rozwoju oprogramowania i ochrony informacji przez zespół usługi i [program ładu](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) obsługuje jej wymagania biznesowe i stosuje toolaws i przepisami, zgodnie z opisem w [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) i [zgodności Centrum zaufania Microsoft](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Jak OMS ustanowić wymagania dotyczące zabezpieczeń, identyfikuje kontroli zabezpieczeń zarządza i monitoruje ryzyka są także opisane istnieje. Co rok, możemy przeglądu zasady, normy, procedury i wskazówek.

Każdego członka zespołu programowanie OMS odbiera szkolenia formalnego aplikacji w zakresie zabezpieczeń. Wewnętrznie używamy system kontroli wersji dla rozwoju oprogramowania. Każdy projekt oprogramowania jest chroniona przez system kontroli wersji powitania.

Firma Microsoft ma zabezpieczeń i zgodności zespołu nadzoruje i ocenia wszystkich usług firmy Microsoft. Zabezpieczenia informatyków uzupełnić hello zespołu i nie są one powiązane z hello inżynierii działów, które opracowanie OMS. Witaj zabezpieczeń ma swoje własne łańcuch zarządzania i przeprowadzenie oceny niezależnych produktów i usług tooensure zabezpieczeń i zgodności.

Operations Management Suite (znanej także jako OMS) to zbiór usług zarządzania, które zostały zaprojektowane w chmurze powitania od początku hello. Składniki pakietu OMS zamiast wdrażania i zarządzania nimi w lokalnych zasobach, całkowicie znajdują się na platformie Azure. Konfiguracja jest ograniczona do minimalnego zakresu, a pracę można rozpocząć dosłownie w ciągu kilku minut.

![Program Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Tak, ponieważ OMS usługi uruchamiane w chmurze hello nie oznacza, że nie można efektywnie zarządzać w lokalnym środowisku.

Umieść agenta w dowolnym systemie Windows lub komputera z systemem Linux w centrum danych która będzie wysyłać tooLog danych analizy, gdzie można przeprowadzić analizę oraz innych danych zebranych z chmury, lub na lokalne usługi. Użyj chmury hello tooleverage kopia zapasowa Azure i usługi Azure Site Recovery dla kopii zapasowej i wysoka dostępność dla zasobów lokalnych.

Elementy Runbook w chmurze hello zwykle nie dostęp do zasobów lokalnych, ale można zainstalować agenta na co najmniej jeden komputer za który będzie hostem elementów runbook w centrum danych. Po uruchomieniu elementu runbook, należy po prostu określić, czy go toorun w chmurze hello lub na lokalnym procesu roboczego.

podstawowe funkcje Hello OMS są udostępniane przez zestaw usług, które działają na platformie Azure. Każda usługa udostępnia funkcję zarządzania określonymi i scenariusze zarządzania różnych tooachieve usług można łączyć.

![Program Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure Operations manager rozszerza jego funkcje zapewniając rozwiązania do zarządzania. [Rozwiązania do zarządzania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) opakowaniach jednostkowych zestawów logiki implementujących scenariusz zarządzania, wykorzystując co najmniej jedną usługę OMS.

![Zarządzanie operacji systemu Azure](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Różnych rozwiązaniach dostępnych firmy Microsoft i partnerów, można łatwo dodać tooyour subskrypcji platformy Azure tooincrease hello wartości inwestycji w OMS.

Przez partnera można utworzyć własne toosupport rozwiązania, aplikacje i usługi i podaj toousers za pośrednictwem hello Azure Marketplace lub Szybki Start szablonów.

## <a name="performance-alerting-and-monitoring"></a>Monitorowanie i alerty wydajności

### <a name="alerting"></a>Generowanie alertów

Metodą monitorowania metryki zasobów platformy Azure, zdarzeń i dzienniki są alerty i powiadomienia po określeniu warunek jest spełniony.

**Alerty w różnych usług platformy Azure**

Alerty są dostępne w różnych usługach, w tym:

- Usługi Application Insights: Włącza testu sieci web i metryki alerty.

>[!Note]
> Zobacz [ustawić alertów w usłudze Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) i [monitorowanie dostępności i czas odpowiedzi dla wszystkich witryn sieci Web](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Analizy dzienników (Operations Management Suite): Umożliwia hello routing tooLog działania i dzienniki diagnostyczne analizy. Operations Management Suite umożliwia metryki, log oraz inne typy alertów.

>[!Note]
> Aby uzyskać więcej informacji, zobacz alerty w [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure Monitor: Włącza alerty oparte na wartości metryki i zdarzenia dziennika aktywności. Można użyć hello [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/dn931943.aspx) toomanage alertów.

>[!Note]
> Aby uzyskać więcej informacji, zobacz [przy użyciu hello portalu Azure, programu PowerShell lub alerty toocreate interfejsu wiersza polecenia hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Monitorowanie

Problemy z wydajnością w Twojej aplikacji w chmurze może wpłynąć na Twojej firmy. Z wielu powiązanych elementów i częste wersjach degradations może nastąpić w dowolnej chwili. I w przypadku tworzenia aplikacji, użytkowników, zazwyczaj odnajdywanie problemy, które nie udało się znaleźć podczas testowania. Należy od razu wiedzieć o tych problemów i narzędzia do diagnozowania i rozwiązywania problemów hello. Microsoft Azure ma szeroką gamę narzędzi do identyfikacji tych problemów.

**Jak monitorować Moje aplikacje w chmurze Azure?**

Istnieje szereg narzędzia do monitorowania usługi i aplikacje platformy Azure. Niektóre z ich funkcji nakładają się. To jest częściowo ze względów historycznych i częściowo powodu toohello rozmycia między rozwoju i działania aplikacji.

Poniżej przedstawiono hello Narzędzia główne:

- **Azure Monitor** jest podstawowym narzędziem do monitorowania usługi działające na platformie Azure. Udostępnia poziomie infrastruktury danych o przepływności hello usługi i hello otaczającego środowiska. W przypadku zarządzania aplikacjami w usłudze Azure podejmowaniu decyzji, czy tooscale w górę lub w dół zasobów, Azure Monitor daje służą toostart.

- **Usługa Application Insights** mogą być używane do tworzenia aplikacji oraz jako rozwiązanie monitorujące produkcji. Działa, instalując pakiet w swojej aplikacji, a więc zapewnia bardziej wewnętrzny widok co się dzieje. Jego danych obejmuje czas reakcji zależności i śladów wyjątek, debugowanie migawki, profile wykonywania. Zapewnia on zaawansowanych narzędzi inteligentne analizowanie danych to dane telemetryczne zarówno toohelp debugowania aplikacji i toohelp zrozumieć, co robią użytkownicy z nim. Można określić, czy kolekcji w czas reakcji przypada toosomething w aplikacji lub niektóre zewnętrznego problemem resourcing. Jeśli używasz programu Visual Studio i aplikacji hello jest uszkodzone, użytkownik może zostać pobrany prawo toohello problem wiersze kodu, można go naprawić.

- **Zaloguj się Analytics** jest potrzebują tootune wydajności i plan konserwacji na aplikacje uruchomione w środowisku produkcyjnym. Jest on oparty na platformie Azure. On zbiera i agregują dane z wielu źródeł, chociaż z opóźnieniem 10 minut too15. Przewiduje całościowe rozwiązanie zarządzania Azure, lokalne i innych firm oparte na chmurze infrastruktury (na przykład usług Amazon Web Services). Zawiera bardziej zaawansowane funkcje narzędzi tooanalyze danych między źródłami więcej, umożliwia złożonych zapytań przez wszystkie dzienniki i może aktywnie alert po wystąpieniu określonego warunku. Można nawet zebrać dane niestandardowe w jego centralnym repozytorium, dzięki czemu może zapytania i wizualizacji go.

- **System Center Operations Manager (SCOM)** jest do zarządzania i monitorowania instalacji dużych chmury. Może być już znasz go jako narzędzia do zarządzania lokalnymi chmury na podstawie funkcji Hyper-V i Windows Server, ale można również zintegrować z i zarządzanie aplikacjami platformy Azure. Między innymi może instalować usługi Application Insights na istniejące aplikacje na żywo. Jeśli aplikacja przestanie działać, określa w sekundach.


## <a name="next-steps"></a>Następne kroki

- [Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Przykłady stosowania ładu subskrypcji platformy Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Microsoft Azure dla instytucji rządowych](https://docs.microsoft.com/azure/azure-government/).
