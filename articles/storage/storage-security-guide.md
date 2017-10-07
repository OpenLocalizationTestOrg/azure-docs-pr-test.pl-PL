---
title: Przewodnik po zabezpieczeniach magazynu aaaAzure | Dokumentacja firmy Microsoft
description: "Szczegóły hello wiele metod zabezpieczania usługi Azure Storage, w tym między innymi tooRBAC, szyfrowanie usługi Magazyn szyfrowania po stronie klienta, SMB 3.0 i szyfrowania dysków Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Przewodnik po zabezpieczeniach magazynu Azure
## <a name="overview"></a>Omówienie
Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji. samo konto magazynu Hello mogą być chronione przy użyciu kontroli dostępu opartej na rolach i Azure Active Directory. Dane mogą być chronione przy użyciu przesyłanych między aplikacją a Azure [szyfrowania po stronie klienta](storage-client-side-encryption.md), HTTPS lub SMB 3.0. Dane można ustawić toobe automatycznie szyfrowane, gdy zapisywane tooAzure magazynu za pomocą [szyfrowanie usługi Magazyn (SSE)](storage-service-encryption.md). Systemu operacyjnego i dysków z danymi używanych przez maszyny wirtualne można ustawić toobe zaszyfrowane za pomocą [szyfrowania dysków Azure](../security/azure-security-disk-encryption.md). Obiekty danych toohello delegowanego dostępu w usłudze Azure Storage można otrzymać za pomocą [sygnatury dostępu współdzielonego](storage-dotnet-shared-access-signature-part-1.md).

W tym artykule zapewni omówienie każdego z tych funkcji zabezpieczeń, które mogą być używane z usługą Azure Storage. Łącza są udostępniane tooarticles, która zapewni szczegóły dotyczące każdej funkcji, można w prosty sposób dalszych badań na każdego tematu.

Poniżej przedstawiono toobe tematy hello omówione w tym artykule:

