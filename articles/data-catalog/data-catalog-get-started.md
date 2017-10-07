---
title: "wprowadzenie do usługi Data Catalog aaaGet | Dokumentacja firmy Microsoft"
description: "Scenariusze hello i możliwości usługi Azure Data Catalog ten kompleksowy samouczek end-to-end."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Rozpoczynanie pracy z usługą Azure Data Catalog
Azure Data Catalog to w pełni zarządzana usługa w chmurze służąca jako system rejestracji i odnajdywania zasobów danych przedsiębiorstwa. Szczegółowe omówienie tej usługi można znaleźć w artykule [Co to jest usługa Azure Data Catalog?](data-catalog-what-is-data-catalog.md).

Ten samouczek ułatwia rozpoczęcie pracy z usługą Azure Data Catalog Należy wykonać hello procedur przedstawionych w tym samouczku:

| Procedura | Opis |
|:--- |:--- |
| [Aprowizowanie wykazu danych](#provision-data-catalog) |Ta procedura obejmuje aprowizację lub konfigurację usługi Azure Data Catalog. Należy wykonać ten krok tylko wtedy, gdy katalog hello nie skonfigurowano przed. W ramach jednej organizacji (domeny usługi Microsoft Azure Active Directory) może istnieć tylko jeden wykaz danych, nawet jeśli z kontem platformy Azure jest powiązanych wiele subskrypcji. |
| [Rejestrowanie zasobów danych](#register-data-assets) |W ramach tej procedury należy zarejestrować zasobów danych z bazy danych przykładowych AdventureWorks2014 hello hello data Catalog. Rejestracja jest proces hello wyodrębnianie kluczowych metadanych strukturalnych, takich jak nazwy, typy i lokalizacje hello źródła danych i skopiowaniu tego wykazu toohello metadanych. Witaj źródła danych i zasobów danych pozostają gdzie są one, ale metadane hello jest używany przez toomake katalogu hello je łatwiej odnaleźć i zrozumieć. |
| [Odnajdywanie zasobów danych](#discover-data-assets) |W tej procedury należy użyć hello Azure Data Catalog portalu toodiscover danych zasobów, które zostały zarejestrowane w poprzednim kroku hello. Po zarejestrowaniu źródła danych z usługi Azure Data Catalog metadanych jest indeksowany przez usługę hello, dzięki czemu użytkownicy mogą łatwo wyszukiwać hello danych, które są im potrzebne. |
| [Dodawanie adnotacji do zasobów danych](#annotate-data-assets) |W ramach tej procedury Podaj adnotacje (informacje takie jak opisy, tagi, dokumentacji lub ekspertów) dla hello zasobów danych. Te informacje uzupełniające hello metadanych wyodrębnionych ze źródła danych hello i źródła danych hello toomake więcej toomore zrozumiały dla osób. |
| [Łączenie zasobów toodata](#connect-to-data-assets) |Ta procedura obejmuje otwieranie zasobów danych za pomocą zintegrowanych narzędzi klienckich (na przykład programu Excel i narzędzi SQL Server Data Tools) oraz narzędzia niezintegrowanego (programu SQL Server Management Studio). |
| [Zarządzanie zasobami danych](#manage-data-assets) |Ta procedura dotyczy konfigurowania zabezpieczeń zasobów danych. Wykaz danych nie zapewniają użytkownikom samych danych toohello dostępu. Właściciel Hello źródła danych hello kontroluje dostęp do danych. <br/><br/> Data Catalog może odnaleźć źródła danych i widok hello **metadanych** powiązane źródła toohello zarejestrowane w wykazie hello. Może to być sytuacjach, jednak źródła danych powinny być widoczne tylko toospecific użytkowników lub toomembers określonych grup. W tych sytuacjach można użyć własność tootake wykazu danych zarejestrowanych zasobów danych w ramach hello katalogu i kontroli hello widoczność zasobów hello, którego jesteś właścicielem. |
| [Usuwanie zasobów danych](#remove-data-assets) |W tej procedurze możesz dowiedzieć się, jak tooremove zasobów danych z hello wykazu danych. |

## <a name="tutorial-prerequisites"></a>Wymagania wstępne dotyczące samouczka
### <a name="azure-subscription"></a>Subskrypcja platformy Azure
tooset się wykaz danych Azure, musi być właścicielem hello lub współwłaściciel subskrypcji platformy Azure.

Subskrypcje platformy Azure ułatwić organizowanie dostępu toocloud usługi zasobów, takich jak Azure Data Catalog. Subskrypcje te ułatwiają również zarządzanie raportowaniem i rozliczaniem użycia zasobów oraz regulowaniem płatności za to użycie. Poszczególne subskrypcje mogą mieć różne ustawienia rozliczeń i płatności, co pozwala na korzystanie z wielu subskrypcji i planów dostosowanych do potrzeb konkretnych działów, projektów, biur regionalnych itp. Co usługa w chmurze należy tooa subskrypcji, i wymagają toohave subskrypcji przed rozpoczęciem konfigurowania usługi Azure Data Catalog. toolearn więcej, zobacz [Zarządzanie kontami, subskrypcje i ról administracyjnych](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

### <a name="azure-active-directory"></a>Usługa Azure Active Directory
tooset się wykaz danych Azure, użytkownik musi zalogować się przy użyciu konta użytkownika usługi Azure Active Directory (Azure AD). Musisz być właścicielem hello lub współwłaściciel subskrypcji platformy Azure.  

Usługa Azure AD zapewnia prosty sposób dla firm toomanage tożsamości i dostępu, zarówno w chmurze hello i lokalnymi. Można użyć pojedynczego pracy lub toosign konta służbowego, które znajdują się w chmurze tooany lub lokalnej aplikacji sieci web. Azure Data Catalog używa usługi Azure AD tooauthenticate logowania. toolearn więcej, zobacz [co to jest usługa Azure Active Directory](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Konfiguracja zasad usługi Azure Active Directory
Może wystąpić sytuacja, w których możesz zalogować się toohello portalu wykazu danych Azure, ale podczas próby toosign w narzędzia rejestracji źródła danych toohello, wystąpi komunikat o błędzie, który uniemożliwia rejestrowanie. Ten błąd może wystąpić, gdy znajduje się w sieci firmowej hello lub gdy nawiązujesz połączenie z hello poza siecią firmową.

Narzędzie rejestracji Hello używa *uwierzytelnianie formularzy* toovalidate logowania użytkowników z usługą Azure Active Directory. Do pomyślnego logowania, administrator usługi Azure Active Directory należy włączyć uwierzytelnianie formularzy w hello *globalne zasady uwierzytelniania*.

Z hello globalne zasady uwierzytelniania można włączyć uwierzytelnianie oddzielnie w intranecie i ekstranecie połączenia, jak pokazano w powitania po obrazu. Błędy logowania może wystąpić, jeśli nie włączono uwierzytelniania formularzy hello sieci, z którym się łączysz.

 ![Globalne zasady uwierzytelniania usługi Azure Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Aby uzyskać więcej informacji, zobacz artykuł [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Aprowizowanie wykazu danych
W ramach organizacji — domeny usługi Azure Active Directory — można aprowizować tylko jeden wykaz danych. W związku z tym jeśli właściciel hello lub współwłaściciel subskrypcji platformy Azure, który należy toothis domeny usługi Azure Active Directory ma już utworzony wykaz, nie będzie możliwe toocreate wykaz ponownie nawet, jeśli masz wiele subskrypcji Azure. tootest, czy wykaz danych został utworzony przez użytkownika w domenie usługi Active Directory Azure, przejdź toohello [strona główna usługi Azure Data Catalog](http://azuredatacatalog.com) i sprawdź, czy katalog hello jest wyświetlany. Jeśli utworzono już katalog dla Ciebie, Pomiń powitania po następnej sekcji toohello procedury, a następnie przejść.    

1. Przejdź toohello [stronę usługi Data Catalog](https://azure.microsoft.com/services/data-catalog) i kliknij przycisk **wprowadzenie**.
   
    ![Usługa Azure Data Catalog — marketingowa strona docelowa](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Zaloguj się przy użyciu konta użytkownika będącego właścicielem hello lub współwłaściciel subskrypcji platformy Azure. Zostanie wyświetlony powitania po stronie po zalogowaniu.
   
    ![Usługa Azure Data Catalog — aprowizowanie wykazu danych](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Określ **nazwa** dla usługi data catalog hello, hello **subskrypcji** toouse, a następnie hello **lokalizacji** hello katalogu.
4. Rozwiń sekcję **Cennik** i wybierz **wersję** usługi Azure Data Catalog (Bezpłatna lub Standardowa).
    ![Usługa Azure Data Catalog — wybieranie wersji](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Rozwiń węzeł **użytkownicy wykazu** i kliknij przycisk **Dodaj** tooadd użytkowników dla usługi data catalog hello. Toothis grupy są automatycznie dodawane.
    ![Usługa Azure Data Catalog — użytkownicy](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Rozwiń węzeł **Administratorzy katalogu** i kliknij przycisk **Dodaj** tooadd kolejnych administratorów hello wykazu danych. Toothis grupy są automatycznie dodawane.
    ![Usługa Azure Data Catalog — administratorzy](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Kliknij przycisk **tworzenia katalogu** toocreate hello danych katalogu dla organizacji. Zostanie wyświetlona strona główna hello hello wykazu danych, po jego utworzeniu.
    ![Usługa Azure Data Catalog — utworzony wykaz](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Znajdź katalog danych hello portalu Azure
1. Na osobnej karcie w przeglądarce sieci web hello lub w oknie przeglądarki WWW, przejdź toohello [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu hello tego samego konta tej możesz używane toocreate hello usługi data catalog w poprzednim kroku hello.
2. Wybierz pozycję **Przeglądaj**, a następnie kliknij pozycję **Wykaz danych**.
   
    ![Wykaz danych Azure — Przeglądaj Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) zostaną wyświetlone dane hello utworzonego w katalogu.
   
    ![Usługa Azure Data Catalog — wykaz widoczny na liście](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Kliknij katalog hello, który został utworzony. Zobacz hello **Data Catalog** bloku w portalu hello.
   
   ![Usługa Azure Data Catalog — blok w portalu ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Można wyświetlić właściwości wykazu danych hello i zaktualizuj je. Na przykład kliknij pozycję **warstwa cenowa** i zmienić hello wersji.
   
    ![Usługa Azure Data Catalog — warstwa cenowa](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Przykładowa baza danych firmy Adventure Works
W tym samouczku zarejestrować zasobów danych (tabele) z hello AdventureWorks2014 bazę danych w hello aparatu bazy danych programu SQL Server, ale można użyć dowolnego obsługiwanego źródła danych, jeśli wolisz toowork z roli tooyour znanego i odpowiednie dane. Aby uzyskać listę obsługiwanych źródeł danych, zobacz [Supported data sources](data-catalog-dsr.md) (Obsługiwane źródła danych).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Bazy danych Adventure Works 2014 OLTP hello instalacji
Baza danych firmy Adventure Works Hello obsługuje standardowe scenariusze przetwarzania transakcji online dla fikcyjnego producenta rowerów (Firma Adventure Works Cycles), który zawiera produkty, sprzedaży i kupna. W tym samouczku informacje o produktach zostaną zarejestrowane w usłudze Azure Data Catalog.

tooinstall hello Adventure Works przykładowa baza danych:

1. Pobierz plik [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) z witryny CodePlex.
2. toorestore hello z bazy danych na komputerze, wykonaj te instrukcje hello [przywrócić kopię zapasową bazy danych przy użyciu programu SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), lub wykonaj następujące czynności:
   1. Otwórz program SQL Server Management Studio i połącz toohello aparatu bazy danych programu SQL Server.
   2. Kliknij prawym przyciskiem myszy pozycję **Bazy danych** i kliknij polecenie **Przywróć bazę danych**.
   3. W obszarze **Restore Database**, kliknij przycisk hello **urządzenia** opcja dla **źródła** i kliknij przycisk **Przeglądaj**.
   4. W obszarze **Wybieranie urządzeń kopii zapasowej** kliknij pozycję **Dodaj**.
   5. Przejdź toohello folder, gdzie masz hello **AdventureWorks2014.bak** plik, wybierz opcję hello i kliknij przycisk **OK** tooclose hello **zlokalizuj plik kopii zapasowej** okno dialogowe.
   6. Kliknij przycisk **OK** tooclose hello **wybierz urządzenia kopii zapasowej** okno dialogowe.    
   7. Kliknij przycisk **OK** tooclose hello **Restore Database** okno dialogowe.

Możesz teraz zarejestrować zasobów danych z bazy danych przykładowej firmy Adventure Works hello przy użyciu usługi Azure Data Catalog.

## <a name="register-data-assets"></a>Rejestrowanie zasobów danych
W tym ćwiczeniu hello rejestracji narzędzia tooregister zasobów danych z bazy danych firmy Adventure Works hello jest używany z hello katalogu. Rejestracja jest hello proces wyodrębniania kluczowych metadanych strukturalnych, takich jak nazwy, typy i lokalizacje hello źródła danych i hello zasoby, które zawiera, a następnie skopiować ten katalog toohello metadanych. Witaj źródła danych i zasobów danych pozostają gdzie są one, ale metadane hello jest używany przez toomake katalogu hello je łatwiej odnaleźć i zrozumieć.

### <a name="register-a-data-source"></a>Rejestrowanie źródła danych
1. Przejdź toohello [strona główna usługi Azure Data Catalog](http://azuredatacatalog.com) i kliknij przycisk **publikowania danych**.
   
   ![Usługa Azure Data Catalog — przycisk Publikuj dane](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Kliknij przycisk **uruchamianie aplikacji** toodownload, instalacji i narzędzia rejestracji wykonywania hello na tym komputerze.
   
   ![Usługa Azure Data Catalog — przycisk Uruchom](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Na powitania **powitalnej** kliknij przycisk **Zaloguj** i wprowadź swoje poświadczenia.     
   
    ![Usługa Azure Data Catalog — strona powitalna](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Na powitania **Microsoft Azure Data Catalog** kliknij przycisk **programu SQL Server** i **dalej**.
   
    ![Usługa Azure Data Catalog — źródła danych](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Wprowadź właściwości połączenia serwera SQL hello **AdventureWorks2014** (zobacz poniższy przykład hello) i kliknij przycisk **CONNECT**.
   
   ![Usługa Azure Data Catalog — ustawienia połączenia programu SQL Server](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Zarejestruj hello metadane zawartości danych. W tym przykładzie należy zarejestrować **Production/Product** obiektów z nazw AdventureWorks Production hello:
   
   1. W hello **hierarchii serwerów** drzewa, a następnie rozwiń **AdventureWorks2014** i kliknij przycisk **produkcji**.
   2. Naciśnij klawisz Ctrl i kliknij pozycje **Product**, **ProductCategory**, **ProductDescription** i **ProductPhoto**.
   3. Kliknij przycisk hello **przenieść strzałkę** (**>**). Ta akcja powoduje przeniesienie wszystkich wybranych obiektów do hello **toobe obiektów w zarejestrowany** listy.
      
      ![Samouczek dotyczący usługi Azure Data Catalog — przeglądanie i wybieranie obiektów](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Wybierz **Dołącz Podgląd** tooinclude Podgląd migawki hello danych. migawki Hello zawiera too20 rekordów z każdej tabeli i jest kopiowany do katalogu hello.
   5. Wybierz **obejmują dane profilu** tooinclude migawkę statystyki obiektu hello hello danych profilu (na przykład: minimalne, maksymalne i średnie wartości kolumny, liczba wierszy).
   6. W hello **Dodaj tagi** wprowadź **adventure works, cykli**. Spowoduje to dodanie tagów wyszukiwania dla tych zasobów danych. Tagi to doskonały sposób którą toohelp użytkownikom znalezienia zarejestrowanego źródła danych.
   7. Określ nazwę hello **ekspertów** na tych danych (opcjonalnie).
      
      ![Samouczek usługi Azure Data Catalog — toobe obiektów w zarejestrowany](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Kliknij pozycję **ZAREJESTRUJ**. Wybrane obiekty zostaną zarejestrowane za pomocą usługi Azure Data Catalog. W tym ćwiczeniu są rejestrowane hello wybrane obiekty z firmy Adventure Works. Narzędzie rejestracji Hello wyodrębnianie metadanych z hello zasobu danych i kopiuje dane do usługi Azure Data Catalog hello. Witaj dane pozostaną gdzie ona się teraz znajduje i pozostaje pod kontrolą hello hello administratorów i zasady hello bieżącego systemu.
      
      ![Usługa Azure Data Catalog — zarejestrowane obiekty](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. toosee Twojego zarejestrowane obiekty źródła danych, kliknij przycisk **Wyświetl Portal**. W portalu Azure Data Catalog hello upewnij się, że widoczne wszystkie cztery tabele i hello bazy danych, w widoku siatki hello.
      
      ![Obiekty w portalu Azure Data Catalog hello ](media/data-catalog-get-started/data-catalog-view-portal.png)

W tym ćwiczeniu zarejestrowano obiekty z hello Adventure Works przykładowej bazy danych, aby łatwo ich odnajdowane przez użytkowników w organizacji. W następnym ćwiczeniu hello możesz dowiedzieć się, jak toodiscover zarejestrowanych zasobów danych.

## <a name="discover-data-assets"></a>Odnajdywanie zasobów danych
Odnajdywanie w usłudze Azure Data Catalog korzysta z dwóch głównych mechanizmów: wyszukiwania i filtrowania.

Wyszukiwanie jest zaprojektowana toobe intuicyjny i wydajne. Domyślnie terminy wyszukiwania są dopasowywane do żadnej właściwości w katalogu hello, łącznie z adnotacjami dostarczane przez użytkownika.

Filtrowanie zaprojektowano toocomplement wyszukiwania. Można wybrać określone właściwości, takie jak ekspertów, typ źródła danych, typu obiektu i dopasowywanie zasobów danych i wyszukiwania tooconstrain tooview tagi powoduje toomatching zasoby.

Przy użyciu kombinacji wyszukiwania i filtrowania, można szybko przejść hello źródeł danych, które zostały zarejestrowane w zasobów danych hello toodiscover Azure Data Catalog, które są potrzebne.

W tym ćwiczeniu używasz zasobów danych pakietu hello Azure Data Catalog toodiscover portalu, zarejestrowanej w poprzednim ćwiczeniu hello. Aby uzyskać szczegółowe informacje o składni wyszukiwania, zobacz artykuł [Data Catalog Search syntax reference](https://msdn.microsoft.com/library/azure/mt267594.aspx) (Dokumentacja dotycząca składni wyszukiwania w usłudze Data Catalog).

Poniżej przedstawiono kilka przykładów do odnajdywania zasobów danych w katalogu hello.  

### <a name="discover-data-assets-with-basic-search"></a>Odnajdywanie zasobów danych przy użyciu wyszukiwania podstawowego
Wyszukiwanie podstawowe ułatwia przeszukiwanie wykazu za pomocą co najmniej jednego wyszukiwanego terminu. Wyniki są wszystkie zasoby zgodnych żadnej właściwości z co najmniej jednego z warunków hello określony.

1. Kliknij przycisk **Home** w portalu Azure Data Catalog hello. Po zamknięciu przeglądarki sieci web hello Przejdź toohello [strona główna usługi Azure Data Catalog](https://www.azuredatacatalog.com).
2. W polu wyszukiwania hello wpisz `cycles` i naciśnij klawisz **ENTER**.
   
    ![Usługa Azure Data Catalog — podstawowe wyszukiwanie tekstowe](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Upewnij się, że widoczne wszystkie cztery tabele i hello bazy danych (AdventureWorks2014) w wynikach hello. Można przełączać się między **widoku siatki** i **widok listy** za pomocą przycisków na pasku narzędzi hello, pokazane na powitania po obrazu. Zwróć uwagę, że słowa kluczowe do wyszukania hello jest wyróżniony w wynikach wyszukiwania hello, ponieważ hello **zaznacz** jest opcja **ON**. Można również określić liczbę hello **wyników na stronie** w wynikach wyszukiwania.
   
    ![Usługa Azure Data Catalog — wyniki podstawowego wyszukiwania tekstowego](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Witaj **wyszukiwania** panelu znajduje się na powitania po lewej i hello **właściwości** panelu znajduje się na powitania prawo. Na powitania **wyszukiwania** panelu, można zmienić kryteria wyszukiwania i filtrowania wyników. Witaj **właściwości** panelu Wyświetla właściwości zaznaczonego obiektu w siatce hello lub na liście.
4. Kliknij przycisk **produktu** w wynikach wyszukiwania hello. Kliknij hello **Podgląd**, **kolumn**, **danych profilu**, i **dokumentacji** karty, lub kliknij przycisk hello Strzałka tooexpand hello dolnym okienku.  
   
    ![Usługa Azure Data Catalog — dolne okienko](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Na powitania **Podgląd** kartę, możesz wyświetlić podgląd danych hello w hello **produktu** tabeli.  
5. Kliknij hello **kolumn** karcie toofind szczegóły kolumn (takich jak **nazwa** i **— typ danych**) w hello danych zasobów.
6. Kliknij hello **danych profilu** karcie toosee hello profilowania danych (na przykład: liczba wierszy, rozmiar danych lub minimalnej wartości w kolumnie) w hello danych zasobów.
7. Filtrowanie wyników hello za pomocą **filtry** powitania po lewej stronie. Na przykład kliknij pozycję **tabeli** dla **typ obiektu**, i zobaczyć hello czterech tabel, nie hello bazy danych.
   
    ![Usługa Azure Data Catalog — filtrowanie wyników wyszukiwania](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Odnajdywanie zasobów danych za pomocą wyznaczania zakresu właściwości
Właściwości zakresu odnajdywania zasobów danych, w którym hello wyszukiwany termin jest zgodny z hello pomaga określić właściwości.

1. Wyczyść hello **tabeli** filtrować pod **typ obiektu** w **filtry**.  
2. W polu wyszukiwania hello wpisz `tags:cycles` i naciśnij klawisz **ENTER**. Zobacz [odwołania do składni wyszukiwania w wykazie danych](https://msdn.microsoft.com/library/azure/mt267594.aspx) dla wszystkich hello właściwości można użyć do wyszukiwania hello wykazu danych.
3. Upewnij się, że widoczne wszystkie cztery tabele i hello bazy danych (AdventureWorks2014) w wynikach hello.  
   
    ![Usługa Data Catalog — wyniki wyszukiwania uzyskane z użyciem wyznaczania zakresu właściwości](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Zapisz wyszukiwanie hello
1. W hello **wyszukiwania** okienka w hello **bieżące wyszukiwanie** , wprowadź nazwę hello wyszukiwania i kliknij pozycję **zapisać**.
   
    ![Usługa Azure Data Catalog — zapisywanie wyszukiwania](media/data-catalog-get-started/data-catalog-save-search.png)
2. Upewnij się, że hello zapisane wyszukiwanie zostaną wyświetlone w obszarze **zapisane wyszukiwania**.
   
    ![Usługa Azure Data Catalog — zapisane wyszukiwania](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Wybierz jedną z akcji hello może przybrać hello zapisane wyszukiwania (**zmienić**, **usunąć**, **Zapisz jako domyślny** wyszukiwania).
   
    ![Usługa Azure Data Catalog — opcje dotyczące zapisanego wyszukiwania](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Operatory logiczne
Za pomocą operatorów logicznych można rozszerzyć lub zawęzić wyszukiwanie.

1. W polu wyszukiwania hello wpisz `tags:cycles AND objectType:table`i naciśnij klawisz **ENTER**.
2. Upewnij się, że jest wyświetlany tylko tabele (nie bazy danych hello) w wynikach hello.  
   
    ![Usługa Azure Data Catalog — zastosowanie operatora logicznego w wyszukiwaniu](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Grupowanie za pomocą nawiasów
Grupowania w nawiasach można grupować części hello zapytania tooachieve izolacji logicznej, szczególnie wraz z operatorów logicznych.

1. W polu wyszukiwania hello wpisz `name:product AND (tags:cycles AND objectType:table)` i naciśnij klawisz **ENTER**.
2. Upewnij się, że jest wyświetlany tylko hello **produktu** tabeli w wynikach wyszukiwania hello.
   
    ![Usługa Azure Data Catalog — wyszukiwanie przy użyciu grupowania](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Operatory porównania
Operatory porównania pozwalają używać innych porównań niż równość dla właściwości, które mają numeryczne i datowe typy danych.

1. W polu wyszukiwania hello wpisz `lastRegisteredTime:>"06/09/2016"`.
2. Wyczyść hello **tabeli** filtrować pod **typ obiektu**.
3. Naciśnij klawisz **ENTER**.
4. Upewnij się, że widoczny hello **produktu**, **ProductCategory**, **ProductDescription**, i **ProductPhoto** tabel i hello AdventureWorks2014 bazy danych, który został zarejestrowany w wynikach wyszukiwania.
   
    ![Usługa Azure Data Catalog — wyniki wyszukiwania z użyciem porównania](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Zobacz [jak zasobów danych toodiscover](data-catalog-how-to-discover.md) szczegółowe informacje dotyczące odnajdywania zasobów danych i [odwołania do składni wyszukiwania w wykazie danych](https://msdn.microsoft.com/library/azure/mt267594.aspx) składni wyszukiwania.

## <a name="annotate-data-assets"></a>Dodawanie adnotacji do zasobów danych
W tym ćwiczeniu używasz tooannotate portalu usługi Azure Data Catalog hello (Dodaj informacje, takie jak opisy, tagi lub ekspertów) zostały wcześniej zarejestrowane w wykazie hello zasobów danych. Adnotacje Hello uzupełnienie i zwiększyć hello metadane strukturalne wyodrębnione ze źródła danych hello podczas rejestracji i sprawia, że zasoby danych hello znacznie łatwiejsze toodiscover i zrozumieć.

W tym ćwiczeniu adnotacje zostaną dodane do pojedynczego zasobu danych (tabeli ProductPhoto). Możesz dodać przyjazną nazwę i opis toohello ProductPhoto danych zasobów.  

1. Przejdź toohello [strona główna usługi Azure Data Catalog](https://www.azuredatacatalog.com) i wyszukiwania z `tags:cycles` zasobów danych hello toofind został zarejestrowany.  
2. Kliknij pozycję **ProductPhoto** w wynikach wyszukiwania.  
3. Wprowadź **obrazy produktu** dla **przyjazną nazwę** i **zdjęć produktu na potrzeby materiałów marketingowych** dla hello **opis**.
   
    ![Usługa Azure Data Catalog — opis tabeli ProductPhoto](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Witaj **opis** ułatwia innym osobom odnajdywanie i zrozumienie, dlaczego i jak toouse hello wybranych zasobów danych. Możesz również dodać więcej tagów i wyświetlić kolumny. Teraz możesz spróbować wyszukiwania i filtrowania zasobów danych toodiscover przy użyciu metadanych opisowych hello dodano toohello katalogu.

Możesz również wykonać hello na tej stronie:

* Dodaj ekspertów hello danych zasobów. Kliknij przycisk **Dodaj** w hello **ekspertów** obszaru.
* Dodaj znaczniki na poziomie hello zestawu danych. Kliknij przycisk **Dodaj** w hello **tagi** obszaru. Możesz dodawać tagi użytkownika lub tagi słownika. Witaj Standard Edition usługi Data Catalog zawiera słownik biznesowy, które ułatwia administratorom wykazu Definiowanie centralnej taksonomii biznesowej. Użytkownicy wykazu mogą następnie dodać adnotacje do zasobów danych za pomocą terminów ze słownika. Aby uzyskać więcej informacji, zobacz [jak tooset się hello słownik biznesowy dla postanowieniom znakowanie](data-catalog-how-to-business-glossary.md)
* Dodaj znaczniki na poziomie kolumny hello. Kliknij przycisk **Dodaj** w obszarze **tagi** dla kolumny hello ma tooannotate.
* Dodaj opis na poziomie kolumny hello. W polu **Opis** wprowadź opis kolumny. Można również wyświetlić hello opis metadanych wyodrębnionych ze źródła danych hello.
* Dodaj **poprosić o dostęp** informacje, które zawiera użytkowników, jak toorequest uzyskują dostęp do zasobów danych toohello.
  
    ![Usługa Azure Data Catalog — dodawanie tagów, opisów](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Wybierz hello **dokumentacji** i podaj dokumentacji hello danych zasobów. W dokumentacji usługi Azure Data Catalog możesz użyć wykazu danych jako repozytorium zawartości toocreate pełną udostępniono elementów zawartości danych.
  
    ![Usługa Azure Data Catalog — karta Dokumentacja](media/data-catalog-get-started/data-catalog-documentation.png)

Można również dodać zasoby danych toomultiple adnotacji. Można na przykład zaznacz wszystkie zasoby danych hello zarejestrowanych i określ eksperta dla nich.

![Usługa Azure Data Catalog — dodawanie adnotacji do wielu zasobów danych](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Wykaz danych Azure obsługuje sourcing tłum tooannotations podejście. Każdy użytkownik wykazu danych można dodać tagów (użytkownik lub słownik), opisów i innych metadanych, dzięki czemu każdy użytkownik z perspektywą zasobu danych i jego użycia może mieć tej perspektywy przechwycony i tooother dostępnych użytkowników.

Zobacz [jak zasobów danych tooannotate](data-catalog-how-to-annotate.md) szczegółowe informacje dotyczące dodawania adnotacji zasobów danych.

## <a name="connect-toodata-assets"></a>Łączenie zasobów toodata
To ćwiczenie obejmuje otwieranie zasobów danych za pomocą zintegrowanego narzędzia klienckiego (programu Excel) oraz narzędzia niezintegrowanego (programu SQL Server Management Studio) przy użyciu informacji o połączeniu.

> [!NOTE]
> Jest ważne, tooremember, który Azure Data Catalog nie umożliwiają uzyskiwanie dostępu do źródła danych rzeczywistych toohello — po prostu ułatwia dla Ciebie toodiscover i go zrozumieć. Po ustanowieniu połączenia źródła danych tooa hello aplikacji klienckiej, wybrać używa poświadczeń systemu Windows, lub wyświetla monit o podanie poświadczeń w razie potrzeby. Jeśli użytkownik nie wcześniej przyznano źródła danych toohello dostępu, należy toobe prawa dostępu, zanim będzie można połączyć.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Połącz tooa zasobów danych z programu Excel
1. Wybierz pozycję **Product** w wynikach wyszukiwania. Kliknij przycisk **Otwórz w** na powitania narzędzi i kliknij przycisk **Excel**.
   
    ![Wykaz danych Azure — Połącz toodata zasobów](media/data-catalog-get-started/data-catalog-connect1.png)
2. Kliknij przycisk **Otwórz** w oknie podręcznym pobierania hello. To środowisko może się różnić w zależności od przeglądarki hello.
   
    ![Usługa Azure Data Catalog — pobrany plik połączenia programu Excel](media/data-catalog-get-started/data-catalog-download-open.png)
3. W hello **powiadomienie o zabezpieczeniach programu Microsoft Excel** okna, kliknij przycisk **włączyć**.
   
    ![Usługa Azure Data Catalog — okno podręczne zabezpieczeń programu Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Zachowaj domyślne hello w hello **i zaimportuj dane** okno dialogowe i kliknij przycisk **OK**.
   
    ![Usługa Azure Data Catalog — importowanie danych w programie Excel](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Widok źródła danych hello w programie Excel.
   
    ![Usługa Azure Data Catalog — tabela produktów w programie Excel](media/data-catalog-get-started/data-catalog-connect2.png)

W tym ćwiczeniu zostanie połączone zasoby toodata wykryte za pomocą usługi Azure Data Catalog. Portal Azure Data Catalog hello można połączyć za pomocą hello aplikacji klienckich zintegrowanych z hello **Otwórz w** menu. Możesz również połączyć z dowolnej aplikacji, wybierz za pomocą informacji o lokalizacji połączenia hello zawarte w metadanych zasobów hello. Na przykład umożliwia korzystanie hello zasobów danych zarejestrowany w tym samouczku SQL Server Management Studio tooconnect toohello AdventureWorks2014 bazy danych tooaccess hello danych.

1. Otwórz program **SQL Server Management Studio**.
2. W hello **połączyć tooServer** okna dialogowego wprowadź nazwę serwera hello z hello **właściwości** okienku w portalu Azure Data Catalog hello.
3. Użyj uwierzytelniania i poświadczeń tooaccess hello danych zasobów. Jeśli nie masz dostępu, użyj informacji w hello **żądania dostępu** tooget pola go.
   
    ![Usługa Azure Data Catalog — żądanie dostępu](media/data-catalog-get-started/data-catalog-request-access.png)

Kliknij przycisk **Wyświetl parametry połączenia** tooview i skopiuj ADF.NET, ODBC i OLEDB połączenie ciągów toohello Schowka do użycia w aplikacji.

## <a name="manage-data-assets"></a>Zarządzanie zasobami danych
W tym kroku, zobacz jak tooset zabezpieczenia trwałych danych. Wykaz danych nie zapewniają użytkownikom samych danych toohello dostępu. Właściciel Hello źródła danych hello kontroluje dostęp do danych.

Katalogu danych można używać źródeł danych toodiscover i tooview hello metadane powiązane źródła toohello zarejestrowane w wykazie hello. Mogą wystąpić sytuacje, jednak gdzie źródeł danych tylko powinna być widoczna toospecific użytkowników lub toomembers określonych grup. W tych sytuacjach można użyć własność tootake wykazu danych zarejestrowanych zasobów danych w katalogu hello i toothen kontroli hello widoczność zasobów hello, którego jesteś właścicielem.

> [!NOTE]
> możliwości zarządzania Hello opisane w tym ćwiczeniu są dostępne tylko w hello Standard Edition usługi Azure Data Catalog, nie znajduje się w hello bezpłatna wersja.
> W wykazie danych Azure możesz przejąć na własność zasobów danych, dodawać współwłaścicieli zasobów toodata i ustawić hello widoczność zasobów danych.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Przejmowanie własności do zasobów danych i ograniczanie ich widoczności
1. Przejdź toohello [strona główna usługi Azure Data Catalog](https://www.azuredatacatalog.com). W hello **wyszukiwania** tekst wprowadź `tags:cycles` i naciśnij klawisz **ENTER**.
2. Kliknij element na liście wyników hello, a następnie kliknij przycisk **Przejmij na własność** na powitania narzędzi.
3. W hello **zarządzania** sekcji hello **właściwości** panelu, kliknij przycisk **Przejmij na własność**.
   
    ![Usługa Azure Data Catalog — przejmowanie własności](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. widoczność toorestrict wybierz **właściciele i następujący użytkownicy** w hello **widoczność** sekcji, a następnie kliknij przycisk **Dodaj**. Wprowadź adresy e-mail użytkowników w polu tekstowym hello i naciśnij klawisz **ENTER**.
   
    ![Usługa Azure Data Catalog — ograniczanie dostępu](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Usuwanie zasobów danych
W tym ćwiczeniu zostanie hello Azure Data Catalog portalu tooremove Podgląd danych z zarejestrowanych zasobów danych i usunąć zasoby danych z katalogu hello.

W usłudze Azure Data Catalog można usuwać pojedyncze zasoby lub wiele zasobów.

1. Przejdź toohello [strona główna usługi Azure Data Catalog](https://www.azuredatacatalog.com).
2. W hello **wyszukiwania** tekst wprowadź `tags:cycles` i kliknij przycisk **ENTER**.
3. Wybierz element na liście wyników hello i kliknij przycisk **usunąć** na powitania narzędzi pokazane na powitania po obrazu:
   
    ![Usługa Azure Data Catalog — usuwanie elementu siatki](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Jeśli używasz widoku listy hello pole wyboru hello jest toohello lewej elementu hello pokazane na powitania po obrazu:
   
    ![Usługa Azure Data Catalog — usuwanie elementu listy](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    Można również wybrać wielu zasobów danych i usunąć je, jak pokazano w powitania po obrazu:
   
    ![Usługa Azure Data Catalog — usuwanie kilku zasobów danych](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> Witaj domyślne zachowanie katalogu hello jest tooallow any tooregister dowolnego użytkownika źródła danych i tooallow toodelete dowolnego użytkownika żadnych zasobów danych, który został zarejestrowany. możliwości zarządzania Hello objęte hello Standard Edition usługi Azure Data Catalog udostępniają dodatkowe opcje dla przejmowania własności zasobów, ograniczenie, którzy mogą odnajdować i ograniczenie, który można usunąć zasoby.
> 
> 

## <a name="summary"></a>Podsumowanie
W tym samouczku zostały przedstawione podstawowe funkcje usługi Azure Data Catalog, w tym rejestrowanie, dodawanie adnotacji, odnajdywanie i zarządzanie firmowymi zasobami danych. Teraz, po ukończeniu samouczka hello, nadszedł czas tooget uruchomiona. Możesz rozpocząć dzisiaj przez rejestrowanie źródeł danych hello przez Ciebie i Twojego zespołu zależne i zapraszania współpracowników toouse hello katalogu.

## <a name="references"></a>Dokumentacja
* [Jak tooregister zasobów danych](data-catalog-how-to-register.md)
* [Jak toodiscover zasobów danych](data-catalog-how-to-discover.md)
* [Jak tooannotate zasobów danych](data-catalog-how-to-annotate.md)
* [Jak toodocument zasobów danych](data-catalog-how-to-documentation.md)
* [Jak tooconnect toodata zasobów](data-catalog-how-to-connect.md)
* [Jak toomanage zasobów danych](data-catalog-how-to-manage.md)

