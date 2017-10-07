---
title: "Samouczek: Konfigurowanie produktu Workday dla użytkownika automatycznego inicjowania obsługi administracyjnej z lokalnej usługi Active Directory i Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse produktu Workday jako źródło danych tożsamości dla usługi Active Directory i Azure Active Directory."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Samouczek: Konfigurowanie produktu Workday dla użytkownika automatycznego inicjowania obsługi administracyjnej z lokalnej usługi Active Directory i Azure Active Directory
Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform tooimport osób z produktu Workday do usługi Active Directory i Azure Active Directory, z opcjonalne zapisywanie zwrotne tooWorkday niektóre atrybuty. 



## <a name="overview"></a>Omówienie

Witaj [użytkownika usługi Azure Active Directory świadczenie usługi](active-directory-saas-app-provisioning.md) integruje się z hello [API kadr produktu Workday](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) w celu tooprovision kont użytkowników. Usługi Azure AD używa tego hello tooenable połączenia po inicjowania obsługi administracyjnej przepływy pracy użytkownika:

* **Inicjowanie obsługi użytkowników tooActive katalogu** -synchronizowanie wybranego zestawu użytkowników z produktu Workday w co najmniej jeden lasów usługi Active Directory. 

* **Inicjowanie obsługi administracyjnej tooAzure tylko w chmurze użytkowników usługi Active Directory** -hybrydowego użytkowników, którzy istnieje w usłudze Active Directory i Azure Active Directory można udostępnić w ostatnim przy użyciu hello [AAD Connect](connect/active-directory-aadconnect.md). Jednak użytkownicy, którzy są tylko w chmurze można alokować bezpośrednio z produktu Workday za pomocą usługi Active Directory tooAzure hello świadczenie usługi użytkownika usługi Azure AD.

* **Zapisywanie zwrotne e-mail adresy tooWorkday** -hello Azure AD użytkownika usługi inicjowania obsługi administracyjnej może zapisywać wybrane usługi Azure AD użytkownika atrybuty wstecz tooWorkday, takie jak adres e-mail hello.

### <a name="scenarios-covered"></a>Omówione scenariusze

Użytkownik produktu Workday Hello inicjowania obsługi przepływów pracy obsługiwanych przez użytkownika usługi Azure AD hello świadczenie usługi umożliwia automatyzację hello następujące scenariusze zarządzania cyklem życia zasobów ludzkich i tożsamości:

* **Nowi pracownicy wynajem** — po dodaniu nowych pracowników tooWorkday, konto użytkownika zostanie automatycznie utworzone w usłudze Active Directory, usługi Azure Active Directory i opcjonalnie usługi Office 365 i [innych aplikacji SaaS obsługiwane przez usługę Azure AD ](active-directory-saas-app-provisioning.md), zapisu obu tooWorkday adres e-mail hello.

* **Aktualizacje atrybutu i profilu pracownika** — po rekordu pracownika jest aktualizowany w pracy (takie jak ich nazwy, tytuł lub manager), ich konta użytkownika zostanie automatycznie zaktualizowana w usłudze Active Directory, usługi Azure Active Directory i opcjonalnie usługi Office 365 i [innych aplikacji SaaS obsługiwane przez usługę Azure AD](active-directory-saas-app-provisioning.md).

* **Liczba przerwanych pracownika** — gdy pracownik zostaje zakończone w pracy, ich konta użytkownika jest automatycznie wyłączana w usłudze Active Directory, usługi Azure Active Directory i opcjonalnie usługi Office 365 i [innych aplikacji SaaS obsługiwane przez usługę Azure AD](active-directory-saas-app-provisioning.md).