* [Zabezpieczenia płaszczyzny Management](#management-plane-security) — zabezpieczanie konta magazynu

  płaszczyzny zarządzania Hello składa się z toomanage zasoby używane hello konta magazynu. W tej sekcji będziesz omawianiu modelu wdrażania usługi Azure Resource Manager hello i jak toocontrol kontroli dostępu opartej na rolach (RBAC) toouse uzyskują dostęp do kont magazynu tooyour. Firma Microsoft będzie również porozmawiać na temat zarządzania kluczami konta magazynu i w jaki sposób tooregenerate je.
* [Bezpieczeństwo danych w płaszczyźnie](#data-plane-security) — tooYour zabezpieczanie dostępu do danych

  W tej sekcji wyjaśniono zezwalania na dostęp toohello rzeczywiste dane obiektów na koncie magazynu obiektów blob, plików, kolejek i tabel, przy użyciu sygnatury dostępu współdzielonego i przechowywane zasad dostępu. Omówimy SAS poziomu usług i poziomie konta sygnatury dostępu Współdzielonego. Firma Microsoft sekcji omówiono również, jak toolimit dostępu tooa określonego adresu IP (lub zakres adresów IP), jak używany protokół hello toolimit tooHTTPS i jak toorevoke a Shared Access Signature nie oczekuje na tooexpire.
* [Szyfrowanie podczas transferu](#encryption-in-transit)

  W tej sekcji omówiono sposób toosecure danych podczas transferu do lub z usługi Azure Storage. Będzie omawianiu hello zalecane użycie protokołu HTTPS i hello szyfrowania używany przez protokół SMB 3.0 do udziały plików platformy Azure. Firma Microsoft będzie także Spójrz na szyfrowanie po stronie klienta, co umożliwia tooencrypt hello dane przed przeniesieniem do magazynu w aplikacji klienckiej i toodecrypt powitania po przeniesieniu poza magazynu.
* [Szyfrowanie w spoczynku](#encryption-at-rest)

  Zostanie omawianiu szyfrowanie usługi Magazyn (SSE) i jak można ją włączyć dla konta magazynu, co powoduje blokowe, stronicowe obiekty BLOB i uzupełnialnych obiektów blob, są szyfrowane automatycznie, gdy zapisywane tooAzure magazynu. Ponadto przedstawiono sposób użycia szyfrowania dysków Azure i Poznaj podstawowe różnice hello i przypadków szyfrowania dysku i SSE i szyfrowania po stronie klienta. Krótko przedstawiono zgodności ze standardem FIPS dla Stanów Zjednoczonych Komputery dla instytucji rządowych.
* Przy użyciu [analityka magazynu](#storage-analytics) tooaudit dostęp do usługi Azure Storage

  W tej sekcji omówiono sposób toofind informacji w module analiz magazynu hello rejestrowania dla żądania. Firma Microsoft będzie Spójrz na analityka magazynu rzeczywiste dane dziennika i zobacz, jak toodiscern czy żądań z hello magazynu klucza za pomocą podpisu dostępu udostępnionego konta lub anonimowo oraz tego, czy powodzeniem lub niepowodzeniem.
* [Włączanie przeglądarki klientów przy użyciu mechanizmu CORS](#Cross-Origin-Resource-Sharing-CORS)

  Ta sekcja zawiera informacje o jak tooallow współużytkowanie zasobów między źródłami (CORS) do udostępniania. Będzie omawianiu dostęp z innych domen i jak toohandle go przy użyciu funkcji CORS hello wbudowane usługi Azure Storage.

## <a name="management-plane-security"></a>Zarządzanie płaszczyzny zabezpieczeń
płaszczyzny zarządzania Hello składa się z operacji, które mają wpływ na konto magazynu hello sam. Na przykład można utworzyć lub usuwania konta magazynu, Pobierz listę kont magazynu w ramach subskrypcji, pobrać klucze konta magazynu hello lub ponownie wygenerować kluczy konta magazynu hello.

Podczas tworzenia nowego konta magazynu jest wybierz model wdrożenia klasycznego lub Menedżera zasobów. Witaj klasycznego modelu tworzenie zasobów na platformie Azure tylko umożliwia subskrypcji toohello all-or-nothing dostępu i z kolei hello konta magazynu.

Ten przewodnik koncentruje się na powitania modelu Resource Manager, który jest hello zalecany sposób tworzenia kont magazynu. Za pomocą kont magazynu hello Resource Manager, a nie dające dostęp toohello całej subskrypcji można kontrolować dostęp na płaszczyźnie bardziej ograniczone Zarządzanie toohello poziomu przy użyciu kontroli dostępu opartej na rolach (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Jak toosecure, konto magazynu, z kontroli dostępu opartej na rolach (RBAC)
Załóżmy porozmawiać na temat RBAC jest i jak można go użyć. Każda subskrypcja platformy Azure zawiera usługę Azure Active Directory. Dostęp do toomanage zasobów w subskrypcji platformy Azure hello korzystających z modelu wdrażania usługi Resource Manager hello można udzielić użytkowników, grup i aplikacji z tego katalogu. Jest to określony tooas kontroli dostępu opartej na rolach (RBAC). toomanage tego dostępu, można użyć hello [portalu Azure](https://portal.azure.com/), hello [narzędzia wiersza polecenia platformy Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), lub hello [interfejsów API REST dostawcy zasobów magazynu Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Witaj modelu Resource Manager należy umieścić w zasobów grupy i kontroli dostępu toohello zarządzania płaszczyźnie tego konta określonego magazynu przy użyciu usługi Azure Active Directory hello konta magazynu. Na przykład możesz zapewnić określonych użytkowników hello możliwości tooaccess hello klucze konta magazynu, podczas gdy inni użytkownicy mogą wyświetlać informacje o koncie magazynu hello, ale nie ma dostępu do kluczy konta magazynu hello.

#### <a name="granting-access"></a>Udzielanie dostępu
Dostęp przez przypisanie hello odpowiednie RBAC roli toousers, grup i aplikacji, w zakresie prawo hello. toogrant dostępu toohello całej subskrypcji, możesz przypisać rolę na poziomie subskrypcji hello. Można przyznać dostęp tooall hello zasobów w grupie zasobów przez udzielanie uprawnień toohello zasobów grupy. Można także przypisać określonych ról toospecific zasobów, takich jak konta magazynu.

Poniżej przedstawiono główne punkty hello konieczność tooknow dotyczące korzystania z operacji zarządzania hello tooaccess RBAC konta magazynu Azure:

* Po przypisaniu dostępu przypisaniu zasadniczo konta toohello roli, które ma dostęp toohave. Można kontrolować toomanage operacje używane toohello dostępu do tego konta magazynu, ale nie toohello danych obiektów na koncie hello. Na przykład można przyznać uprawnień właściwości hello tooretrieve hello konta magazynu (na przykład nadmiarowość), ale nie tooa kontenera lub dane w kontenerze wewnątrz magazynu obiektów Blob.
* Osoba, która tooaccess uprawnienia toohave hello obiektów danych na koncie magazynu hello, nadać im klucze konta magazynu hello tooread uprawnień i użytkownik może następnie użyć tych kluczy tooaccess hello blob, kolejek, tabel i plików.
* Role można przypisywać tooa określonego konta użytkownika, grupy użytkowników lub tooa określonej aplikacji.
* Każda rola ma listę działania i nie działania. Na przykład Rola współautora maszyny wirtualnej hello ma akcję "listKeys", która umożliwia toobe klucze konta magazynu hello do odczytu. Witaj współautora ma "Nie akcje" jak aktualizowanie hello dostępu dla użytkowników w hello usługi Active Directory.
* Role dla magazynu obejmują (ale nie są ograniczone do) hello następujące czynności:

  * Właściciel — mogą zarządzać wszystkim łącznie z dostępem.
  * Współautor — Administratorzy mogą wykonywać żadnych czynności właściciela hello oprócz przypisywanie dostępu. Ktoś z tą rolą mogą wyświetlać i ponownie wygenerować kluczy konta magazynu hello. Z hello klucze konta magazynu uzyskać dostęp do obiektów danych hello.
  * Czytnik — mogą wyświetlać informacje o koncie magazynu hello, z wyjątkiem kluczy tajnych. Na przykład po przypisaniu roli z uprawnieniami czytnika toosomeone konta magazynu hello mogą wyświetlać właściwości hello hello konta magazynu, ale nie mogą wprowadzać żadnych zmian właściwości toohello lub Wyświetl klucze konta magazynu hello.
  * Współautor konta magazynu — mogą zarządzać konta magazynu hello — może odczytywać hello subskrypcji grup zasobów i zasobów, tworzenie i zarządzanie wdrożeniami grup zasobów subskrypcji. Można także przejść klucze konta magazynu hello, co z kolei oznacza, że mogą uzyskiwać dostęp do hello płaszczyzna danych.
  * Administrator dostępu użytkowników — mogą zarządzać konto magazynu toohello dostępu użytkownika. Na przykład można udzielać czytnika dostępu tooa określonego użytkownika.
  * Maszyna wirtualna współautora — mogą zarządzać maszyn wirtualnych, ale nie hello magazynu konta toowhich gdy są połączeni. Tę rolę można wyświetlić listę hello klucze konta magazynu, co oznacza, że hello toowhom użytkownika przypisać tę rolę można aktualizować hello płaszczyzna danych.

    Aby toocreate użytkownika maszyny wirtualnej mają one toobe toocreate stanie hello odpowiedniego pliku VHD na koncie magazynu. toodo, że powinni toobe tooretrieve stanie hello magazynu klucz konta i przekaż go toohello interfejsu API tworzenia hello maszyny Wirtualnej. W związku z tym, można wyświetlić listę kluczy konta magazynu hello muszą mieć te uprawnienia.
* role niestandardowe toodefine możliwości Hello jest funkcją, która pozwala toocompose zestaw akcji z listy dostępnych akcji, które mogą być wykonywane na zasobów platformy Azure.
* Użytkownik Hello ma toobe zdefiniować przed przypisaniem toothem roli w usłudze Azure Active Directory.
* Można utworzyć raport, który przyznane/odwołany jakiego rodzaju dostępu do i z którego i na jakie zakresu przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure.

#### <a name="resources"></a>Zasoby
* [Kontrola dostępu oparta na rolach w usłudze Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  W tym artykule opisano hello kontroli dostępu opartej na roli Azure Active Directory i jej działania.
* [Kontrola dostępu oparta na rolach (RBAC): wbudowane role](../active-directory/role-based-access-built-in-roles.md)

  Ten artykuł zawiera szczegóły dotyczące wszystkich ról wbudowanych hello dostępne w RBAC.
* [Omówienie wdrażania przy użyciu usługi Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md)

  W tym artykule opisano hello wdrożenie usługi Resource Manager i klasycznych modeli wdrażania, a ponadto wyjaśniono hello zalety korzystania z grup hello Resource Manager i zasobów. Wyjaśniono, jak działają hello rozwiązań usługi obliczenia Azure, sieci i dostawcy magazynu pod hello modelu Resource Manager.
* [Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu API REST](../active-directory/role-based-access-control-manage-access-rest.md)

  W tym artykule opisano, jak toouse hello toomanage interfejsu API REST RBAC.
* [Dokumentacja interfejsu API REST dostawcy zasobów magazynu Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  To odwołanie hello hello interfejsów API służy toomanage Twojego konta magazynu programowo.
* [Tooauth przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  W tym artykule opisano, jak za pomocą tooauthenticate hello interfejsów API Menedżera zasobów.
* [Kontrola dostępu oparta na rolach dla platformy Microsoft Azure — konferencja Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  To jest łącze tooa wideo w witrynie Channel 9 z konferencji Ignite 2015 MS hello. W tej sesji porozmawiać o dostęp do zarządzania i możliwości raportowania w programie Azure i eksplorowanie najlepsze rozwiązania dotyczące zabezpieczania dostępu tooAzure subskrypcji przy użyciu usługi Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Zarządzanie kluczami konta magazynu
Konto magazynu, że klucze są ciągami 512-bitowe utworzone przez platformę Azure, które wraz z magazynu hello nazwa, konta mogą być obiekty danych hello używane tooaccess przechowywane na koncie magazynu hello, np. obiekty BLOB, jednostek w tabeli, kolejki komunikatów i plików w udziale plików Azure. Kontrolowanie kontroli klucze konta magazynu dostępu toohello dostępu toohello płaszczyzna danych dla tego konta magazynu.

Każde konto magazynu ma dwa klucze określonego tooas "Klucz 1" i "Klucz 2" w hello [portalu Azure](http://portal.azure.com/) w hello poleceń cmdlet programu PowerShell. Te mogą zostać wygenerowane ponownie ręcznie przy użyciu jednej z kilku metod, w tym, ale nie wyłącznie toousing hello [portalu Azure](https://portal.azure.com/), programu PowerShell, interfejsu wiersza polecenia Azure hello lub programowo przy użyciu hello biblioteki klienta usługi Storage platformy .NET lub hello Azure Interfejs API REST usług magazynu.

Istnieje wiele przyczyn tooregenerate kluczy konta magazynu.

* Użytkownik może ponownie wygenerować ich regularnie ze względów bezpieczeństwa.
* Jeśli ktoś zarządzane toohack do aplikacji i pobrać klucz hello zostało zapisane na stałe lub zapisany w pliku konfiguracji, zapewniając im konta magazynu tooyour pełny dostęp, czy ponownie wygenerować kluczy konta magazynu.
* Innym przypadku ponowne generowanie klucza jest zespołem używa aplikacji Eksploratora magazynu, który zachowuje klucz konta magazynu hello, jeden z członków zespołu hello pozostawia. Aplikacja Hello będzie nadal toowork, zapewniając im konta magazynu tooyour dostępu po zrobi to ktoś inny. Jest rzeczywiście hello głównej przyczyny one utworzone sygnatury dostępu współdzielonego konta poziom — SAS poziomie konta można użyć zamiast przechowywanie kluczy dostępu hello w pliku konfiguracji.

#### <a name="key-regeneration-plan"></a>Ponowne generowanie klucza planu
Nie chcesz, aby klucz regenerate hello toojust używasz bez niektóre planowania. Można to zrobić, można odcięte wszystkich dostępu toothat konta magazynu, która może spowodować przestoje głównych. Jest to, dlatego dostępne są dwa klucze. Należy ponownie wygenerować jeden klucz w czasie.

Wygenerować klucze, upewnij się, że masz listę wszystkich aplikacji, które są zależne od konta magazynu hello, a także innych usług używanych na platformie Azure. Na przykład jeśli używasz usługi Azure Media Services, które są zależne od konta magazynu, musisz ponownie zsynchronizować klucze dostępu hello z usługą multimediów po ponownym wygenerowaniu klucza hello. Jeśli używane są wszystkie aplikacje, takie jak Eksploratora magazynu, należy tooprovide hello nowych kluczy toothose aplikacji oraz. Należy pamiętać, że jeśli masz maszyny wirtualne, których pliki VHD są przechowywane na koncie magazynu hello ich nie dotyczy ponowne generowanie kluczy konta magazynu hello.

Można ponownie wygenerować klucze w hello portalu Azure. Po klucze są generowane może potrwać too10 toobe minut synchronizację usługi magazynu.

Jeśli wszystko jest gotowe, Oto ogólny proces hello opisujące, jak należy zmienić klucz. W takim przypadku hello zakłada się, że obecnie używasz klucz 1 i ma toochange wszystko toouse klucz 2 zamiast tego.

1. Wygeneruj ponownie klucz 2 tooensure jest bezpieczne. Można to zrobić w hello portalu Azure.
2. We wszystkich aplikacji hello przechowywania klucza magazynu hello zmienić hello magazynu kluczy toouse klucza 2 nową wartość. Testowanie i publikowanie aplikacji hello.
3. Po wszystkich hello aplikacje i usługi są uruchomione i uruchomiony pomyślnie, należy ponownie wygenerować klucz 1. Gwarantuje to, że każdy toowhom nie mają wyraźnie hello nowy klucz nie będą mieć dostęp do konta magazynu toohello.

Jeśli obecnie używasz 2 klucza, można użyć tego samego procesu, ale hello odwrotnej nazwy kluczy hello.

Przez kilka dni, można migrować zmiana każdego toouse hello nowy klucz aplikacji i jej opublikowaniem. Po wykonaniu wszystkich z nich czynności należy wrócić do poprzedniej strony i ponownie wygenerować hello starego klucza, ale nie działa.

Innym rozwiązaniem jest klucz konta magazynu hello tooput w [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) jako klucz tajny i mają klucz hello pobierania aplikacji z tego miejsca. Następnie po ponownie wygenerować klucz hello i zaktualizować hello Azure Key Vault aplikacji hello nie będzie konieczne toobe ponownego wdrożenia, ponieważ ich przejmą hello nowy klucz ze hello Azure Key Vault automatycznie. Należy pamiętać, że program może odczytać klucza hello trzeba go aplikacji hello lub można ją buforują w pamięci i w przypadku niepowodzenia podczas korzystania z niego, klucz hello ponownego pobrania z hello Azure Key Vault.

Również przy użyciu usługi Azure Key Vault dodaje kolejny poziom zabezpieczeń dla kluczy magazynu. Jeśli używasz tej metody, nigdy nie należy hello magazynu kluczy ustalony w pliku konfiguracji, co spowoduje usunięcie tego ścieżek ktoś uzyskiwania dostępu do kluczy toohello bez odpowiedniego uprawnienia.

Inną zaletą używania usługi Azure Key Vault jest można też kontrolować dostęp tooyour kluczy przy użyciu usługi Azure Active Directory. Oznacza to, że można udzielać dostępu toohello kilku aplikacji, które są wymagane klucze hello tooretrieve z usługi Azure Key Vault i wiedzieć, że inne aplikacje nie będą tooaccess stanie hello kluczy bez przyznania im uprawnień w szczególności.

Uwaga: zalecane jest toouse tylko jedną hello kluczy we wszystkich aplikacjach na powitania sam czas. Jeśli używasz klucz 1 w niektórych miejscach i 2 klucza w innych, nie będzie można toorotate stanie klucze bez utraty dostępu do aplikacji.

#### <a name="resources"></a>Zasoby
* [Informacji o kontach magazynu Azure](storage-create-storage-account.md#regenerate-storage-access-keys)

  Ten artykuł zawiera omówienie kont magazynu i wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu do magazynu.
* [Dokumentacja interfejsu API REST dostawcy zasobów magazynu Azure](https://msdn.microsoft.com/library/mt163683.aspx)

  Ten artykuł zawiera łącza toospecific artykułów na temat pobierania kluczy konta magazynu hello i Trwa ponowne generowanie kluczy konta magazynu hello konta platformy Azure przy użyciu hello interfejsu API REST. Uwaga: Jest to w przypadku kont magazynu Menedżera zasobów.
* [Operacje na kontach magazynu](https://msdn.microsoft.com/library/ee460790.aspx)

  W tym artykule w hello dokumentacja interfejsu API REST magazynu Service Manager zawiera artykuł toospecific łącza na pobieranie i Trwa ponowne generowanie kluczy konta magazynu hello przy użyciu hello interfejsu API REST. Uwaga: Jest to w przypadku kont magazynu Classic hello.
* [Powiedzieć praktyczny brak jakichkolwiek tookey management — Zarządzanie dostępu tooAzure magazynu danych, przy użyciu usługi Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  W tym artykule przedstawiono sposób tooyour usługi Azure Storage klucze w usłudze Azure Key Vault dostępu toouse toocontrol usługi Active Directory. Pokazuje też, jak toouse usługi Automatyzacja Azure zadania tooregenerate hello kluczy co godzinę.

## <a name="data-plane-security"></a>Zabezpieczenia warstwy danych
Bezpieczeństwo płaszczyzna danych odwołuje się metody toohello toosecure używane hello danych obiektów przechowywanych w magazynie Azure — hello obiektów blob, kolejek, tabel i plików. Firma Microsoft przedstawiono metody tooencrypt hello danych i bezpieczeństwo podczas przesyłania danych hello, ale jak uzyskać informacje umożliwiające dostęp do obiektów toohello?

Istnieją dwie metody kontrolowania dostępu toohello danych same obiekty. Hello jest najpierw klucze konta magazynu toohello kontroli dostępu i hello drugi jest przy użyciu sygnatury dostępu współdzielonego toogrant dostępu toospecific dane obiektów dla określonego przedziału czasu.

Jeden wyjątek toonote jest ustawienie poziomu dostępu hello hello kontener obiektów blob hello odpowiednio umożliwia obiekty BLOB tooyour dostępu publicznego. Jeśli ustawisz dostępu tooBlob kontenera lub kontenera, umożliwia publiczny dostęp do odczytu obiektów blob hello w danym kontenerze. Oznacza to, że każdy użytkownik z adresem URL wskazującym blob tooa w danym kontenerze otworzyć go w przeglądarce bez przy użyciu sygnaturę dostępu współdzielonego i klucze konta magazynu hello o.

### <a name="storage-account-keys"></a>Klucze kont magazynu
Klucze konta magazynu są tworzone przez platformę Azure, która wraz z nazwą konta magazynu hello, może być obiektów danych hello używane tooaccess przechowywane na koncie magazynu hello ciągi 512-bitowe.

Można na przykład obiekty BLOB do odczytu, zapisu tooqueues, tworzenie tabel i modyfikowanie plików. Wiele z tych akcji mogą być wykonywane za pośrednictwem hello Azure portalu lub przy użyciu jednej z wielu aplikacji Eksploratora magazynu. Można również napisać kod toouse hello interfejsu API REST lub jednego z tooperform biblioteki klienta magazynu hello te operacje.

Zgodnie z opisem w sekcji hello na powitania [zabezpieczeń płaszczyzny zarządzania](#management-plane-security), dostęp toohello magazynu kluczy dla konta magazynu Classic można otrzymać, zapewniając toohello pełnego dostępu do subskrypcji platformy Azure. Dostęp toohello magazynu kluczy dla konta magazynu przy użyciu modelu usługi Azure Resource Manager hello można sterować za pośrednictwem kontroli dostępu opartej na rolach (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Jak toodelegate dostępu tooobjects na koncie przy użyciu sygnatury dostępu współdzielonego i przechowywane zasad dostępu
Sygnaturę dostępu współdzielonego jest ciąg zawierający token zabezpieczający, który może być dołączony tooa identyfikator URI, który pozwala toodelegate dostępu toostorage obiektów i określić ograniczeń, takich jak uprawnienia hello i hello daty/godziny zakresu dostępu.

Można przyznać dostęp tooblobs, kontenery wiadomości w kolejce, plików i tabele. Tabel można faktycznie przyznać uprawnienia tooaccess zakresu jednostek w tabeli hello określając hello partycji i wiersza zakresami kluczy toowhich program access toohave użytkownika hello. Na przykład jeśli masz dane przechowywane z użyciem klucza partycji geograficzne stanu nadać ktoś dane hello toojust dostępu dla Polski.

W kolejnym przykładzie może dać tokenu sygnatury dostępu Współdzielonego, umożliwiający toowrite wpisy tooa kolejki aplikacji sieci web i nadaj pracownik roli aplikacji komunikaty tooget tokenu sygnatury dostępu Współdzielonego z hello kolejka i przetwarzanie ich. Lub jednego klienta można nadać tokenu sygnatury dostępu Współdzielonego, można użyć tooupload obrazy tooa kontenera w magazynie obiektów Blob i zapewniają te obrazy tooread uprawnienia aplikacji sieci web. W obu przypadkach jest separacji — każdej aplikacji można przyznać dostęp tylko hello, które są wymagane w kolejności tooperform ich zadań. Jest to możliwe przy użyciu hello sygnatury dostępu współdzielonego.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Dlaczego chcesz sygnatury dostępu współdzielonego toouse
Dlaczego chcesz toouse SAS, a nie tylko nadawania klucz konta magazynu jest dużo łatwiejszy? Nadawania klucz konta magazynu jest podobne do udostępniania kluczy hello Królestwo Twojego magazynu. Udziela uprawnień pełny dostęp. Ktoś może użycie klawiszy i przekazać swoje konto magazynu całą biblioteki tooyour. One można również zastąpić pliki wersjami zainfekowany wirusów lub kradzieży danych. Przekazywanie konta magazynu tooyour nieograniczony dostęp, to element, którego nie powinny być uwzględniane w niewielkim stopniu.

Z sygnatury dostępu współdzielonego można nadać klienta tylko hello uprawnienia wymagane przez ograniczony czas. Na przykład jeśli ktoś przekazuje konta tooyour obiektów blob, można przyznać im dostęp do zapisu dla wystarczającego czasu tooupload hello obiektów blob (w zależności od rozmiaru hello hello obiektu blob, oczywiście). A jeśli zmienisz zdanie, że dostęp można odwołać.

Ponadto można określić, że żądania przy użyciu sygnatury dostępu Współdzielonego są ograniczone tooa niektórych adres IP lub adres IP zewnętrznego tooAzure zakresu adresów. Możesz również wymagać, że żądania są wykonywane przy użyciu określonego protokołu (HTTPS lub HTTP/HTTPS). Oznacza to, jeśli mają tooallow ruchu HTTPS, można ustawić tylko tooHTTPS protokołu hello wymagane, a ruch HTTP będzie zablokowany.

#### <a name="definition-of-a-shared-access-signature"></a>Definicja sygnatury dostępu współdzielonego
Sygnaturę dostępu współdzielonego jest zestaw parametrów zapytania dołączany toohello adres URL, wskazując hello zasobów

zapewnia informacje o dostępie do hello dozwolone i hello długość czasu, dla których hello dostęp jest dozwolony. Oto przykład; Ten identyfikator URI zawiera blob tooa dostęp do odczytu przez pięć minut. Uwaga SAS parametry zapytania musi być zakodowanych jako adres URL, takich jak 3A % dwukropka (:) lub % 20 spacją.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Jak powitalne sygnatura dostępu współdzielonego jest uwierzytelniany przez hello usługi magazynu Azure
Usługa Magazyn hello odebrania żądania hello przyjmuje parametry zapytania hello i tworzy podpis przy użyciu hello tę samą metodę jak hello program wywołujący. Porównuje dwa podpisów hello. Jeśli zgadzają się następnie hello usługi magazynu można Sprawdź się, że jest on prawidłowy toomake wersji usług magazynu hello, sprawdź, czy hello aktualnej daty i godziny są w określonym przedziale czasu hello, upewnij się, że hello dostępu odpowiada żądania toohello itp.

Na przykład z naszych powyżej adresu URL, jeśli adres URL hello został wskazuje plik tooa zamiast obiektu blob to żądanie nie powiedzie się, ponieważ określa on tego hello jest sygnatura dostępu współdzielonego dla obiekt blob. Jeśli hello polecenia REST wywoływana tooupdate obiektu blob, będą się kończyć niepowodzeniem, ponieważ hello sygnatura dostępu współdzielonego Określa, czy jest dozwolony dostęp tylko do odczytu.

#### <a name="types-of-shared-access-signatures"></a>Rodzaje sygnatur dostępu współdzielonego
* SAS poziomu usług mogą być używane tooaccess określonych zasobów na koncie magazynu. Przykłady to pobiera listę obiektów blob w kontenerze, pobieranie obiektu blob, aktualizowania jednostki w tabeli, dodawanie kolejka tooa wiadomości lub przekazywanie pliku tooa udziału plików.
* Sygnatury dostępu Współdzielonego z poziomu konta mogą być używane tooaccess wszystko, co umożliwia SAS poziomu usług. Ponadto pozwala tooresources opcje, które nie są dozwolone z poziomu usługi sygnatury dostępu Współdzielonego, takich jak hello możliwości toocreate kontenerów, tabel, kolejek i udziałów plików. Można również określić usługi toomultiple dostęp na raz. Na przykład może przekażesz ktoś dostęp do obiektów blob tooboth i plików na Twoim koncie magazynu.

#### <a name="creating-an-sas-uri"></a>Tworzenie identyfikatora URI połączenia SAS
1. Można utworzyć URI ad hoc na żądanie, zdefiniowania wszystkich parametrów zapytania hello zawsze.

   Jest to naprawdę elastycznych, ale jeśli masz logiczne zestaw parametrów, które są podobne za każdym razem, za pomocą zasad dostępu przechowywany jest zorientować się.
2. Można utworzyć zasady dostępu do przechowywanych dla całego kontenera, udziału plików, tabel lub kolejek. Można to podstawę hello dla hello tworzenia URI sygnatury dostępu Współdzielonego. Łatwo można odwołać uprawnień na podstawie zasad dostępu przechowywane. Może mieć up too5 zasady zdefiniowane dla każdego kontenera, kolejki, tabeli lub udziału plików.

   Na przykład zostały ma toohave wiele osób do odczytu obiektów blob hello w określonym kontenerze, można utworzyć zasady dostępu przechowywane informacją "zapewniają dostęp do odczytu" i inne ustawienia, które będą hello sam zawsze. Następnie można utworzyć identyfikatora URI połączenia SAS za pomocą ustawienia hello hello przechowywane zasady dostępu i określając wygaśnięcia hello daty/godziny. Witaj dzięki temu będzie masz toospecify wszystkie hello parametry zapytania zawsze.

#### <a name="revocation"></a>Odwołania
Załóżmy, że naruszono bezpieczeństwo sieci SAS lub ma toochange go z powodu zabezpieczeń firmy lub wymagania dotyczące zgodności z przepisami. Jak odwołać zasób tooa dostępu za pomocą tego skojarzenia zabezpieczeń? To zależy od sposobu tworzenia hello identyfikatora URI połączenia SAS.

Jeśli używasz ad hoc identyfikatora URI, masz trzy opcje. Można wystawiać tokeny sygnatury dostępu Współdzielonego z zasadami wygasania krótki i po prostu poczekaj, aż hello tooexpire sygnatury dostępu Współdzielonego. Można zmienić lub usunąć hello zasobów (przy założeniu, że hello token był tooa zakresie pojedynczego obiektu). Klucze konta magazynu hello, można zmienić. Ta opcja ostatniego może mieć duży wpływ, w zależności od tego, jak wiele usług korzystają z tego konta magazynu i prawdopodobnie nie oczekiwał toodo bez niektóre planowania.

Jeśli używasz sygnatury dostępu Współdzielonego uzyskane z zasad dostępu przechowywany, można usunąć dostęp, odwołując hello przechowywane zasady dostępu — Zmień go tak, aby już wygasł, albo usuń go całkowicie. Aktywne natychmiast i unieważnia co SAS utworzone za pomocą tego przechowywane zasad dostępu. Aktualizowanie lub usuwanie hello przechowywane zasady dostępu może mieć wpływ na osób uzyskuje dostęp do tego określonego kontenera, udziału plików, tabel lub kolejek za pomocą sygnatury dostępu Współdzielonego, ale jeśli hello klientów są zapisywane, dzięki czemu żądają nowe skojarzenia zabezpieczeń, gdy hello stary staje się nieprawidłowy, to będzie działać prawidłowo.

Ponieważ przy użyciu sygnatury dostępu Współdzielonego uzyskane z zasad dostępu do przechowywanych umożliwia toorevoke możliwości hello czy SAS, jest ona hello zalecane najlepsze praktyki tooalways Użyj przechowywane zasad dostępu, gdy jest to możliwe.

#### <a name="resources"></a>Zasoby
Aby uzyskać szczegółowe informacje na temat używania sygnatur dostępu współdzielonego i przechowywane zasad dostępu, wraz z przykładami zapoznaj się z toohello następujące artykuły:

* Są to hello odwołanie artykułów.

  * [Usługa SAS](https://msdn.microsoft.com/library/dn140256.aspx)

    Ten artykuł zawiera przykłady użycia SAS poziomu usług z obiektów blob, kolejki komunikatów, zakresy tabeli i plików.
  * [Utworzenie sygnatury dostępu Współdzielonego usługi](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Utworzenie konta SAS](https://msdn.microsoft.com/library/mt584140.aspx)
* Są to samouczki dotyczące użycia hello .NET klienta biblioteki toocreate sygnatur dostępu współużytkowanego i przechowywane zasad dostępu.

  * [Przy użyciu sygnatury dostępu współdzielonego (SAS)](storage-dotnet-shared-access-signature-part-1.md)
  * [Udostępnione sygnatur dostępu, część 2: Tworzenie i sygnatury dostępu Współdzielonego za pomocą hello usługi Blob](storage-dotnet-shared-access-signature-part-2.md)

    Ten artykuł zawiera wyjaśnienie hello modelu sygnatur dostępu Współdzielonego, przykłady sygnatury dostępu współdzielonego i zalecenia dotyczące najlepszych praktyk hello Użyj SAS. Opisano również jest odwołanie hello hello uprawnienia przyznane.
* Ograniczanie dostępu według adresu IP (IP ACL)

  * [Co to jest punkt końcowy listy kontroli dostępu (ACL)?](../virtual-network/virtual-networks-acl.md)
  * [Utworzenie sygnatury dostępu Współdzielonego usługi](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    To jest hello odwołanie artykułem dla skojarzeń zabezpieczeń poziomu usługi; składa się z przykładem IP ACLing.
  * [Utworzenie konta SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    To jest artykuł odwołanie hello na poziomie konta SAS; składa się z przykładem IP ACLing.
* Authentication

  * [Uwierzytelnianie dla hello usług magazynu Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Pierwsze kroki samouczka sygnatury dostępu współdzielonego

  * [Pierwsze kroki samouczka SAS](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania
### <a name="transport-level-encryption--using-https"></a>Szyfrowanie na poziomie transportu — przy użyciu protokołu HTTPS
Kolejny krok należy wykonać tooensure hello bezpieczeństwa danych usługi Azure Storage jest tooencrypt hello danych między powitania klienta i usługi Azure Storage. zalecenie pierwszy Hello jest tooalways Użyj hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS) protokołu, który zapewnia bezpieczną komunikację za pośrednictwem hello publicznej sieci Internet.

bezpieczny kanał komunikacyjny toohave, zawsze należy używać protokołu HTTPS podczas wywoływania hello interfejsów API REST lub uzyskiwanie dostępu do obiektów w magazynie. Ponadto **sygnatury dostępu współdzielonego**, które mogą być używane toodelegate dostępu tooAzure magazynu obiektów, obejmują toospecify opcji tego hello tylko przy użyciu sygnatury dostępu współdzielonego, upewniając się, że każdy można użyć protokołu HTTPS Wysyłanie linków z tokenami SAS użyje hello odpowiedni protokół.

Można wymusić hello korzystanie z protokołu HTTPS podczas wywoływania metody hello interfejsów API REST tooaccess obiektów na kontach magazynu przez włączenie [bezpieczny transfer wymagane](storage-require-secure-transfer.md) dla konta magazynu hello. Połączenia przy użyciu protokołu HTTP będą przyjmowane, gdy ta opcja jest włączona.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Szyfrowanie podczas przesyłania z udziałami plików Azure
Magazyn plików Azure obsługuje protokołu HTTPS, używając hello interfejsu API REST, ale jest najczęściej używany jako udział plików SMB dołączony tooa maszyny Wirtualnej. Protokół SMB 2.1 nie obsługuje szyfrowania, więc połączeń są dozwolone jedynie w ramach hello sam region platformy Azure. Jednak protokół SMB 3.0 obsługuje szyfrowanie i jest dostępna w systemie Windows Server 2012 R2, Windows 8, Windows 8.1 i Windows 10, umożliwiając między region dostępu, a nawet dostępu na pulpicie hello.

Należy pamiętać, że chociaż udziały plików platformy Azure mogą być używane w systemie Unix, powitania klienta SMB w systemie Linux jeszcze nie obsługuje szyfrowania, więc dostęp jest dozwolony tylko w obrębie regionu platformy Azure. Obsługa szyfrowania dla systemu Linux znajduje się na plan hello deweloperów Linux odpowiedzialny za funkcje protokołu SMB. Podczas dodawania szyfrowania, konieczne będzie hello tej samej możliwości dostępu do udziału plików Azure w systemie Linux, podobnie jak w przypadku systemu Windows.

Można wymusić użycie hello szyfrowania z hello usługi pliki Azure przez włączenie [bezpieczny transfer wymagane](storage-require-secure-transfer.md) dla konta magazynu hello. Jeśli przy użyciu hello interfejsów API REST, wymagany jest protokół HTTPs. Dla protokołu SMB tylko połączenia protokołu SMB, które obsługuje szyfrowanie połączenie zostanie nawiązane pomyślnie.

#### <a name="resources"></a>Zasoby
* [Jak toouse magazyn plików Azure z systemem Linux](storage-how-to-use-files-linux.md)

  W tym artykule opisano, jak toomount plików Azure udostępnianie plików systemu i przekaż/Pobierz systemu Linux.
* [Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows](storage-dotnet-how-to-use-files.md)

  Ten artykuł zawiera omówienie udziały plików platformy Azure i w jaki sposób toomount i używać ich przy użyciu programu PowerShell i .NET.
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)

  W tym artykule ogłasza hello ogólnej dostępności usługi Magazyn plików Azure i zawiera szczegółowe informacje techniczne dotyczące szyfrowania hello protokołu SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Przy użyciu toosecure danych szyfrowania po stronie klienta, wysyłanie toostorage
Inną opcją, która pomaga zagwarantować, że dane są bezpieczne podczas ich przesyłania między aplikacją klienta i magazynu jest szyfrowanie po stronie klienta. Witaj, dane są szyfrowane przed przesyłane do usługi Azure Storage. Podczas pobierania danych hello z usługi Azure Storage, hello dane zostaną odszyfrowane, po odebraniu na powitania po stronie klienta. Mimo że hello dane są szyfrowane, przechodzi przez sieć hello, zalecamy również używać protokołu HTTPS, ponieważ ta kolumna ma wbudowane którego zmniejszenia wpływu na powitania integralność danych hello błędy sieciowe sprawdzania integralności danych.

Szyfrowanie po stronie klienta jest również szyfrowanie danych magazynowanych, jak hello dane są przechowywane w postaci zaszyfrowanej. Będzie omawianiu to bardziej szczegółowo w sekcji hello na [szyfrowanie magazynowanych](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Szyfrowanie magazynowanych
Istnieją trzy funkcje platformy Azure umożliwiających szyfrowanie przechowywanych. Szyfrowanie dysków Azure jest hello tooencrypt używanego systemu operacyjnego i dysków z danymi w maszyny wirtualne IaaS. Witaj innych dwa — są szyfrowania po stronie klienta i SSE — zarówno dane tooencrypt używanych w usłudze Azure Storage. Umożliwia każdy z nich, a następnie wykonaj porównanie i zobacz, gdy każda z nich może służyć.

Za pomocą szyfrowania po stronie klienta tooencrypt hello danych podczas przesyłania (które są także przechowywane w postaci zaszyfrowanej w magazynie), mogą preferować toosimply użycie protokołu HTTPS podczas transferu hello i ma niewłaściwy dla toobe danych hello automatycznie szyfrowane, gdy jest przechowywane. Istnieją dwa sposoby toodo to--szyfrowania dysków Azure i SSE. Co najmniej jedna jest używana toodirectly szyfrowania hello danych na dyskach systemu operacyjnego i danych używany przez maszyny wirtualne i hello innych jest używane tooencrypt danymi zapisywanymi tooAzure magazynu obiektów Blob.

### <a name="storage-service-encryption-sse"></a>Szyfrowanie usługi Magazyn (SSE)
SSE umożliwia toorequest, że Usługa magazynu hello automatycznie szyfrowania danych hello podczas jej pisania tooAzure magazynu. Po przeczytaniu hello danych z usługi Magazyn Azure zostanie odszyfrowany przez usługę magazynu hello przed zwróceniem. Dzięki temu toosecure danych bez konieczności toomodify kod lub Dodaj aplikacje tooany kodu.

To ustawienie, które stosuje toohello konta całego magazynu. Można włączyć i wyłączyć tę funkcję, zmieniając wartość hello hello ustawienia. toodo, można użyć hello hello portalu Azure, programu PowerShell, interfejsu wiersza polecenia Azure, interfejsu API REST dostawcy zasobów magazynu hello lub hello biblioteki klienta usługi Storage platformy .NET. SSE jest domyślnie wyłączona.

W tej chwili hello klucze szyfrowania hello są zarządzane przez firmę Microsoft. Firma Microsoft pierwotnie Generuj klucze hello i zarządzaj nimi hello bezpiecznego magazynu kluczy hello, a także regularne obrotu hello, zgodnie z definicją w wewnętrznych zasad firmy Microsoft. W przyszłości hello będzie pobrać toomanage możliwości hello kluczy szyfrowania i podaj ścieżkę migracji z kluczy zarządzany przez firmę Microsoft toocustomer zarządzanych kluczy.

Ta funkcja jest dostępna dla kont Standard i Premium Storage utworzonych przy użyciu modelu wdrażania usługi Resource Manager hello. SSE stosuje tylko tooblock obiektów blob, stronicowe obiekty BLOB i uzupełnialnych obiektów blob. Witaj innych typów danych, w tym tabel, kolejek i plików, nie będą szyfrowane.

Dane są szyfrowane tylko wtedy, gdy jest włączone SSE i zapisywania danych hello tooBlob magazynu. Włączanie lub wyłączanie SSE nie wpływa na istniejących danych. Innymi słowy włączenie szyfrowania nie wrócić do poprzedniej strony i szyfrowania danych, która już istnieje; nie powoduje odszyfrowania danych hello, która już istnieje po wyłączeniu SSE.

Chcąc toouse tej funkcji w programie klasycznym konta magazynu, można utworzyć nowe konto magazynu Menedżera zasobów i używanie narzędzia AzCopy toocopy hello danych toohello nowego konta.

### <a name="client-side-encryption"></a>Szyfrowanie po stronie klienta
Wspomniano szyfrowania po stronie klienta przy omawianiu hello szyfrowania hello danych podczas przesyłania. Ta funkcja umożliwia tooprogrammatically należy szyfrować danych w aplikacji klienta przed wysłaniem przez toobe przewodowy hello zapisywane tooAzure magazynu i tooprogrammatically odszyfrowywania danych po pobraniu go z magazynu Azure.

To zapewnia szyfrowanie podczas przesyłania, ale także hello funkcji szyfrowania w stanie spoczynku. Należy pamiętać o tym, mimo że hello dane są szyfrowane podczas przesyłania, nadal zaleca się przy użyciu protokołu HTTPS tootake zaletą hello kontroli integralności danych wbudowanych, które zmniejszenia wpływu na powitania integralność danych hello błędy sieci.

Przykładem gdzie tej opcji można użyć jest, jeśli masz aplikację sieci web przechowuje obiekty BLOB i pobiera obiekty BLOB i chcesz toobe danych i aplikacji hello należycie zabezpieczone. W takim przypadku użyje szyfrowania po stronie klienta. Hello ruch między powitania klienta i hello usługi obiektów Blob Azure zawiera zasób hello szyfrowane, a nikt nie można zinterpretować hello danych podczas przesyłania i przywróć ją do prywatnego obiektów blob.

Szyfrowanie po stronie klienta jest wbudowana w hello Java i biblioteki klienta magazynu .NET hello, które z kolei używają hello klucza magazynu interfejsów API usługi Azure, dzięki czemu pretty tooimplement można. proces szyfrowania i odszyfrowywania danych hello Hello stosowana metoda koperty hello i przechowuje metadane używane przez szyfrowanie hello w każdym obiekcie magazynu. Na przykład dla obiektów blob, przechowuje go w hello metadane obiektu blob, natomiast w przypadku kolejek, dodanie go tooeach kolejki wiadomości.

Do szyfrowania hello się można wygenerować i zarządzanie kluczami szyfrowania. Umożliwia także klucze generowane przez hello biblioteki klienta magazynu Azure lub program hello Azure Key Vault Generuj klucze hello. Można przechowywać kluczy szyfrowania w Twoim magazynie kluczy lokalnymi lub można przechowywać w usłudze Azure Key Vault. Usługa Azure Key Vault umożliwia kluczy tajnych toohello dostępu toogrant z usługi Azure Key Vault toospecific użytkowników przy użyciu usługi Azure Active Directory. Oznacza to, że nie tylko każdy może odczytywać hello Azure Key Vault i pobieranie kluczy hello, używanego do szyfrowania po stronie klienta.

#### <a name="resources"></a>Zasoby
* [Szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md)

  W tym artykule przedstawiono sposób toouse szyfrowania po stronie klienta z usługi Azure Key Vault, w tym jak toocreate hello KEK i zapisz go w magazynie hello przy użyciu programu PowerShell.
* [Magazyn kluczy szyfrowania po stronie klienta i Azure dla magazynu Microsoft Azure](storage-client-side-encryption.md)

  W tym artykule podaje wyjaśnienie szyfrowania po stronie klienta i zawiera przykłady użycia powitania klienta biblioteki tooencrypt i odszyfrowywania zasobów magazynu z hello cztery usługi magazynu. Zawiera ona również informacje o usługi Azure Key Vault.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Przy użyciu szyfrowania dysków Azure dysków tooencrypt używany przez maszyny wirtualne
Szyfrowanie dysków Azure to nowa funkcja. Ta funkcja umożliwia dysków systemu operacyjnego hello tooencrypt i dysków danych używanych przez maszyny wirtualne IaaS. W systemie Windows hello dyski są szyfrowane za pomocą technologii szyfrowania BitLocker standardowych. Dla systemu Linux dyski hello są szyfrowane za pomocą technologii hello DM-Crypt. To jest zintegrowany z usługą Azure Key Vault tooallow możesz toocontrol i zarządzać kluczami szyfrowania dysku hello.

rozwiązanie Hello obsługuje następujące scenariusze dla maszyn wirtualnych IaaS, jeśli są włączone w systemie Microsoft Azure hello:

* Integracja z usługi Azure Key Vault
* Maszyny wirtualne warstwy standardowa: [A, D DS, G, GS i itp szeregów maszyn wirtualnych IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Włączenie szyfrowania w systemach Windows i maszyn wirtualnych systemu Linux IaaS
* Wyłączenie szyfrowania systemu operacyjnego i danych dyski dla maszyn wirtualnych IaaS systemu Windows
* Wyłączenie szyfrowania dla dysków z danymi dla maszyn wirtualnych systemu Linux IaaS
* Włączenie szyfrowania na maszynach wirtualnych IaaS, którego uruchomiono system operacyjny klienta systemu Windows
* Włączenie szyfrowania na woluminach ze ścieżki instalacji
* Włączenie szyfrowania na maszynach wirtualnych systemu Linux, które są skonfigurowane przy użyciu rozkładanie (RAID) przy użyciu mdadm
* Włączenie szyfrowania na maszynach wirtualnych systemu Linux przy użyciu LVM dla dysków z danymi
* Włączenie szyfrowania na maszynach wirtualnych systemu Windows, które są skonfigurowane przy użyciu funkcji miejsca do magazynowania
* Wszystkie publiczne regiony platformy Azure są obsługiwane.

rozwiązanie Hello nie obsługuje następujące scenariusze, funkcje i technologie w wersji hello hello:

* Maszyny wirtualne IaaS warstwa podstawowa
* Wyłączenie szyfrowania na dysku systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS
* Maszyny wirtualne IaaS, utworzony przy użyciu hello klasycznego metodę tworzenia maszyny Wirtualnej
* Integracja z lokalnej usługi zarządzania kluczami
* Magazyn plików Azure (udostępnionego systemu plików), sieciowego systemu plików (NFS), dynamiczne woluminy i maszyn wirtualnych systemu Windows, które są skonfigurowane przy użyciu systemów opartych na oprogramowaniu RAID


> [!NOTE]
> Szyfrowanie dysków systemu operacyjnego Linux jest obecnie obsługiwany na powitania po dystrybucje systemu Linux: RHEL 7.2, CentOS 7.2n i Ubuntu 16.04.
>
>

Ta funkcja zapewnia, że wszystkie dane na dyskach maszyny wirtualnej jest szyfrowane, gdy w usłudze Azure Storage.

#### <a name="resources"></a>Zasoby
* [Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Porównanie szyfrowania dysków Azure, SSE i szyfrowania po stronie klienta
#### <a name="iaas-vms-and-their-vhd-files"></a>Maszyny wirtualne IaaS i swoich plików wirtualnego dysku twardego
W przypadku dysków używanych przez maszyny wirtualne IaaS zaleca się przy użyciu szyfrowania dysków Azure. Można włączyć plików VHD hello tooencrypt SSE, które są używane tooback tych dysków w magazynie Azure, ale są szyfrowane tylko nowo napisanych danych. Oznacza to, że jeśli możesz utworzyć Maszynę wirtualną, a następnie włączyć SSE na powitania konta magazynu, które znajduje się plik VHD hello, tylko hello zmiany będą szyfrowane, nie hello oryginalny plik wirtualnego dysku twardego.

Jeśli tworzysz Maszynę wirtualną przy użyciu obrazu z portalu Azure Marketplace hello Azure wykonuje [skrócona kopiowania](https://en.wikipedia.org/wiki/Object_copying) z hello tooyour obraz konta magazynu w usłudze Azure Storage, a nie są szyfrowane nawet wtedy, gdy SSE włączone. Po tworzy hello maszyny Wirtualnej i uruchamia aktualizacji obrazu hello, szyfrowanie danych hello SSE zostanie uruchomiony. Z tego powodu jest najlepszym toouse, szyfrowania dysków Azure na maszyny wirtualne utworzone na podstawie obrazów w portalu Azure Marketplace hello należy je w pełni szyfrowane.

Przełączeniem zaszyfrowane wstępnie maszyny Wirtualnej na platformie Azure z lokalnej będzie można tooupload stanie hello szyfrowania kluczy tooAzure magazyn kluczy i nadal korzystać z szyfrowania hello tej maszyny Wirtualnej, aby były używane lokalnie. Szyfrowanie dysków Azure jest włączone toohandle tego scenariusza.

Jeśli masz niezaszyfrowane wirtualnego dysku twardego z lokalnej, należy przekazać go do galerii hello jako obraz niestandardowy i udostępnić Maszynę wirtualną z niego. Jeśli możesz to zrobić za pomocą szablonów usługi Resource Manager hello, poproś go tooturn na szyfrowania dysków Azure po jego rozruchu hello maszyny Wirtualnej.

Podczas dodawania dysku danych i zainstalować go na powitania maszyny Wirtualnej, można włączyć szyfrowania dysków Azure na tym dysku danych. Go zostanie najpierw szyfrowania dysku danych lokalnie, a następnie warstwa zarządzania usługi hello będzie wykonaj opóźnieniem zapisu względem magazynu, zawartość magazynu hello jest zaszyfrowana.

#### <a name="client-side-encryption"></a>Szyfrowania po stronie klienta
Szyfrowanie po stronie klienta jest hello najbezpieczniejszą metodą szyfrowania danych, ponieważ szyfruje go przed przesyłania i szyfruje hello przechowywanych danych. Jednak wymagają, aby dodać aplikacje tooyour kodu przy użyciu magazynu, który może nie być toodo. W takich przypadkach można użyć HTTPs dla danych podczas przesyłania i SSE tooencrypt hello przechowywanych danych.

Szyfrowanie po stronie klienta można zaszyfrować jednostek tabeli, kolejki komunikatów i obiekty BLOB. Z SSE można szyfrować obiektów blob. Jeśli potrzebujesz kolejek i tabel toobe dane zaszyfrowane, należy używać szyfrowania po stronie klienta.

Szyfrowanie po stronie klienta zarządza całkowicie aplikacji hello. Jest to najbezpieczniejsza metoda hello, ale wymaga toomake programowe zmiany tooyour aplikacji i wprowadzone procesy zarządzania kluczami. Spowoduje to używać, gdy chce hello dodatkowych zabezpieczeń podczas przesyłania, a chcesz Twojej toobe przechowywane dane zaszyfrowane.

Szyfrowanie po stronie klienta jest większe obciążenie na powitania klienta i masz tooaccount tego w planów skalowalność, zwłaszcza, jeśli są szyfrowania i przesyłania dużych ilości danych.

#### <a name="storage-service-encryption-sse"></a>Szyfrowanie usługi Magazyn (SSE)
SSE jest zarządzana przez usługi Azure Storage. Przy użyciu SSE nie zapewnia bezpieczeństwa hello hello danych podczas przesyłania, ale jego szyfrowania danych hello są zapisywane tooAzure magazynu. Nie ma żadnych wpływu na wydajność hello podczas używania tej funkcji.

Można tylko szyfrowania blokowych obiektów blob, uzupełnialnych obiektów blob i stronicowe przy użyciu SSE. Jeśli potrzebujesz danych tabeli tooencrypt lub kolejki, należy rozważyć przy użyciu szyfrowania po stronie klienta.

Jeśli archiwum lub biblioteka plików VHD, które używa jako podstawy do tworzenia nowych maszyn wirtualnych, Utwórz nowe konto magazynu, włączyć SSE, a następnie przekaż konta toothat pliki VHD hello. Te pliki VHD będą szyfrowane przez Magazyn Azure.

Jeśli masz szyfrowania dysków Azure włączone hello dysków maszyny Wirtualnej i włączona na koncie magazynu hello zawierający pliki VHD hello SSE będzie działać prawidłowo; spowoduje danych nowo zapisywane szyfrowany dwa razy.

## <a name="storage-analytics"></a>Analityka magazynu
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Przy użyciu typu autoryzacji toomonitor analityka magazynu
Dla każdego konta magazynu należy włączyć rejestrowanie tooperform analityka magazynu Azure i zapisania danych metryki. Jest to toouse doskonałe narzędzie, gdy mają metryki wydajności hello toocheck konta magazynu, lub potrzeby tootroubleshoot konta magazynu, ponieważ występują problemy z wydajnością.

Inny element danych wyświetlanych w dziennikach analityka magazynu hello jest hello metoda uwierzytelniania używana przez inną przy uzyskiwaniu dostępu do magazynu. Na przykład z magazynem obiektów Blob widać, użycie sygnaturę dostępu współdzielonego i klucze konta magazynu hello lub jeśli blob hello dostęp publiczny.

Może to być naprawdę pomocne, jeśli są ściśle ochrona toostorage dostępu. Na przykład w magazynie obiektów Blob można ustawić dla wszystkich tooprivate kontenery hello i zaimplementować hello korzystania z usługi SAS w całej aplikacji. Następnie można sprawdzić dzienniki hello regularnie toosee czy obiektów blob są dostępne przy użyciu kluczy konta magazynu hello, które mogą wskazywać naruszenia zabezpieczeń, czy obiekty BLOB hello są publiczne, ale nie powinny być one.

#### <a name="what-do-hello-logs-look-like"></a>Jak hello dzienniki wyglądają?
Po włączyć metryki konta magazynu hello i rejestrowanie za pośrednictwem hello portalu Azure, dane analityczne rozpocznie tooaccumulate szybko. Rejestrowanie Hello i metryki dla każdej usługi jest oddzielona; Rejestrowanie Hello tylko są zapisywane w przypadku działania na tym koncie magazynu podczas metryki hello będą rejestrowane co minutę, co godzinę lub codziennie, w zależności od sposobu skonfigurowania.

Witaj dzienniki są przechowywane w blokowych obiektów blob w kontenerze o nazwie $logs hello koncie magazynu. Ten kontener jest tworzony automatycznie, gdy analityka magazynu jest włączona. Po utworzeniu tego kontenera nie można usunąć, mimo że można usunąć jego zawartość.

W ramach kontenera hello $logs znajduje się tam folder dla każdej usługi, a następnie istnieją podfoldery dla hello roku miesiąc/dzień/na godzinę. W obszarze godzinę po prostu są numerowane hello dzienniki. Jest to jakie hello będzie wyglądać strukturę katalogów:

![Wyświetl pliki dziennika](./media/storage-security-guide/image1.png)

Jest rejestrowane co tooAzure żądania magazynu. Oto migawki pliku dziennika, przedstawiający hello pierwszy mało pól.

![Migawki pliku dziennika](./media/storage-security-guide/image2.png)

Widać, których można używać tootrack dzienniki hello dowolnego rodzaju konto magazynu tooa wywołania.

#### <a name="what-are-all-of-those-fields-for"></a>Co to są wszystkich tych pól?
Istnieje na liście poniżej zasobów hello artykułu, który zawiera listę hello hello wiele pól w hello dzienników i ich używać. Oto hello Lista pól w kolejności:

![Migawki pól w pliku dziennika](./media/storage-security-guide/image3.png)

Interesuje nas hello wpisy GetBlob i sposób ich uwierzytelniania, dlatego firma Microsoft muszą toolook dla wpisów z operacji typu "Get-obiektu Blob", a sprawdzić stan żądania hello (4<sup>th</sup> kolumny) i typ autoryzacji hello (8<sup>th</sup> kolumny).

Na przykład w hello najpierw kilka wierszy na powyższej liście hello, stan żądania hello jest "Powodzenie" i typ autoryzacji hello "uwierzytelnieniu". Oznacza to, że hello żądania została zweryfikowana przy użyciu klucza konta magazynu hello.

#### <a name="how-are-my-blobs-being-authenticated"></a>Jak są jest uwierzytelniane Moje obiektów blob?
Mamy trzech przypadkach, w których Dbamy o.

1. Witaj obiektu blob jest publiczny i jest on dostępny przy użyciu adresu URL bez sygnaturę dostępu współdzielonego. W takim przypadku stan żądania hello jest "AnonymousSuccess" i "anonymous" jest typ autoryzacji hello.

   1.0; 2015-11-17T02:01:29.0488963Z; GetBlob; **AnonymousSuccess**200 124; 37; **anonimowe**; mystorage...
2. Obiekt blob Hello jest prywatny i została użyta z sygnaturą dostępu współdzielonego. W takim przypadku stan żądania hello jest "SASSuccess" i typ autoryzacji hello jest "sas".

   1.0; 2015-11-16T18:30:05.6556115Z; GetBlob; **SASSuccess**200 416; 64; **sygnatury dostępu współdzielonego**; mystorage...
3. Hello blob jest prywatny i klucz magazynu hello był używany tooaccess go. W takim przypadku stan żądania hello jest "**Powodzenie**"i typ autoryzacji hello jest"**uwierzytelniony**".

   1.0; 2015-11-16T18:32:24.3174537Z; GetBlob; **Powodzenie**206 59; 22; **uwierzytelniony**; mystorage...

Można użyć hello tooview programu Microsoft Message Analyzer i analizować te dzienniki. Obejmuje on możliwości wyszukiwania i filtrowania. Na przykład może być toosearch dla wystąpień toosee GetBlob w przypadku użycia hello oczekiwań, tj. toomake się, że ktoś jest nie uzyskiwanie dostępu do konta magazynu niewłaściwie.

#### <a name="resources"></a>Zasoby
* [Analityka magazynu](storage-analytics.md)

  Ten artykuł zawiera omówienie analityka magazynu i w jaki sposób tooenable je.
* [Format dziennika analityka magazynu](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  W tym artykule przedstawiono hello Format dziennika analityka magazynu, a szczegóły hello dostępnych pól, w tym — typ uwierzytelniania, co oznacza hello typu uwierzytelniania używanego dla żądania hello.
* [Monitor konta magazynu w hello portalu Azure](storage-monitor-storage-account.md)

  W tym artykule przedstawiono sposób tooconfigure monitorowanie metryki i rejestrowania dla konta magazynu.
* [Rozwiązywanie problemów na trasie przy użyciu metryk usługi Azure Storage i rejestrowania, AzCopy i analizatora komunikatów](storage-e2e-troubleshooting.md)

  Ten artykuł zawiera informacje o Rozwiązywanie problemów przy użyciu hello analityka magazynu i pokazuje, jak toouse hello programu Microsoft Message Analyzer.
* [Przewodnik operacyjny analizatora wiadomości firmy Microsoft](https://technet.microsoft.com/library/jj649776.aspx)

  W tym artykule jest odwołanie hello hello programu Microsoft Message Analyzer i zawiera łącza tooa samouczek szybki start i Podsumowanie funkcji.

## <a name="cross-origin-resource-sharing-cors"></a>Współużytkowanie zasobów między źródłami (CORS)
### <a name="cross-domain-access-of-resources"></a>Dostęp z innych domen zasobów
Gdy przeglądarki sieci web działa w jednej domenie wysyła żądanie HTTP dla zasobu z innej domeny, jest to żądanie HTTP cross-origin. Na przykład strona HTML z contoso.com zażąda hostowanych na fabrikam.blob.core.windows.net jpeg. Ze względów bezpieczeństwa przeglądarki ograniczanie żądań HTTP cross-origin inicjowane przy użyciu skryptów, takich jak JavaScript. Oznacza to, że jeśli kod JavaScript na stronie sieci web w domenie contoso.com zażąda tej jpeg na fabrikam.blob.core.windows.net, przeglądarki hello nie zezwoli hello żądania.

Co to oznacza ma toodo z usługą Azure Storage? Dobrze, jeśli przechowujesz statycznych zasobów, takich jak pliki danych JSON i XML w magazynie obiektów Blob przy użyciu konta magazynu o nazwie firmy Fabrikam, domena hello trwałych hello będzie fabrikam.blob.core.windows.net i aplikacji sieci web contoso.com hello nie będą mogli tooaccess je przy użyciu języka JavaScript, ponieważ różnią się hello domen. Jest to również wartość true, jeśli próbujesz toocall jedną z usług magazynu Azure — takie jak magazyn tabel — Witaj zwracających toobe danych JSON przetworzonych przez program hello JavaScript klienta.

#### <a name="possible-solutions"></a>Możliwe rozwiązania
Jednym ze sposobów tooresolve jest tooassign domeny niestandardowej, takich jak toofabrikam.blob.core.windows.net "storage.contoso.com". Hello problem jest, że konto domeny niestandardowej tooone magazynu można przypisać tylko. Co zrobić, jeśli zasoby hello są przechowywane w wielu kont magazynu?

Inny sposób tooresolve to działanie aplikacji sieci web hello toohave jako serwer proxy dla połączenia magazynu hello. Oznacza to, podczas przekazywania pliku tooBlob pamięci masowej, aplikacji sieci web hello czy albo Zapisz lokalnie, a następnie skopiować go tooBlob magazynu lub zostaną odczytać wszystkich go do pamięci, a następnie zapisz je tooBlob magazynu. Alternatywnie można zapisać dedykowanych aplikacji sieci web (np. interfejsu API sieci Web) przekazuje hello plików lokalnie i zapisuje je tooBlob magazynu. W obu przypadkach należy tooaccount dla tej funkcji podczas określania skalowalność hello musi.

#### <a name="how-can-cors-help"></a>Jak może pomóc CORS
Magazyn Azure umożliwia tooenable CORS — Cross udostępniania zasobów pochodzenia. Dla każdego konta magazynu można określić domeny, które mogą uzyskiwać dostęp do zasobów hello na tym koncie magazynu. Na przykład w tym przypadku opisanych powyżej firma Microsoft można włączyć mechanizm CORS na koncie magazynu fabrikam.blob.core.windows.net hello i skonfigurować tooallow toocontoso.com dostępu. Następnie contoso.com aplikacji sieci web hello bezpośrednio dostęp do zasobów hello w fabrikam.blob.core.windows.net.

Jeden element toonote jest czy CORS zezwala na dostęp, ale nie zapewnia uwierzytelniania, który jest wymagany dla wszystkich dostępu publicznego zasobów magazynu. To oznacza, że użytkownik ma dostęp tylko do obiektów blob, jeśli są one publiczne lub dołączeniu zapewniając sygnaturę dostępu współdzielonego hello odpowiednich uprawnień. Tabel, kolejek i plików nie mają publicznego dostępu i wymagają sygnatury dostępu Współdzielonego.

Domyślnie CORS jest wyłączona na wszystkich usług. Mechanizm CORS można włączyć, używając hello interfejsu API REST lub hello magazynu klienta biblioteki toocall jedną z hello metody tooset hello usługi zasad. Po wykonaniu tej czynności, możesz dołączyć regułę CORS, która jest w formacie XML. Oto przykład reguły CORS, która została ustawiona przy użyciu operacji ustawić właściwości usługi hello hello usługa Blob dla konta magazynu. Można wykonać tej operacji za pomocą biblioteki klienta usługi storage hello lub hello interfejsów API REST usługi Azure Storage.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Oto, co oznacza każdy wiersz:

* **AllowedOrigins** informuje żądać i odbierać dane z usługi magazynowania hello niezgodny domen. To mówi, że zarówno contoso.com i fabrikam.com można zażądać danych z magazynu obiektów Blob na koncie magazynu określonym. Można również ustawić tego symbolu wieloznacznego tooa (\*) tooallow tooaccess domen wszystkich żądań.
* **AllowedMethods** to hello listę metod (zleceń HTTP żądania), które mogą być używane podczas tworzenia żądania hello. W tym przykładzie są dozwolone tylko PUT i GET. Można ustawić tego symbolu wieloznacznego tooa (\*) tooallow używane wszystkie toobe metody.
* **AllowedHeaders** to Żądanie hello nagłówki, które hello domeny pochodzenia można określić podczas tworzenia żądania hello. W tym przykładzie wszystkie nagłówki metadanych, począwszy od x-ms-meta-data x-ms-meta docelowego, a x-ms-meta-abc są dozwolone. Witaj wieloznacznego (\*) wskazuje, że wszystkie nagłówka, począwszy od hello określić prefiks jest dozwolone.
* **ExposedHeaders** informuje nagłówki odpowiedzi, które powinny zostać ujawnione przez emitenta żądania toohello hello w przeglądarce. W tym przykładzie wszystkie nagłówka, począwszy od "x-ms - meta-" mają być widoczne.
* **MaxAgeInSeconds** to hello maksymalną ilość czasu, w przeglądarce zostanie buforowania przez żądania wstępnego opcje hello. (Aby uzyskać więcej informacji na temat żądania wstępnego hello Sprawdź hello pierwszego artykułu poniżej).

#### <a name="resources"></a>Zasoby
Aby uzyskać więcej informacji na temat mechanizmu CORS i w jaki sposób tooenable, zapoznaj się z tych zasobów.

* [Obsługa udostępniania zasobów między źródłami (CORS) hello usług magazynu Azure w witrynie Azure.com](storage-cors-support.md)

  Ten artykuł zawiera omówienie mechanizmu CORS i jak tooset hello zasady hello innego magazynu usługi.
* [Obsługa udostępniania zasobów między źródłami (CORS) hello usług magazynu Azure w witrynie MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Jest to hello dokumentacji dla obsługi mechanizmu CORS dla usług magazynu Azure hello. Ma tooarticles łącza stosowania tooeach usługi magazynu i przedstawiono przykład i opisano każdy element hello CORS pliku.
* [Usługi Microsoft Azure Storage: Wprowadzenie CORS](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  To jest łącze artykuł początkowej blog toohello announcing CORS i przedstawiający sposób toouse go.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Często zadawane pytania dotyczące zabezpieczeń usługi Azure Storage
1. **Jak można sprawdzić integralności hello hello obiektów blob, który I używam transferu do lub z usługi Azure Storage, jeśli nie można użyć protokołu HTTPS hello?**

   Jeśli z jakiegokolwiek powodu potrzebne toouse HTTP zamiast HTTPS, a użytkownik pracuje z blokowych obiektów blob, można użyć sprawdzanie MD5 toohelp Sprawdź integralność hello obiektów blob hello przesyłane. Pomoże to ochrony z sieci/transport layer błędów, ale niekoniecznie pośredniczące ataków.

   Jeśli używasz protokołu HTTPS, który zapewnia zabezpieczeń na poziomie transportu, następnie przy użyciu algorytmu MD5 sprawdzanie jest nadmiarowe i niepotrzebne.

   Aby uzyskać więcej informacji można znaleźć na powitania [Przegląd MD5 obiektów Blob Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **Informacje o zgodności FIPS dla hello stany USA Rządowych Stanów Zjednoczonych?**

   Witaj Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) definiuje algorytmy kryptograficzne zatwierdzone do użycia przez amerykański Systemów komputerowych federalnych hello ochrony poufnych danych. Włączanie FIPS tryb na serwerze z systemem Windows lub pulpitu informuje hello systemu operacyjnego należy używać tylko standardem FIPS algorytmów kryptograficznych. Jeśli aplikacja używa algorytmów niezgodnych, aplikacji hello zostaną przerwane. With.NET Framework w wersji 4.5.2 lub nowszego, aplikacja hello automatycznie przełącza algorytmów toouse zgodne ze standardem FIPS algorytmów kryptograficznych hello podczas hello komputer jest w trybie FIPS.

   Microsoft pozostawia jej w górę toodecide klienta tooeach czy tooenable trybie FIPS. Mamy nadzieję, że to nie ma powodu istotnych dla klientów, którzy nie są w trybie FIPS podmiotu toogovernment wykonawcze tooenable domyślnie.

   **Zasoby**

* [Dlaczego jest nie zalecamy "Tryb FIPS" już](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  W tym artykule na blogu powinien zawierać omówienie FIPS i objaśniono, dlaczego nie umożliwiają one trybie FIPS domyślnie.
* [FIPS 140 sprawdzania poprawności](https://technet.microsoft.com/library/cc750357.aspx)

  Ten artykuł zawiera informacje dotyczące sposobu produktów firmy Microsoft i modułów kryptograficznych zgodne ze standardem FIPS hello hello USA Federalnych.
* ["Kryptografia systemu: Użyj FIPS algorytmów szyfrowania, mieszania i podpisywania" efekty ustawienia zabezpieczeń w systemie Windows XP i w nowszych wersjach systemu Windows](https://support.microsoft.com/kb/811833)

  Ten artykuł zawiera informacje o użycie hello w trybie FIPS w starszych komputerów z systemem Windows.
