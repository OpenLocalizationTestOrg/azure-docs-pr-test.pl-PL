---
title: Magazyn klucz aaaSecure | Dokumentacja firmy Microsoft
description: "Zarządzaj uprawnieniami dostępu do magazynu kluczy na potrzeby zarządzania magazynami, kluczami i wpisami tajnymi. Model uwierzytelniania i autoryzacji dla magazynu kluczy i jak toosecure klucz magazynu"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Zabezpieczanie własnego magazynu kluczy
Usługa Azure Key Vault to usługa w chmurze, która zabezpiecza klucze szyfrowania i wpisy tajne (takie jak certyfikaty, parametry połączenia, hasła) dla aplikacji w chmurze. Ponieważ te dane są liter i biznesowe krytyczne, ma toosecure magazynów kluczy tooyour dostępu tylko autoryzowane aplikacji i użytkownicy mogą uzyskiwać dostęp do magazynu kluczy. Ten artykuł zawiera omówienie magazynu kluczy dostępu do modelu, wyjaśniono uwierzytelniania i autoryzacji i w tym artykule opisano, jak toosecure tookey dostępu do magazynu dla aplikacji w chmurze z przykładem.

## <a name="overview"></a>Omówienie
Magazyn kluczy tooa dostęp jest kontrolowany za pośrednictwem dwóch oddzielnych interfejsów: płaszczyzny zarządzania i płaszczyzna danych. Dla obu płaszczyzn odpowiednie uwierzytelnianie i autoryzacja jest wymagana przed wywołującego (użytkownik lub aplikacja) można uzyskać dostępu do magazynu tookey. W ramach uwierzytelniania ustalana hello tożsamości wywołującego hello podczas autoryzacji określa, jakie operacje hello wywołujący może tooperform.

Na potrzeby uwierzytelniania płaszczyzna zarządzania i płaszczyzna danych używają usługi Azure Active Directory. Na potrzeby autoryzacji płaszczyzna zarządzania używa kontroli dostępu opartej na rolach (RBAC), natomiast płaszczyzna danych używa zasad dostępu magazynu kluczy.

Oto krótkie omówienie hello tematy:

[Uwierzytelnianie przy użyciu usługi Azure Active Directory](#authentication-using-azure-active-directory) — w tej sekcji opisano, jak obiekt wywołujący jest uwierzytelniany w usłudze Azure Active Directory tooaccess magazynu kluczy za pomocą płaszczyzny zarządzania i płaszczyzna danych. 

[Płaszczyzna zarządzania i płaszczyzna danych](#management-plane-and-data-plane) — płaszczyzna zarządzania i płaszczyzna danych to dwie płaszczyzny używane do uzyskiwania dostępu do magazynu kluczy. Każda płaszczyzna dostępu obsługuje konkretne operacje. W tej sekcji opisano punkty końcowe dostępu hello, operacje obsługiwane i używane przez każdego płaszczyzny metody kontroli dostępu. 

[Kontrola dostępu płaszczyzny zarządzania](#management-plane-access-control) — w tej sekcji wyjaśniono zezwalania na dostęp toomanagement płaszczyzny operacji za pomocą kontroli dostępu opartej na rolach.

[Kontrola dostępu płaszczyzna danych](#data-plane-access-control) — w tej sekcji opisano, jak dane toocontrol zasad dostępu do magazynu kluczy toouse płaszczyzny dostępu.

[Przykład](#example) — w tym przykładzie przedstawiono sposób toosetup ACL dla magazynu kluczy tooallow trzech różnych zespołów (zespołu zabezpieczeń, deweloperzy/operatory i audytorów) tooperform toodevelop określonych zadań, zarządzanie i monitorowanie aplikacji na platformie Azure .

## <a name="authentication-using-azure-active-directory"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory
Po utworzeniu magazynu kluczy w subskrypcji platformy Azure jest automatycznie kojarzony z hello subskrypcji dzierżawy usługi Azure Active Directory. Wszystkie obiekty wywołujące (Użytkownicy i aplikacje) musi być zarejestrowany w tym tooaccess dzierżawy tego magazynu kluczy. Aplikacji lub użytkownik musi uwierzytelnić z magazynu kluczy tooaccess usługi Azure Active Directory. Dotyczy to płaszczyzny zarządzania tooboth i płaszczyzna danych programu access. W obu przypadkach aplikacja może uzyskiwać dostęp do magazynu kluczy na dwa sposoby:

* **dostęp użytkownika i aplikacji** — zwykle stosowany dla aplikacji, które uzyskują dostęp do magazynu kluczy w imieniu zalogowanego użytkownika. Program Azure PowerShell i witryna Azure Portal to przykłady tego typu dostępu. Istnieją dwa sposoby toousers dostępu toogrant: jednym ze sposobów jest toousers dostępu toogrant tak uzyskiwania dostępu do magazynu kluczy z poziomu dowolnej aplikacji i hello inny sposób toogrant magazynu tookey dostępu użytkownika tylko wtedy, gdy korzystają z określonej aplikacji (tooas określona tożsamość złożona). 
* **dostęp tylko do aplikacji** — w przypadku aplikacji, że demon usługi uruchamiać, zadań w tle uzyskuje tożsamość aplikacji hello itp. dostęp do toohello klucza magazynu.

W przypadku obu typów aplikacji, aplikacji hello jest uwierzytelniany w usłudze Azure Active Directory przy użyciu dowolnego hello [obsługiwane metody uwierzytelniania](../active-directory/active-directory-authentication-scenarios.md) i uzyskuje token. Metoda uwierzytelniania używana, zależy od typu aplikacji hello. Następnie aplikacja hello używa ten token i wysyła magazynu tookey żądania interfejsu API REST. W przypadku zarządzania płaszczyzny dostępu hello żądania są kierowane za pośrednictwem punktu końcowego usługi Azure Resource Manager. Podczas uzyskiwania dostępu do płaszczyzna danych, aplikacji hello komunikuje bezpośrednio tooa magazynu kluczy w punkcie końcowym. Dowiedz się więcej na powitania [przepływ uwierzytelniania całego](../active-directory/active-directory-protocols-oauth-code.md). 

Nazwa zasobu Hello, dla których aplikacja hello żąda token różni się w zależności od tego, czy dostęp do aplikacji hello płaszczyzny zarządzania lub płaszczyzna danych. Dlatego hello Nazwa zasobu jest albo zarządzania płaszczyzna danych płaszczyzny końcowy lub opisem w tabeli hello w dalszej części artykułu, w zależności od hello środowiska platformy Azure.

O jeden pojedynczy mechanizm uwierzytelniania tooboth płaszczyzny zarządzania oraz danych ma własną korzyści:

* Organizacje centralnie kontrolować magazynów kluczy tooall dostępu w organizacji
* Jeśli użytkownik opuści, natychmiast utracą dostęp tooall magazynów kluczy w organizacji hello
* Organizacje można dostosować uwierzytelniania za pomocą opcji hello w usłudze Azure Active Directory (na przykład włączenie uwierzytelniania wieloskładnikowego na zwiększyć bezpieczeństwo)

## <a name="management-plane-and-data-plane"></a>Płaszczyzna zarządzania i płaszczyzna danych
Usługa Azure Key Vault to usługa platformy Azure dostępna za pośrednictwem modelu wdrażania przy użyciu usługi Azure Resource Manager. Po utworzeniu magazynu kluczy uzyskujesz kontener wirtualny, wewnątrz którego możesz utworzyć inne obiekty, takie jak klucze, wpisy tajne i certyfikaty. Następnie możesz uzyskać dostępu do magazynu kluczy przy użyciu danych i płaszczyzny płaszczyzny tooperform określonych operacji zarządzania. Interfejs zarządzania płaszczyzny jest używane toomanage klucza magazynu siebie, takie jak tworzenie, usuwanie, aktualizowaniem atrybutów magazynu kluczy i ustawienie zasad dostępu dla płaszczyzny danych. Tooadd używany jest interfejs płaszczyzna danych, Usuń, modyfikowania i użyj hello kluczy, kluczy tajnych i certyfikaty przechowywane w magazynie kluczy.

Witaj zarządzania płaszczyzna danych płaszczyzny interfejsów i są dostępne za pośrednictwem różnych punktów końcowych (patrz tabela). Witaj drugiej kolumny w tabeli hello opisuje hello nazwy DNS dla tych punktów końcowych w różnych środowiskach Azure. trzecia kolumna Hello opisuje hello operacje, które można wykonywać z każdej warstwy dostępu. Każda płaszczyzna dostępu ma również swój własny mechanizm kontroli dostępu: w przypadku płaszczyzny zarządzania kontrola dostępu jest ustawiana przy użyciu kontroli dostępu opartej na rolach (RBAC) w usłudze Azure Resource Manager, natomiast w przypadku płaszczyzny danych kontrola dostępu jest ustawiana za pomocą zasad dostępu magazynu kluczy.

| Płaszczyzna dostępu | Punkty końcowe dostępu | Operacje | Mechanizm kontroli dostępu |
| --- | --- | --- | --- |
| Płaszczyzna zarządzania |**Cały świat:**<br> management.azure.com:443<br><br> **Chińska wersja platformy Azure:**<br> management.chinacloudapi.cn:443<br><br> **Wersja platformy Azure dla administracji USA:**<br> management.usgovcloudapi.net:443<br><br> **Niemiecka wersja platformy Azure:**<br> management.microsoftazure.de:443 |Tworzenie /odczyt/aktualizowanie/usuwanie magazynu kluczy <br> Ustawianie zasad dostępu dla magazynu kluczy<br>Ustawianie tagów dla magazynu kluczy |Kontrola dostępu oparta na rolach (RBAC) przy użyciu usługi Azure Resource Manager |
| Płaszczyzna danych |**Cały świat:**<br> &lt;nazwa_magazynu&gt;.vault.azure.net:443<br><br> **Chińska wersja platformy Azure:**<br> &lt;nazwa_magazynu&gt;.vault.azure.cn:443<br><br> **Wersja platformy Azure dla administracji USA:**<br> &lt;nazwa_magazynu&gt;.vault.usgovcloudapi.net:443<br><br> **Niemiecka wersja platformy Azure:**<br> &lt;nazwa_magazynu&gt;.vault.microsoftazure.de:443 |Dla kluczy: Odszyfruj, Szyfruj, Opakuj klucz, Odpakuj klucz, Weryfikuj, Podpisz, Pobierz, Lista, Aktualizuj, Utwórz, Importuj, Usuń, Kopia zapasowa, Przywróć<br><br> Dla wpisów tajnych: Pobierz, Lista, Ustaw, Usuń |Zasady dostępu magazynu kluczy |

Hello zarządzania płaszczyzny i dane płaszczyzny kontroli dostępu działają niezależnie. Na przykład jeśli chcesz toogrant kluczy toouse dostępu do aplikacji w magazynie kluczy, wystarczy toogrant płaszczyzny uprawnień dostępu do danych za pomocą zasad dostępu do magazynu kluczy i brak zarządzania płaszczyzny dostępu jest niezbędna do tej aplikacji. I odwrotnie, jeśli chcesz toobe użytkownika może tooread magazynu właściwości i tagi, ale nie ma żadnych tookeys dostępu, kluczy tajnych ani certyfikatów, można udzielić temu użytkownikowi, "read" dostęp przy użyciu RBAC i nie płaszczyzny toodata dostępu jest wymagany.

## <a name="management-plane-access-control"></a>Kontrola dostępu do płaszczyzny zarządzania
płaszczyzny zarządzania Hello składa się z operacji, które mają wpływ na magazyn kluczy hello sam. Można na przykład utworzyć lub usunąć magazyn kluczy, a także pobrać listę magazynów w subskrypcji. Można pobrać właściwości magazynu kluczy (takich jak jednostki SKU tagów) i ustawić zasady dostępu, określające hello użytkownicy i aplikacje, które mogą uzyskiwać dostęp do kluczy i kluczy tajnych w magazynie kluczy hello magazynu kluczy. Kontrola dostępu do płaszczyzny zarządzania korzysta z funkcji RBAC. Zobacz pełną listę hello operacje magazynu kluczy, które mogą być wykonywane za pośrednictwem zarządzania płaszczyzny w tabeli hello w powyższej sekcji. 

### <a name="role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach (RBAC)
Każda subskrypcja platformy Azure zawiera usługę Azure Active Directory. Zasoby toomanage dostępu w hello subskrypcji platformy Azure, które używają modelu wdrażania usługi Azure Resource Manager hello można udzielić użytkowników, grup i aplikacji z tego katalogu. Ten typ kontroli dostępu jest określony tooas kontroli dostępu opartej na rolach (RBAC). toomanage tego dostępu, można użyć hello [portalu Azure](https://portal.azure.com/), hello [narzędzia wiersza polecenia platformy Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), lub hello [Azure Resource Manager REST API](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Model usługi Azure Resource Manager hello tworzenia magazynu kluczy zasobów grupy i kontroli dostępu toohello zarządzania płaszczyźnie tego klucza magazynu przy użyciu usługi Azure Active Directory. Można na przykład przyznać użytkowników lub grupy możliwości toomanage magazynów kluczy w określonej grupy zasobów.

Przypisując odpowiednie role RBAC można udzielić dostępu toousers, grup i aplikacji w określonym zakresie. Na przykład toogrant dostępu tooa użytkownika toomanage magazynów kluczy wstępnie zdefiniowanej roli "magazyn kluczy współautora" przypisywanej toothis użytkownika w określonym zakresie. zakres Hello w takim przypadku będzie subskrypcji, grupy zasobów lub tylko określonego magazynu kluczy. Rola przypisana na poziomie subskrypcji stosuje tooall grup zasobów i zasobów w ramach danej subskrypcji. Rola przypisana na poziomie grupy zasobów ma zastosowanie tooall zasobów w danej grupie zasobów. Rola przypisana do określonego zasobu ma zastosowanie tylko toothat zasobów. Istnieje kilka wstępnie zdefiniowanych ról (zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md)), lub jeśli hello wstępnie zdefiniowanych ról nie odpowiadają potrzebom, możesz również definiować własne role.

> [!IMPORTANT]
> Należy pamiętać, że jeśli użytkownik ma współautora uprawnienia (RBAC) tooa magazynu kluczy zarządzania płaszczyzny, klika można przyznać sobie płaszczyźnie toodata dostępu, przez ustawienie zasad dostępu do magazynu kluczy, który kontroluje dostęp toodata płaszczyzny. W związku z tym zaleca tootightly kontrolować, kto może "Współautora" dostępu tooyour magazynów kluczy tooensure tylko autoryzowane osoby mogą dostępu i zarządzanie magazynów kluczy, kluczy, kluczy tajnych i certyfikatów.
> 
> 

## <a name="data-plane-access-control"></a>Kontrola dostępu do płaszczyzny danych
płaszczyzna danych magazynu kluczy Hello składa się z operacji, które wpływają na obiekty hello w magazynie kluczy, takie jak klucze, kluczy tajnych i certyfikatów.  Obejmuje to operacje dotyczące kluczy, takie jak tworzenie, importowanie, aktualizowanie, wyświetlanie, wykonywanie kopii zapasowych i przywracanie kluczy, operacje kryptograficzne, takie jak podpisywanie, weryfikowanie, szyfrowanie, odszyfrowywanie, kodowanie i odkodowywanie, oraz ustawianie tagów i innych atrybutów kluczy. W przypadku wpisów tajnych obejmuje operacje pobierania, ustawiania, wyświetlania i usuwania.

Dostęp do płaszczyzny danych jest udzielany przez ustawienie zasad dostępu magazynu kluczy. Użytkownik, grupy lub aplikacja musi mieć uprawnienia współautora (RBAC) dla płaszczyzny zarządzania dla magazynu kluczy toobe stanie tooset na zasady dostępu do tego magazynu kluczy. Użytkownika, grupy lub aplikacji można otrzymać dostęp do określonych operacji tooperform kluczy lub kluczy tajnych w magazynie kluczy. Obsługa magazynu kluczy się too16 wpisów zasad dostępu do magazynu kluczy. Tworzenie grupy zabezpieczeń usługi Azure Active Directory i dodawanie użytkowników toothat grupy toogrant danych płaszczyzny dostępu tooseveral użytkowników tooa magazynu kluczy.

### <a name="key-vault-access-policies"></a>Zasady dostępu magazynu kluczy
Zasady dostępu do magazynu kluczy przyznać oddzielnie tookeys uprawnienia i klucze tajne certyfikatów. Na przykład można podać tooonly klucze dostępu użytkownika, ale brak uprawnień dla kluczy tajnych. Jednak uprawnienia tooaccess kluczy lub kluczy tajnych lub certyfikaty są na poziomie magazynu hello. Innymi słowy, zasady dostępu magazynu kluczy nie obsługują uprawnień na poziomie obiektu. Można użyć [portalu Azure](https://portal.azure.com/), hello [narzędzia wiersza polecenia platformy Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), lub hello [magazynu kluczy interfejsów API REST zarządzania](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset zasad dostępu dla magazynu kluczy.

> [!IMPORTANT]
> Należy pamiętać, stosowanie zasad dostępu do klucza magazynu na poziomie magazynu hello. Na przykład gdy użytkownik uzyskuje uprawnienia toocreate i usuwania kluczy, będzie mogła wykonywać te operacje na wszystkie klucze w tym magazynie kluczy.
> 
> 

## <a name="example"></a>Przykład
Załóżmy, że tworzona jest aplikacja, która używa certyfikatu dla protokołu SSL, usługi Azure Storage do przechowywania danych oraz klucza RSA o długości 2048 bitów dla operacji podpisywania. Załóżmy, że ta aplikacja działa na maszynie wirtualnej (lub w zestawie skalowania maszyny wirtualnej). Możesz użyć toostore magazynu kluczy, hello wszystkich kluczy tajnych w aplikacji i Użyj magazynu kluczy toostore hello ładowania początkowego certyfikatu, który jest używany przez tooauthenticate aplikacji hello w usłudze Azure Active Directory.

Tak w tym miejscu jest podsumowanie wszystkich hello kluczy i kluczy tajnych toobe przechowywane w magazynie kluczy.

* **Certyfikat SSL** — używany do obsługi protokołu SSL
* **Klucz magazynu** -tooget dostępu tooStorage konta
* **2048-bitowy klucz RSA** — używany dla operacji podpisywania
* **Ładowania początkowego certyfikatu** -używany do podpisywania tooAzure tooauthenticate usługi Active Directory, klucza magazynu hello toofetch magazynu tooget dostępu tookey i Użyj klucza RSA hello.

Teraz załóżmy spełnia osoby hello zarządzanie, wdrażanie i inspekcję tej aplikacji. W tym przykładzie użyjemy trzech ról.

* **Zespół zabezpieczeń** — są to zazwyczaj personelu IT z hello "urząd hello CSO (Chief Security Officer)" lub równoważne, odpowiedzialny za hello właściwe przechowywanie kluczy tajnych takich jak certyfikaty SSL, używany do podpisywania, parametry połączenia dla kluczy RSA bazy danych, klucze konta magazynu.
* **Deweloperzy/operatory** — są to hello pracowników, którzy opracowanie tej aplikacji, a następnie wdrożyć go na platformie Azure. Zazwyczaj nie są częścią zespołu zabezpieczeń hello i dlatego nie powinny mieć dostępu tooany poufnych danych, takich jak certyfikaty SSL, kluczy RSA, ale aplikacja hello wdrażaniu przez nich powinien mieć toothose dostępu.
* **Audytorzy** — zazwyczaj jest to inny zestaw osób odizolowanych od hello deweloperzy i pracownicy działu IT ogólne. Odpowiedzialność jest tooreview prawidłowego użycia i obsługi certyfikatów, kluczy itp. i zapewnienia zgodności ze standardami zabezpieczeń danych. 

Co więcej rola, która jest poza zakresem hello tej aplikacji, ale odpowiednie toobe tutaj wymienionych i będzie hello subskrypcji (lub grupy zasobów) jest administratorem. Administratorem subskrypcji ustawia uprawnienia dostępu początkowej hello zespołu pracowników ochrony obiektu. W tym miejscu przyjęto założenie, że administrator subskrypcji hello udzielono dostępu toohello zabezpieczeń zespołu tooa grupy zasobów w którym wszystkie hello zasobów niezbędnych do tej aplikacji reside okresu.

Teraz zobaczmy, jakie akcje wykonuje każdej roli w kontekście hello tej aplikacji.

* **Zespół ds. zabezpieczeń**
  * Tworzenie magazynów kluczy
  * Włączenie funkcji rejestrowania magazynu kluczy
  * Dodawanie kluczy/wpisów tajnych
  * Tworzenie kopii zapasowych kluczy na potrzeby odzyskiwania po awarii
  * Operacje na zestawie uzyskiwania dostępu do klucza magazynu zasad toogrant uprawnienia toousers i aplikacje tooperform określonych
  * Okresowe wycofywanie (ponowne tworzenie) kluczy/wpisów tajnych
* **Deweloperzy/operatorzy**
  * Pobierz toobootstrap odwołań i certyfikatami SSL (odciski palców), klucz magazynu (klucz tajny identyfikatora URI) i podpisywanie klucza (identyfikator URI klucza) od zespołu zabezpieczeń
  * Opracowywanie i wdrażanie aplikacji, która programowo uzyskuje dostęp do kluczy i wpisów tajnych
* **Audytorzy**
  * Użycie Przejrzyj dzienniki tooconfirm prawidłowego użycia klucza/klucz tajny i zgodność ze standardami zabezpieczeń danych

Teraz zobaczmy, jakie magazynu tookey uprawnienia dostępu są wymagane przez wszystkie role (i aplikacji hello) tooperform przydzielone zadania. 

| Rola użytkownika | Uprawnienia do płaszczyzny zarządzania | Uprawnienia do płaszczyzny danych |
| --- | --- | --- |
| Zespół ds. zabezpieczeń |Współautor magazynu kluczy |Klucze: wykonywanie kopii zapasowej, tworzenie, usuwanie, pobieranie, importowanie, wyświetlanie, przywracanie <br> Wpisy tajne: wszystkie |
| Deweloperzy/operatorzy |magazyn kluczy wdrożyć uprawnienia tak, aby maszyny wirtualne hello wdrażaniu przez nich można pobrać kluczy tajnych z hello magazynu kluczy |Brak |
| Audytorzy |None |Klucze: wyświetlanie<br>Wpisy tajne: wyświetlanie |
| Aplikacja |None |Klucze: podpisywanie<br>Wpisy tajne: pobieranie |

> [!NOTE]
> Audytorów muszą listy uprawnień dla kluczy i kluczy tajnych, więc kontrolują atrybuty klucze i klucze tajne, które nie są emitowane w dziennikach hello, takich jak tagi, dat aktywacji i ważności.
> 
> 

Oprócz magazynu tookey uprawnień wszystkie trzy role również muszą uzyskać dostęp do tooother zasobów. Na przykład toobe stanie toodeploy maszyn wirtualnych (lub sieci Web Apps itp.) Deweloperzy/operatory muszą również typy zasobów toothose dostępu "Współautora". Audytorów wymagają konta magazynu toohello dostęp do odczytu przechowywania hello dzienniki magazynu kluczy.

Ponieważ hello fokus w tym artykule jest zabezpieczenie magazynu kluczy dostępu tooyour, możemy tylko ilustrują hello odpowiednich części dotyczące toothis tematu i Pomiń szczegóły dotyczące wdrażanie certyfikatów, uzyskiwania dostępu do kluczy i kluczy tajnych programowo itp. Te szczegóły zostały już omówione w innym miejscu. Wdrażanie certyfikatów przechowywanych w magazynie kluczy tooVMs jest objęte [wpis w blogu](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)i ma [przykładowy kod](https://www.microsoft.com/download/details.aspx?id=45343) dostępne który ilustruje sposób toouse ładowania początkowego certyfikatu tooauthenticate tooget tooAzure AD Magazyn tookey dostępu.

Większość hello uprawnienia można przyznać przy użyciu portalu Azure, ale szczegółowe uprawnienia toogrant hello tooachieve toouse programu Azure PowerShell (lub wiersza polecenia platformy Azure) może być konieczne żądanego wyniku. 

Przykładowa powitania po wstawki kodu programu PowerShell:

* administrator usługi Azure Active Directory Hello utworzył grup zabezpieczeń, które reprezentują hello trzech ról, to znaczy zespołu zabezpieczeń firmy Contoso, metodyki Devops aplikacji Contoso, audytorów aplikacji Contoso. Hello administrator dodano również grup toohello użytkowników.
* **ContosoAppRG** jest hello grupa zasobów, w którym znajdują się wszystkie zasoby hello. **contosologstorage** jest, gdzie są przechowywane dzienniki hello. 
* Magazyn kluczy **ContosoKeyVault** i konto magazynu dla dzienników magazynu kluczy **contosologstorage** musi być w hello tej samej lokalizacji platformy Azure

Pierwszym administratorem subskrypcji hello przypisuje "klucza magazynu współautora" i zespołu zabezpieczeń toohello ról użytkownika administratora dostępu. Umożliwia hello zabezpieczeń zespołu toomanage dostęp do tooother zasobów i zarządzanie magazynów kluczy w grupie zasobów hello ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Witaj poniższy skrypt ilustruje sposób hello zabezpieczeń zespołu można utworzyć magazyn kluczy, Konfiguracja rejestrowania i ustaw uprawnienia dostępu dla innych ról i aplikacji hello. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

Rola niestandardowa Hello zdefiniowane, jest tylko subskrypcji można przypisać toohello, w którym zostanie utworzona grupa zasobów ContosoAppRG hello. Jeśli hello niestandardowych ról będzie służyć do innych projektów w inne subskrypcje, jej zakres może mieć więcej subskrypcji dodane.

Przypisanie roli niestandardowych Hello dla deweloperów hello/operatory uprawnienia "Wdrażanie/action" hello jest zakresem toohello grupy zasobów. W ten sposób tylko hello maszyny wirtualne utworzone w grupie zasobów Witaj, "ContosoAppRG" zostanie wyświetlony hello hasła (certyfikat SSL i certyfikatów bootstrap). Wszystkie maszyny wirtualne, które jest członkiem zespołu deweloperów/ops tworzy się w innej grupie zasobów nie będą mogli tooget tych kluczy tajnych nawet wtedy, gdy znał hello klucz tajny identyfikatorów URI.

W tym przykładzie przedstawiono prosty scenariusz. Rzeczywistych scenariuszach może być bardziej złożone i konieczne może być tooadjust uprawnienia tooyour magazynu kluczy na podstawie Twoich potrzeb. Na przykład w tym przykładzie przyjęto założenie, że tego zespołu zabezpieczeń można znaleźć klucza hello i tajne odwołań (identyfikatory URI i odciski palców) tego tooreference potrzeba zespołu deweloperów/operatory w swoich aplikacjach. W związku z tym nie potrzebują toogrant deweloperzy/operatory dostępu do żadnych danych płaszczyzny. Należy również zauważyć, że ten przykład koncentruje się na zabezpieczaniu magazynu kluczy. Należy zwrócić szczególną uwagę podobne toosecure [maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machines/security/), [kont magazynu](../storage/common/storage-security-guide.md) i innych zasobów platformy Azure za.

> [!NOTE]
> Uwaga: W tym przykładzie pokazano, jak dostęp do magazynu kluczy będzie zabezpieczany (blokowany) w środowisku produkcyjnym. Deweloperzy Hello powinna mieć własne subskrypcji lub grupa zasobów gdzie mają pełne uprawnienia toomanage ich magazynów, maszyn wirtualnych i konto magazynu gdzie opracowywania aplikacji hello.
> 
> 

## <a name="resources"></a>Zasoby
* [Kontrola dostępu oparta na rolach w usłudze Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  W tym artykule opisano hello kontroli dostępu opartej na roli Azure Active Directory i jej działania.
* [Kontrola dostępu oparta na rolach (RBAC): wbudowane role](../active-directory/role-based-access-built-in-roles.md)
  
  Ten artykuł szczegóły wszystkich hello wbudowane Role dostępne w RBAC.
* [Omówienie wdrażania przy użyciu usługi Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md)
  
  W tym artykule opisano hello wdrożenie usługi Resource Manager i klasycznych modeli wdrażania i opisano hello zalety korzystania z grup hello Resource Manager i zasobów
* [Zarządzanie kontrolą dostępu opartą na rolach za pomocą programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  W tym artykule opisano, jak kontrola przy użyciu programu Azure PowerShell dostępu toomanage opartej na rolach
* [Zarządzanie oparte na rolach kontrola dostępu przy użyciu hello interfejsu API REST](../active-directory/role-based-access-control-manage-access-rest.md)
  
  W tym artykule opisano, jak toouse hello toomanage interfejsu API REST RBAC.
* [Kontrola dostępu oparta na rolach dla platformy Microsoft Azure — konferencja Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  To jest łącze tooa wideo w witrynie Channel 9 z konferencji Ignite 2015 MS hello. W tej sesji porozmawiać o dostęp do zarządzania i możliwości raportowania w programie Azure i eksplorowanie najlepsze rozwiązania dotyczące zabezpieczania dostępu tooAzure subskrypcji przy użyciu usługi Azure Active Directory.
* [Autoryzowanie dostępu tooweb aplikacji przy użyciu protokołu OAuth 2.0 i usługi Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  W tym artykule opisano kompletny przepływ protokołu OAuth 2.0 używany do uwierzytelniania za pomocą usługi Azure Active Directory.
* [Interfejsy API REST zarządzania magazynem kluczy](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Ten dokument jest odwołanie hello toomanage interfejsów API REST hello klucz magazynu programowo, włączając ustawienie zasad dostępu do magazynu kluczy.
* [Interfejsy API REST magazynu kluczy](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Magazyn tookey łącze dokumentacji interfejsu API REST.
* [Kontrola dostępu do kluczy](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Łącze tooSecret dostępu kontroli dokumentacji.
* [Kontrola dostępu do kluczy tajnych](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Łącze tooKey dostępu kontroli dokumentacji.
* [Ustawianie](https://msdn.microsoft.com/library/mt603625.aspx) i [usuwanie](https://msdn.microsoft.com/library/mt619427.aspx) zasad dostępu magazynu kluczy przy użyciu programu PowerShell
  
  Dokumentacja tooreference łącza dla zasad dostępu magazynu kluczy toomanage poleceń cmdlet programu PowerShell.

## <a name="next-steps"></a>Następne kroki
Aby zapoznać się z samouczkiem wprowadzającym dla administratora, zobacz [Wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).

Aby uzyskać więcej informacji na temat rejestrowania użycia usługi Key Vault, zobacz [Funkcja rejestrowania usługi Azure Key Vault](key-vault-logging.md).

Aby uzyskać więcej informacji na temat używania kluczy i wpisów tajnych w usłudze Azure Key Vault, zobacz [Informacje o kluczach i wpisach tajnych](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Jeśli masz pytania dotyczące magazynu kluczy, odwiedź stronę hello [usługi Azure key vault fora](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