* **Pracownik ponownie wynajmuje** — gdy pracownik jest rehired w pracy, ich stare konto można automatycznie ponownie uaktywnić lub ponownie elastycznie (w zależności od swoich preferencji) tooActive katalogu, Azure Active Directory i opcjonalnie usługi Office 365 i [innych aplikacji SaaS obsługiwane przez usługę Azure AD](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Planowanie rozwiązania

Przed rozpoczęciem integracji z produktem Workday, sprawdź hello wymagania wstępne, poniżej i odczytu hello następujące instrukcje toomatch Twojej bieżącej architektury usługi Active Directory i przypisywania wymagania z użytkowników hello solution(s) udostępniane przez usługi Azure Active Katalog.

### <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Prawidłową subskrypcję z uprawnieniami administratora globalnego usługi Azure AD Premium P1
* Dzierżawca implementacji produktu Workday do celów testowania i integracji
* Uprawnienia administratora w toocreate produktu Workday użytkownika integracji systemu i zmiany tootest pracownika dane do celów testowych
* Dla użytkownika inicjowania obsługi administracyjnej tooActive katalogu przyłączonych do domeny serwera z systemem usługi systemu Windows 2012 lub nowszego jest wymagany toohost hello [agent synchronizacji lokalnej](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) synchronizacji od usługi Active Directory i Azure AD

> [!NOTE]
> Jeśli znajduje się w Europie dzierżawy usługi Azure AD, zobacz hello [znane problemy](#known-issues) poniższej sekcji.


### <a name="solution-architecture"></a>Architektura rozwiązania

Usługa Azure AD zapewnia bogaty zestaw inicjowania obsługi administracyjnej toohelp łączników, które rozwiązywać zarządzania cyklem życia inicjowania obsługi i tożsamości z produktu Workday tooActive katalogu usługi Azure AD, aplikacji SaaS i późniejsze. Funkcje użytkownik użyje i sposób konfigurowania rozwiązania hello będą się różnić w zależności od środowiska i wymagań Twojej organizacji. Pierwszym krokiem wykonać zapasów, o ile następującego hello są obecne i wdrożony w organizacji:

* Ile lasy usługi Active Directory są używane?
* Jak wiele domen usługi Active Directory są używane?
* Ile Active Directory jednostek organizacyjnych (OU) są używane?
* Jak wiele dzierżaw usługi Azure Active Directory są używane?
* Czy istnieją użytkowników, którzy potrzebują tooboth toobe udostępniane usługi Active Directory i Azure Active Directory (np. "hybrydowe" użytkowników)?
* Czy istnieją użytkowników, którzy potrzebują tooAzure toobe udostępniane usługi Active Directory, ale nie Active Directory (np. "tylko w chmurze" użytkowników)?
* Czy adresu e-mail użytkownika muszą toobe zapisywane tooWorkday?

Po utworzeniu toothese odpowiedzi na pytania, możesz zaplanować pracy inicjowania obsługi wdrożenia według poniższych wskazówek hello poniżej.

#### <a name="using-provisioning-connector-apps"></a>Za pomocą aplikacji łącznika inicjowania obsługi administracyjnej

Azure Active Directory obsługuje wstępnie zintegrowanych łączników inicjowania obsługi administracyjnej dla produktu Workday i wiele innych aplikacji SaaS. 

Pojedynczy łącznik inicjowania obsługi administracyjnej interfejsy z hello interfejsu API systemu jednego źródła i pomaga udostępniania danych tooa pojedynczym elementem docelowym systemu. Większość inicjowania obsługi administracyjnej łączniki, które obsługuje usługę Azure AD dla jednego źródła i systemu docelowego (np. tooServiceNow usługi Azure AD) i można skonfigurować przez dodanie aplikacji hello zagrożona z galerii aplikacji Azure AD hello (np. usługi ServiceNow). 

Jest relacją między inicjowania obsługi administracyjnej wystąpienia łącznika i wystąpień aplikacji w usłudze Azure AD:

| Systemu źródłowego | System docelowy |
| ---------- | ---------- | 
| Dzierżawy usługi Azure AD | Aplikacja SaaS |


Podczas pracy z produktu Workday i usługi Active Directory, istnieją jednak wiele źródłowa i docelowa toobe systemów uznawane za:

| Systemu źródłowego | System docelowy | Uwagi |
| ---------- | ---------- | ---------- |
| Dzień roboczy | Lasu usługi Active Directory | Każdy las jest traktowany jako system docelowy różne |
| Dzień roboczy | Dzierżawy usługi Azure AD | Co jest wymagane dla użytkowników tylko w chmurze |
| Lasu usługi Active Directory | Dzierżawy usługi Azure AD | Ten przepływ jest obecnie obsługiwany przez AAD Connect |
| Dzierżawy usługi Azure AD | Dzień roboczy | Dla zapisu zwrotnego adresów e-mail |

toofacilitate te wiele przepływów pracy toomultiple źródłowe i docelowe systemy, usługi Azure AD zapewnia wielu inicjowania obsługi administracyjnej aplikacji łącznika, które można dodać z galerii aplikacji hello Azure AD:

![Galerii aplikacji usługi AAD](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **WORKDAY tooActive udostępniania katalogu** -ta aplikacja umożliwia przypisywanie konta użytkowników z produktu Workday tooa jednego lasu usługi Active Directory. Jeśli masz wiele lasów, można dodać z galerii aplikacji hello Azure AD dla każdego lasu usługi Active Directory, należy tooprovision do jedno wystąpienie tej aplikacji.

* **WORKDAY tooAzure AD inicjowania obsługi administracyjnej** -podczas AAD Connect to narzędzie hello, który powinien być tooAzure użytkowników usługi Active Directory używanych toosynchronize usługi Active Directory, ta aplikacja może być używane toofacilitate inicjowania obsługi administracyjnej tylko na chmurze użytkowników z produktu Workday tooa pojedynczego Dzierżawy usługi Azure Active Directory.

* **Zapisywanie zwrotne WORKDAY** -ta aplikacja umożliwia zapisywanie zwrotne adresu e-mail użytkownika z tooWorkday usługi Azure Active Directory.

> [!TIP]
> regularne aplikacji "Produktu Workday" Hello jest używany do konfigurowania rejestracji jednokrotnej między produktu Workday i Azure Active Directory. 

Jak tooset Konfigurowanie i konfiguruje je specjalne inicjowania obsługi administracyjnej łącznika aplikacji jest przedmiotem hello hello pozostałej części tego samouczka. Aplikacje, które możesz wybrać tooconfigure będzie zależeć na systemach, w których należy tooprovision, ile lasy usługi Active Directory i Azure AD to dzierżawców w danym środowisku.

![Omówienie](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Skonfiguruj użytkownika integracji systemu w pracy
Typowe wymagania wszystkich łączników inicjowania obsługi administracyjnej produktu Workday hello jest wymagają podania poświadczeń dla produktu Workday systemu integracji konta tooconnect toohello produktu Workday API zasobów ludzkich. W tej sekcji opisano, jak konto toocreate integrator systemu produktu Workday.

> [!NOTE]
> Jest możliwe toobypass tej procedury i zamiast tego użyć konta administratora globalnego produktu Workday jako konta integracji systemu hello. Może działać prawidłowo w przypadku pokazów, ale nie jest zalecane w przypadku wdrożeń produkcyjnych.

### <a name="create-an-integration-system-user"></a>Utwórz użytkownika integracji systemu

**toocreate integracji systemu użytkownika:**

1. Zaloguj się do konta administratora dzierżawy produktu Workday. W hello **Workbench produktu Workday**, wprowadź użytkownika w polu wyszukiwania hello, a następnie kliknij polecenie **Tworzenie użytkownika System integracji**. 
   
    ![Utwórz użytkownika](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "tworzenia użytkownika")
2. Zakończenie hello **Tworzenie użytkownika System integracji** zadanie, podając nazwę użytkownika i hasło dla nowego użytkownika System integracji.  
 * Pozostaw hello **wymagają nowe hasło przy następnej znak** opcja nie jest zaznaczona, ponieważ ten użytkownik będzie logować się programowo. 
 * Pozostaw hello **minut limitu czasu sesji** z jego wartość domyślna 0, która uniemożliwi sesje użytkowników hello przedwcześnie limit czasu. 
   
    ![Utwórz użytkownika System integracji](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "utworzyć integracji systemu użytkownika")

### <a name="create-a-security-group"></a>Utwórz grupę zabezpieczeń
Należy toocreate grupa zabezpieczeń systemu nieograniczonego integracji i przypisać hello tooit użytkownika.

**toocreate grupy zabezpieczeń:**

1. Wprowadź Utwórz grupę zabezpieczeń w polu wyszukiwania hello, a następnie kliknij przycisk **Utwórz grupę zabezpieczeń**. 
   
    ![Grupa CreateSecurity](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity grupy")
2. Zakończenie hello **Utwórz grupę zabezpieczeń** zadań.  
3. Wybierz grupy zabezpieczeń systemu integracji — nieograniczonego z hello **typ grupy zabezpieczeń dzierżawcza** listy rozwijanej.
4. Utwórz toowhich grupy zabezpieczeń, zostaną jawnie dodane elementy członkowskie. 
   
    ![Grupa CreateSecurity](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity grupy")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Przypisz grupę zabezpieczeń toohello użytkownika hello integracji systemu

**Użytkownik systemu tooassign hello integracji:**

1. Wprowadź w polu wyszukiwania hello Edytuj grupę zabezpieczeń, a następnie kliknij przycisk **Edytuj grupę zabezpieczeń**. 
   
    ![Edytuj grupę zabezpieczeń](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edytuj grupę zabezpieczeń")
2. Wyszukaj i wybierz nową grupę zabezpieczeń integracji hello według nazwy. 
   
    ![Edytuj grupę zabezpieczeń](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edytuj grupę zabezpieczeń")
3. Dodaj hello nowe integracji systemu użytkownika toohello nową grupę zabezpieczeń. 
   
    ![Grupa zabezpieczeń systemu](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "grupa zabezpieczeń systemu")  

### <a name="configure-security-group-options"></a>Skonfiguruj opcje grupy zabezpieczeń
W tym kroku przyznane toohello nowych zabezpieczeń uprawnienia grupy do **uzyskać** i **Put** operacje na obiektach hello zabezpieczone przez hello następujące zasady zabezpieczeń domeny:

* Inicjowanie obsługi konta zewnętrznego
* Danych procesu roboczego: Raporty publicznego procesu roboczego
* Danych procesu roboczego: Wszystkie pozycje
* Danych procesu roboczego: Personel informacje o bieżącej
* Danych procesu roboczego: Tytuł firm proces roboczy w profilu

**tooconfigure opcje grupy zabezpieczeń:**

1. Wprowadź w polu wyszukiwania hello zasady zabezpieczeń domeny, a następnie kliknij łącze hello **zasady zabezpieczeń domeny dla Obszar funkcjonalny**.  
   
    ![Zasady zabezpieczeń domeny](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "zasady zabezpieczeń domeny")  
2. Wyszukaj systemu i wybierz hello **systemu** Obszar funkcjonalny.  Kliknij przycisk **OK**.  
   
    ![Zasady zabezpieczeń domeny](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "zasady zabezpieczeń domeny")  
3. Na liście hello zasad zabezpieczeń dla hello Obszar funkcjonalny systemu, rozwiń węzeł **administrowania zabezpieczeniami** i wybierz zasady zabezpieczeń domeny hello **zewnętrznych Inicjowanie obsługi konta**.  
   
    ![Zasady zabezpieczeń domeny](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "zasady zabezpieczeń domeny")  
4. Kliknij przycisk **Edytuj uprawnienia**, a następnie na powitania **Edytuj uprawnienia**okno dialogowe Dodaj hello nową zabezpieczeń grupy toohello listę grup zabezpieczeń z **uzyskać** i **Put** uprawnienia integracji. 
   
    ![Edytuj uprawnienia](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "uprawnienia do edycji")  
5. Powtórz krok 1 powyżej tooreturn toohello ekran wybierania obszarów funkcjonalnych, a teraz, wyszukaj personel, wybierz hello **personel Obszar funkcjonalny** i kliknij przycisk **OK**.
   
    ![Zasady zabezpieczeń domeny](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "zasady zabezpieczeń domeny")  
6. Listy hello zasad zabezpieczeń dla hello Staffing Obszar funkcjonalny, rozwiń węzeł **danych procesu roboczego: Staffing** i powtórz kroki 4 powyżej dla każdej z tych pozostałych zasady zabezpieczeń:

   * Danych procesu roboczego: Raporty publicznego procesu roboczego
   * Danych procesu roboczego: Wszystkie pozycje
   * Danych procesu roboczego: Personel informacje o bieżącej
   * Danych procesu roboczego: Tytuł firm proces roboczy w profilu
   
7. Powtórz kroki 1, powyżej tooreturn ekran toohello Wybieranie obszarów funkcjonalnych i tym razem wyszukiwać **informacje kontaktowe**, wybierz obszar funkcjonalny Staffing hello i kliknij przycisk **OK**.

8.  Listy hello zasad zabezpieczeń dla hello Staffing Obszar funkcjonalny, rozwiń węzeł **danych procesu roboczego: informacje kontaktowe pracy**i powtórz kroki 4 powyżej dla zasad zabezpieczeń hello poniżej:

    * Dane procesu roboczego: Służbowy adres E-mail

    ![Zasady zabezpieczeń domeny](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "zasady zabezpieczeń domeny")  
    
### <a name="activate-security-policy-changes"></a>Aktywuj zmian zasad zabezpieczeń

**tooactivate zmian zasad zabezpieczeń:**

1. Wprowadź aktywować w polu wyszukiwania hello, a następnie kliknij łącze hello **aktywować oczekujących zmian zasad zabezpieczeń**. 
   
    ![Aktywuj](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "aktywacji") 
2. Witaj BEGIN aktywować oczekujących zmian zasad zabezpieczeń zadań wprowadzić komentarz dla inspekcji, a następnie kliknij **OK**. 
   
    ![Aktywuj oczekujących zabezpieczeń](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "aktywować oczekujących zabezpieczeń")   
3. Zadania ukończone hello na następnym ekranie powitania zaznaczając pole wyboru hello **Potwierdź**, a następnie kliknij przycisk **OK**. 
   
    ![Aktywuj oczekujących zabezpieczeń](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "aktywować oczekujących zabezpieczeń")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Konfigurowanie Inicjowanie obsługi użytkowników z produktu Workday tooActive katalogu
Wykonaj te instrukcje konta użytkownika tooconfigure inicjowania obsługi administracyjnej z produktu Workday tooeach lasu usługi Active Directory, wymagających inicjowania obsługi administracyjnej.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Część 1: Dodawanie hello inicjowania obsługi administracyjnej łącznik aplikacji i tworzenie hello tooWorkday połączenia

**tooconfigure produktu Workday tooActive katalogu inicjowania obsługi administracyjnej:**

1.  Przejdź do zbyt<https://portal.azure.com>

2.  Na pasku nawigacyjnym po lewej stronie powitania, wybierz **usługi Azure Active Directory**

3.  Wybierz **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.

4.  Wybierz **dodać aplikację**i wybierz hello **wszystkie** kategorii.

5.  Wyszukaj **produktu Workday inicjowania obsługi administracyjnej tooActive katalogu**i Dodaj danej aplikacji hello galerii.

6.  Hello — po dodaniu aplikacji i jest wyświetlany ekran szczegółów aplikacji hello, wybierz **inicjowania obsługi administracyjnej**

7.  Zmień hello **inicjowania obsługi administracyjnej** **tryb** zbyt**automatyczne**

8.  Zakończenie hello **poświadczeń administratora** sekcji w następujący sposób:

   * **Nazwa użytkownika administratora** — wprowadź nazwę użytkownika hello z hello produktu Workday integracji konto system, nazwę domeny dzierżawy hello dołączane. **Powinien wyglądać mniej więcej tak:username@contoso4**

   * **Hasło administratora —** wprowadź hasło hello hello produktu Workday integracji systemu konta

   * **Adres URL — dzierżawy** Wprowadź końcowy usług sieci web produktu Workday toohello hello adres URL dzierżawy. To powinien wyglądać następująco: https://wd3-impl-services1.workday.com/ccx/service/contoso4, gdzie contoso4 jest zastępowany nazwa dzierżawy poprawne, a wd3 impl jest zastępowany hello poprawne środowisko ciągu.

   * **Lasu usługi Active Directory -** Witaj "Name" w lesie usługi Active Directory, zwracane przez polecenia powershell Get-ADForest hello. Zazwyczaj jest to ciąg, takich jak: *contoso.com*

   * **Kontener usługi Active Directory -** wprowadź ciąg hello kontenera, która zawiera wszystkich użytkowników w lesie usługi AD. Przykład: *OU = użytkowników standardowych, OU = użytkownicy, DC = contoso, DC = test*

   * **Wiadomość E-mail z powiadomieniem —** wprowadź swój adres e-mail, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail, jeśli wystąpi błąd".

   * Kliknij przycisk hello **Testuj połączenie** przycisku. Jeśli test połączenia hello zakończy się powodzeniem, kliknij przycisk hello **zapisać** przycisk u góry hello. W przypadku niepowodzenia dokładnie sprawdzić, czy poświadczenia dla produktu Workday hello są prawidłowe w pracy. 

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Część 2: Konfigurowanie mapowań atrybutów 

W tej sekcji skonfigurujesz, jak dane użytkownika wypływających z produktu Workday do usługi Active Directory.

1.  Na karcie Udostępnianie hello w obszarze **mapowania**, kliknij przycisk **tooOnPremises zsynchronizować pracowników z produktu Workday**.

2.  W hello **zakres obiektu źródłowego** pole, można wybrać, które zestawów użytkowników w pracy powinna być w zakresie obsługi tooAD, definiując zestaw opartych na atrybutach filtrów. zakres domyślnej Hello jest "wszyscy użytkownicy w pracy". Przykładowe filtry:

   * Przykład: Toousers zakres z identyfikatorami procesu roboczego między 1000000 i 2000000

      * Atrybut: WorkerID

      * Operator: Dopasowanie wyrażenia REGULARNEGO

      * Wartość: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Przykład: Tylko pracownicy i nie pracowników warunkowe 

      * Atrybut: identyfikator pracownika

      * Operator: Nie ma wartości NULL

3.  W hello **akcji obiektów docelowych** pole globalnie filtrowania, jakie akcje mogą toobe w usłudze Active Directory. **Utwórz** i **aktualizacji** są najczęściej.

4.  W hello **mapowania atrybutów** sekcji, można zdefiniować poszczególne produktu Workday atrybuty mapy tooActive atrybutów katalogu.

5. Kliknij na istniejących tooupdate mapowanie atrybutu lub **Dodaj nowe mapowanie** u dołu hello hello ekranu tooadd nowe mapowania. Mapowanie atrybutu poszczególnych obsługuje następujące właściwości:

      * **Typ mapowania**

         * **Bezpośrednie** — zapisuje hello wartość atrybutu hello produktu Workday atrybutu toohello AD, bez zmian

         * **Stała** -zapisać wartości ciągu statycznych, stałych do atrybutu hello AD

         * **Wyrażenie** — pozwala toowrite Niestandardowa wartość atrybutu hello AD, na podstawie co najmniej jeden dzień roboczy atrybutów. [Aby uzyskać więcej informacji, zobacz ten artykuł wyrażeń](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Atrybut źródłowy** -hello atrybut użytkownika z produktu Workday.

      * **Wartość domyślna** — jest to opcjonalne. Jeśli atrybut źródłowy hello ma wartość pustą, mapowanie hello zapisu wtedy tę wartość.
            Najbardziej typowe konfiguracje jest tooleave tym puste.

      * **Atrybut TARGET** — Witaj atrybut użytkownika w usłudze Active Directory.

      * **Zgodne obiektów przy użyciu tego atrybutu** — czy stosuje się to mapowanie toouniquely zidentyfikować użytkowników między produktu Workday i usługi Active Directory. Jest to zazwyczaj ustawiona w polu Identyfikator procesu roboczego dla produktu Workday, która zwykle jest mapowana na jeden z atrybutów identyfikator pracownika hello w usłudze Active Directory.

      * **Dopasowywanie pierwszeństwo** — wiele pasujących atrybuty można ustawić. Jeśli dostępnych jest wiele, są oceniane pod w kolejności wynika z tego pola. Jak dopasowania zostanie znaleziony, żadne dodatkowe dopasowania atrybuty są oceniane.

      * **Zastosuj to mapowanie**
       
         * **Zawsze** — Zastosuj to mapowanie na obu Tworzenie użytkownika i aktualizowanie akcji

         * **Tylko podczas tworzenia** -Zastosuj to mapowanie tylko akcje creation użytkownika

6. toosave mapowania, kliknij przycisk **zapisać** u góry hello sekcji atrybutu mapowania.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**Poniżej przedstawiono przykładowe Mapowanie atrybutów między produktu Workday i usługi Active Directory, z niektórych typowych wyrażeń**

-   wyrażenie Hello mapuje toohello parentDistinguishedName AD atrybut może być używane tooprovision tooa użytkownika, który określoną jednostkę Organizacyjną na podstawie co najmniej jeden dzień roboczy źródła atrybutów. W tym przykładzie umieszcza użytkowników w różnych jednostkach organizacyjnych w zależności od ich danych Miasto w pracy.

-   wyrażenie Hello Odwzorowuje atrybut userPrincipalName AD toohello utworzyć nazwę UPN firstName.LastName@contoso.com. Zastępuje ona niedozwolone znaki specjalne.

-   [Brak dokumentację dotyczącą tutaj wyrażeń.](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| ATRYBUT WORKDAY | ATRYBUT USŁUGI ACTIVE DIRECTORY |  ZGODNYM IDENTYFIKATOREM? | UTWÓRZ / ZAKTUALIZUJ |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  Identyfikator pracownika | **Tak** | Napisane przy tworzeniu tylko | 
|  **Jednostki administracyjnej**   |   l   |     | Tworzenie i aktualizowanie |
|  **Firmy**         | Firmy   |     |  Tworzenie i aktualizowanie |
|  **CountryReferenceTwoLetter**      |   co |     |   Tworzenie i aktualizowanie |
| **CountryReferenceTwoLetter**    |  C  |     |         Tworzenie i aktualizowanie |
| **SupervisoryOrganization**  | Dział  |     |  Tworzenie i aktualizowanie |
|  **PreferredNameData**  |  Nazwa wyświetlana |     |   Tworzenie i aktualizowanie |
| **Identyfikator pracownika**    |  Nazwa pospolita    |   |   Napisane przy tworzeniu tylko |
| **Faksów**      | facsimileTelephoneNumber     |     |    Tworzenie i aktualizowanie |
| **Imię**   | Imię       |     |    Tworzenie i aktualizowanie |
| **Przełącznik (\[Active\],, "0", "True", "1")** |  AccountDisabled      |     | Tworzenie i aktualizowanie |
| **Telefon komórkowy**  |    Telefon komórkowy       |     |       Napisane przy tworzeniu tylko |
| **EmailAddress**    | Poczty    |     |     Tworzenie i aktualizowanie |
| **ManagerReference**   | Menedżer  |     |  Tworzenie i aktualizowanie |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Tworzenie i aktualizowanie |
| **KodPocztowy**  |   KodPocztowy  |     | Tworzenie i aktualizowanie |
| **LocalReference** |  preferredLanguage  |     |  Tworzenie i aktualizowanie |
| ** Zastąp (Mid (Zastąp (\[identyfikator pracownika\],, "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\ &lt; \\ \\ &gt; \]) "," ",), 1, 20)," ([\\\\.) \* \$] (file:///\\.) *$)", , "", , )**      |    sAMAccountName            |     |         Napisane przy tworzeniu tylko |
| **Nazwisko**   |   SN   |     |  Tworzenie i aktualizowanie |
| **CountryRegionReference** |  St     |     | Tworzenie i aktualizowanie |
| **AddressLineData**    |  Adres  |     |   Tworzenie i aktualizowanie |
| **PrimaryWorkTelephone**  |  TelephoneNumber   |     | Napisane przy tworzeniu tylko |
| **BusinessTitle**   |  Tytuł     |     |  Tworzenie i aktualizowanie |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])" ,, "m",), "([ñńňÑŃŇN])", "n",), "([öòőõôóÖÒŐÕÔÓO])", "o",), "[P]", "p",), "([Q])", "q",), "([řŘR])", "r",), "([ßšśŠŚS])", "s",), "([TŤť])", "t",), "([üùûúůűÜÙÛÚŮŰU])", "u",), "([V])", "v",), "([W])", "w",), "([ýÿýŸÝY])", "y",), "([źžżŹŽŻZ])", "z",), "",,, "",), "contoso.com")**   | userPrincipalName     |     | Tworzenie i aktualizowanie                                                   
| **Przełącznika (\[jednostki administracyjnej\], "jednostki Organizacyjnej użytkowników standardowych, OU = użytkowników, OU = domyślne, OU = lokalizacjach, DC = = contoso, DC = com", "Dallas", "jednostki Organizacyjnej użytkowników standardowych, OU = użytkowników, OU = Dallas, OU = lokalizacjach, DC = = contoso, DC = com", "Austin", "jednostki Organizacyjnej użytkowników standardowych, OU = użytkowników, OU = Austin, OU = lokalizacjach, DC = = contoso, DC = com", "Seattle", "jednostki Organizacyjnej użytkowników standardowych, OU = użytkowników, OU = Seattle, OU = lokalizacjach, DC = = contoso, DC = com", "Londyn", "jednostki Organizacyjnej = użytkownicy w wersji Standard Jednostki Organizacyjnej użytkowników, OU = Londyn, OU = = lokalizacjach, DC = contoso, DC = com ")**  | parentDistinguishedName     |     |  Tworzenie i aktualizowanie |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Część 3: Konfigurowanie agenta synchronizacji lokalne powitania

W kolejności tooprovision tooActive w lokalnym katalogu na serwerze przyłączonym do domeny w desire hello lasu usługi Active Directory musi być zainstalowany agent. Administrator domeny (lub administratorem przedsiębiorstwa), poświadczenia są wymagane do wykonania procedury hello.

**[Możesz pobrać agent synchronizacji lokalne powitania tutaj](https://go.microsoft.com/fwlink/?linkid=847801)**

Po zainstalowaniu agenta, Uruchom polecenia programu Powershell hello poniżej tooconfigure hello agenta w danym środowisku.

**Polecenie #1**

> CD C:\\pliki programów\\Agent synchronizacji usługi Microsoft Azure Active Directory\\modułów\\AADSyncAgent

> Import-module AADSyncAgent.psd1

**Polecenie #2**

> Dodaj ADSyncAgentActiveDirectoryConfiguration

* Wejście: "Nazwa katalogu", wprowadź nazwę lasu hello AD, jak został wprowadzony w części \#2
* Wejście: Nazwa użytkownika i hasło dla lasu usługi Active Directory

**Polecenie #3**

> Dodaj ADSyncAgentAzureActiveDirectoryConfiguration

* Wejście: Nazwa użytkownika administratora globalnego i hasło dla dzierżawy usługi Azure AD

**Polecenie #4**

> Get-AdSyncAgentProvisioningTasks

* Akcja: Upewnij się, że dane są zwracane. To polecenie automatycznie odnajduje produktu Workday Inicjowanie obsługi aplikacji w dzierżawie usługi Azure AD. Przykładowe dane wyjściowe:

> Nazwa: Moje lesie usługi Active Directory
>
> Włączono: True
>
> DirectoryName: mydomain.contoso.com
>
> Przetwarzający: False
>
> Identyfikator: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Polecenie #5**

> Start AdSyncAgentSynchronization-automatyczne

**Polecenie #6**

> polecenie net stop aadsyncagent

**Polecenie #7**

> polecenie net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Część 4: Usługa hello Start
Po zakończeniu części 1-3, można uruchomić hello usługi w portalu zarządzania Azure hello inicjowania obsługi administracyjnej.

1.  W hello **inicjowania obsługi administracyjnej** kartę, zestaw hello **stan inicjowania obsługi administracyjnej** do **na**.

2. Kliknij pozycję **Zapisz**.

3. Spowoduje to uruchomienie synchronizacji początkowej hello, jakie mogą mieć różną liczbą godzin, zależnie od liczby użytkowników znajdują się w pracy.

4. Synchronizacja poszczególnych zdarzeń, takich jak użytkownicy są odczytywane z produktem Workday, a następnie później dodane lub zaktualizowane tooActive katalogu, można wyświetlić w hello **dzienników inspekcji** kartę. **[Zobacz hello inicjowania obsługi administracyjnej Przewodnik po raportowaniu szczegółowe instrukcje sposobu tooread hello inspekcji logowania](active-directory-saas-provisioning-reporting.md)**

5.  Dziennik aplikacji systemu Windows Hello na maszynie agenta hello zostaną wyświetlone wszystkie operacje wykonane przez agenta hello.

6. Jeden ukończone, będą zapisywane podsumowanie inspekcji **inicjowania obsługi administracyjnej** karcie, jak pokazano poniżej.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Konfigurowanie inicjowania obsługi administracyjnej tooAzure usługi Active Directory użytkownika
Jak skonfigurować tooAzure zastrzegania usługi Active Directory zależy od wymagań inicjowania obsługi administracyjnej, zgodnie z opisem w poniższej tabeli hello.

| Scenariusz | Rozwiązanie |
| -------- | -------- |
| **Użytkownicy muszą tooActive toobe elastycznie Directory i Azure AD** | Użyj  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Użytkownicy muszą toobe elastycznie tooActive katalogu tylko** | Użyj  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Użytkownicy muszą toobe elastycznie tooAzure AD tylko (chmura tylko)** | Użyj hello **inicjowania obsługi usługi Active Directory tooAzure produktu Workday** aplikacji w galerii aplikacji hello |

Aby uzyskać instrukcje na temat konfigurowania usługi Azure AD Connect, zobacz hello [dokumentacji usługi Azure AD Connect](connect/active-directory-aadconnect.md).

Hello następujące sekcje opisują Konfigurowanie połączenia między produktu Workday i Azure AD tooprovision tylko w chmurze użytkowników.

> [!IMPORTANT]
> Tylko wykonaj poniższą procedurę hello, jeśli masz tylko w chmurze użytkowników, którzy potrzebują tooAzure toobe elastycznie AD i nie lokalnej usługi Active Directory.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Część 1: Dodawanie hello Azure AD inicjowania obsługi administracyjnej łącznik aplikacji i tworzenie hello tooWorkday połączenia

**tooconfigure produktu Workday tooAzure usługi Active Directory inicjowania obsługi administracyjnej dla użytkowników tylko w chmurze:**

1.  Przejdź za<https://portal.azure.com>.

2.  Na pasku nawigacyjnym po lewej stronie powitania, wybierz **usługi Azure Active Directory**

3.  Wybierz **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.

4.  Wybierz **dodać aplikację**, a następnie wybierz hello **wszystkie** kategorii.

5.  Wyszukaj **udostępniania tooAzure AD produktu Workday**i Dodaj danej aplikacji hello galerii.

6.  Hello — po dodaniu aplikacji i jest wyświetlany ekran szczegółów aplikacji hello, wybierz **inicjowania obsługi administracyjnej**

7.  Zmień hello **inicjowania obsługi administracyjnej** **tryb** zbyt**automatyczne**

8.  Zakończenie hello **poświadczeń administratora** sekcji w następujący sposób:

   * **Nazwa użytkownika administratora** — wprowadź nazwę użytkownika hello z hello produktu Workday integracji konto system, nazwę domeny dzierżawy hello dołączane. Powinien wyglądać mniej więcej tak:username@contoso4

   * **Hasło administratora —** wprowadź hasło hello hello produktu Workday integracji systemu konta

   * **Adres URL — dzierżawy** Wprowadź końcowy usług sieci web produktu Workday toohello hello adres URL dzierżawy. To powinien wyglądać następująco: https://wd3-impl-services1.workday.com/ccx/service/contoso4, gdzie contoso4 jest zastępowany nazwa dzierżawy poprawne, a wd3 impl jest zastępowany hello poprawne środowisko ciąg (Jeśli to konieczne).

   * **Wiadomość E-mail z powiadomieniem —** wprowadź swój adres e-mail, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail, jeśli wystąpi błąd".

   * Kliknij przycisk hello **Testuj połączenie** przycisku.

   * Jeśli test połączenia hello zakończy się powodzeniem, kliknij przycisk hello **zapisać** przycisk u góry hello. W przypadku niepowodzenia dokładnie Sprawdź ten adres URL produktu Workday hello i poświadczenia są prawidłowe w pracy.


### <a name="part-2-configure-attribute-mappings"></a>Część 2: Konfigurowanie mapowań atrybutów 

W tej sekcji skonfigurujesz, jak dane użytkownika wypływających z produktu Workday do usługi Azure Active Directory dla użytkowników tylko w chmurze.

1.  Na karcie Udostępnianie hello w obszarze **mapowania**, kliknij przycisk **tooAzure zsynchronizować pracowników AD**.

2.   W hello **zakres obiektu źródłowego** pole, można wybrać, które zestawów użytkowników w pracy powinna być w zakresie obsługi tooAzure AD, definiując zestaw opartych na atrybutach filtrów. zakres domyślnej Hello jest "wszyscy użytkownicy w pracy". Przykładowe filtry:

   * Przykład: Toousers zakres z identyfikatorami procesu roboczego między 1000000 i 2000000

      * Atrybut: WorkerID

      * Operator: Dopasowanie wyrażenia REGULARNEGO

      * Wartość: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Przykład: Tylko warunkowe pracowników i pracowników nie regularne

      * Atrybut: ContingentID

      * Operator: Nie ma wartości NULL

3.  W hello **akcji obiektów docelowych** pole globalnie filtrowania, jakie akcje mogą toobe w usłudze Azure AD. **Utwórz** i **aktualizacji** są najczęściej.

4.  W hello **mapowania atrybutów** sekcji, można zdefiniować poszczególne produktu Workday atrybuty mapy tooActive atrybutów katalogu.

5. Kliknij na istniejących tooupdate mapowanie atrybutu lub **Dodaj nowe mapowanie** u dołu hello hello ekranu tooadd nowe mapowania. Mapowanie atrybutu poszczególnych obsługuje następujące właściwości:

   * **Typ mapowania**

      * **Bezpośrednie** — zapisuje hello wartość atrybutu hello produktu Workday atrybutu toohello AD, bez zmian

      * **Stała** -zapisać wartości ciągu statycznych, stałych do atrybutu hello AD

      * **Wyrażenie** — pozwala toowrite Niestandardowa wartość atrybutu hello AD, na podstawie co najmniej jeden dzień roboczy atrybutów. [Aby uzyskać więcej informacji, zobacz ten artykuł wyrażeń](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Atrybut źródłowy** -hello atrybut użytkownika z produktu Workday.

   * **Wartość domyślna** — jest to opcjonalne. Jeśli atrybut źródłowy hello ma wartość pustą, mapowanie hello zapisu wtedy tę wartość.
            Najbardziej typowe konfiguracje jest tooleave tym puste.

   * **Atrybut TARGET** — Witaj atrybut użytkownika w usłudze Azure AD.

   * **Zgodne obiektów przy użyciu tego atrybutu** — czy stosuje się to mapowanie toouniquely zidentyfikować użytkowników między produktu Workday i Azure AD. Jest to zazwyczaj ustawiona w polu Identyfikator procesu roboczego dla produktu Workday, która zwykle jest mapowana na powitania identyfikator atrybutu (nowy) lub atrybutu rozszerzenia w usłudze Azure AD.

   * **Dopasowywanie pierwszeństwo** — wiele pasujących atrybuty można ustawić. Jeśli dostępnych jest wiele, są oceniane pod w kolejności wynika z tego pola. Jak dopasowania zostanie znaleziony, żadne dodatkowe dopasowania atrybuty są oceniane.

   * **Zastosuj to mapowanie**

     * **Zawsze** — Zastosuj to mapowanie na obu Tworzenie użytkownika i aktualizowanie akcji

     * **Tylko podczas tworzenia** -Zastosuj to mapowanie tylko akcje creation użytkownika

6. toosave mapowania, kliknij przycisk **zapisać** u góry hello sekcji atrybutu mapowania.

### <a name="part-3-start-hello-service"></a>Część 3: Usługa hello Start
Po zakończeniu części 1 i 2, można uruchomić hello inicjowania obsługi usługi.

1.  W hello **inicjowania obsługi administracyjnej** kartę, zestaw hello **stan inicjowania obsługi administracyjnej** do **na**.

2. Kliknij pozycję **Zapisz**.

3. Spowoduje to uruchomienie synchronizacji początkowej hello, jakie mogą mieć różną liczbą godzin, zależnie od liczby użytkowników znajdują się w pracy.

4. Synchronizacja poszczególnych zdarzeń mogą być wyświetlane w hello **dzienników inspekcji** kartę. **[Zobacz hello inicjowania obsługi administracyjnej Przewodnik po raportowaniu szczegółowe instrukcje sposobu tooread hello inspekcji logowania](active-directory-saas-provisioning-reporting.md)**

5. Jeden ukończone, będą zapisywane podsumowanie inspekcji **inicjowania obsługi administracyjnej** karcie, jak pokazano poniżej.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Konfigurowanie zapisywanie zwrotne tooWorkday adresy e-mail
Wykonaj te zapisywanie zwrotne tooconfigure instrukcje adresu e-mail użytkownika z tooWorkday usługi Azure Active Directory.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Część 1: Dodawanie hello inicjowania obsługi administracyjnej łącznik aplikacji i tworzenie hello tooWorkday połączenia

**tooconfigure produktu Workday tooActive katalogu inicjowania obsługi administracyjnej:**

1.  Przejdź do zbyt<https://portal.azure.com>

2.  Na pasku nawigacyjnym po lewej stronie powitania, wybierz **usługi Azure Active Directory**

3.  Wybierz **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.

4.  Wybierz **dodać aplikację**, a następnie wybierz pozycję hello **wszystkie** kategorii.

5.  Wyszukaj **zapisywania zwrotnego produktu Workday**i Dodaj danej aplikacji hello galerii.

6.  Hello — po dodaniu aplikacji i jest wyświetlany ekran szczegółów aplikacji hello, wybierz **inicjowania obsługi administracyjnej**

7.  Zmień hello **inicjowania obsługi administracyjnej** **tryb** zbyt**automatyczne**

8.  Zakończenie hello **poświadczeń administratora** sekcji w następujący sposób:

   * **Nazwa użytkownika administratora** — wprowadź nazwę użytkownika hello z hello produktu Workday integracji konto system, nazwę domeny dzierżawy hello dołączane. Powinien wyglądać mniej więcej tak:username@contoso4

   * **Hasło administratora —** wprowadź hasło hello hello produktu Workday integracji systemu konta

   * **Adres URL — dzierżawy** Wprowadź końcowy usług sieci web produktu Workday toohello hello adres URL dzierżawy. To powinien wyglądać następująco: https://wd3-impl-services1.workday.com/ccx/service/contoso4, gdzie contoso4 jest zastępowany nazwa dzierżawy poprawne, a wd3 impl jest zastępowany hello poprawne środowisko ciąg (Jeśli to konieczne).

   * **Wiadomość E-mail z powiadomieniem —** wprowadź swój adres e-mail, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail, jeśli wystąpi błąd".

   * Kliknij przycisk hello **Testuj połączenie** przycisku. Jeśli test połączenia hello zakończy się powodzeniem, kliknij przycisk hello **zapisać** przycisk u góry hello. W przypadku niepowodzenia dokładnie Sprawdź ten adres URL produktu Workday hello i poświadczenia są prawidłowe w pracy.


### <a name="part-2-configure-attribute-mappings"></a>Część 2: Konfigurowanie mapowań atrybutów 


W tej sekcji skonfigurujesz, jak dane użytkownika wypływających z produktu Workday do usługi Active Directory.

1.  Na karcie Udostępnianie hello w obszarze **mapowania**, kliknij przycisk **tooWorkday synchronizacji Azure AD użytkownicy**.

2.  W hello **zakres obiektu źródłowego** pole, można również filtrować które zestawów użytkowników w usłudze Azure Active Directory powinny mieć ich adresów e-mail zapisywane tooWorkday. zakres domyślnej Hello jest "wszyscy użytkownicy w usłudze Azure AD". 

3.  W hello **mapowania atrybutów** sekcji, można zdefiniować poszczególne produktu Workday atrybuty mapy tooActive atrybutów katalogu. Brak mapowania dla adresu e-mail hello domyślnie. Jednak hello zgodnym Identyfikatorem musi być toomatch zaktualizowanych użytkowników w usłudze Azure AD z ich odpowiednie pozycje w pracy. Popularne odpowiadającej metody jest identyfikator procesu roboczego produktu Workday hello toosynchronize lub pracowników IDENTYFIKATORA tooextensionAttribute1 15 w usłudze Azure AD, a następnie użyć tego atrybutu w usłudze Azure AD użytkownicy toomatch w pracy.

4.  toosave mapowania, kliknij przycisk **zapisać** u góry hello hello sekcji atrybutu mapowania.

### <a name="part-3-start-hello-service"></a>Część 3: Usługa hello Start
Po zakończeniu części 1 i 2, można uruchomić hello inicjowania obsługi usługi.

1.  W hello **inicjowania obsługi administracyjnej** kartę, zestaw hello **stan inicjowania obsługi administracyjnej** do **na**.

2. Kliknij pozycję **Zapisz**.

3. Spowoduje to uruchomienie synchronizacji początkowej hello, jakie mogą mieć różną liczbą godzin, zależnie od liczby użytkowników znajdują się w pracy.

4. Synchronizacja poszczególnych zdarzeń mogą być wyświetlane w hello **dzienników inspekcji** kartę. **[Zobacz hello inicjowania obsługi administracyjnej Przewodnik po raportowaniu szczegółowe instrukcje sposobu tooread hello inspekcji logowania](active-directory-saas-provisioning-reporting.md)**

5. Jeden ukończone, będą zapisywane podsumowanie inspekcji **inicjowania obsługi administracyjnej** karcie, jak pokazano poniżej.

## <a name="known-issues"></a>Znane problemy

* **Dzienniki przy ustawieniach regionalnych Europejskiego inspekcji** — wersji hello tej wersji technical preview, jest to znany problem z hello [dzienniki inspekcji](active-directory-saas-provisioning-reporting.md) dla aplikacji łącznika produktu Workday hello nie pojawia się w hello [portaluAzure](https://portal.azure.com) Jeśli dzierżawy usługi Azure AD hello znajduje się w centrum danych Europejskich. Nadchodzi poprawkę dotyczącą tego problemu. Sprawdź, czy to miejsce ponownie w hello niemal przyszłych aktualizacji. 

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Samouczek: Konfigurowanie logowania jednokrotnego między produktu Workday i Azure Active Directory](active-directory-saas-workday-tutorial.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
