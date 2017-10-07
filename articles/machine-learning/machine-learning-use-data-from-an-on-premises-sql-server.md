---
title: "aaaUse lokalnego serwera SQL w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj danych z lokalnego serwera SQL bazy danych tooperform zaawansowane analizy przy użyciu usługi Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Wykonywanie zaawansowanych analiz za pomocą usługi Azure Machine Learning, używając danych z lokalnej bazy danych programu SQL Server

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Często w przypadku przedsiębiorstw, które współpracują z lokalnymi danymi chcieliby tootake zaletą skali hello oraz elastyczność hello chmury dla ich machine learning obciążeń. Ale nie mają toodisrupt bieżącego procesów biznesowych i przepływów pracy przez przeniesienie ich lokalnych danych toohello w chmurze. Usługa Azure Machine Learning obsługuje teraz odczytywanie danych z lokalną bazą danych programu SQL Server, a następnie celów szkoleniowych i oceniania modelu przy użyciu tych danych. Nie masz już toomanually kopiowania i synchronizacji danych hello między chmurą powitania serwera lokalnego. Zamiast tego hello **i zaimportuj dane** modułu w usłudze Azure Machine Learning Studio umożliwia teraz odczyt bezpośrednio z lokalną bazą danych programu SQL Server do szkolenia i oceniania zadania.

Ten artykuł zawiera omówienie sposobu tooingress lokalnych danych programu SQL server do usługi Azure Machine Learning. Przyjęto założenie, że znasz pojęcia dotyczące usługi Azure Machine Learning obszarów roboczych, modułów, zestawy danych, eksperymentów, *itp.*.

> [!NOTE]
> Ta funkcja nie jest dostępnych bezpłatnych obszarów roboczych. Aby uzyskać więcej informacji o cenach uczenia maszynowego i warstw, zobacz [Azure Machine Learning — cennik](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Zainstaluj hello brama zarządzania danymi firmy Microsoft
tooaccess lokalną bazą danych programu SQL Server w usłudze Azure Machine Learning, należy toodownload i zainstaluj hello brama zarządzania danymi firmy Microsoft. Po skonfigurowaniu połączenia bramy hello w usłudze Machine Learning Studio, masz możliwość hello pobieranie i instalowanie bramy hello przy użyciu hello **Pobierz i zarejestruj bramę danych** okna dialogowego opisanego poniżej.

Można też zainstalować hello brama zarządzania danymi wcześniejsze przez pobieranie i uruchamianie pakiet Instalatora MSI hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Wybierz hello najnowszą wersję, wybierając 32-bitowy lub 64-bitowych odpowiednie dla danego komputera. Witaj MSI może być również używane tooupgrade istniejącej bramy zarządzania danymi toohello najnowszej wersji, wszystkie ustawienia zachowane.

Brama Hello ma hello następujące wymagania wstępne:

* wersje systemu operacyjnego Windows Hello obsługiwane są systemu Windows 7, Windows 8/8.1, Windows 10, systemu Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2.
* Hello zaleca się, że konfiguracja maszyny bramy hello jest co najmniej 2 GHz 4 rdzenie, 8 GB pamięci RAM i dysk 80 GB.
* Hibernacja hello komputer hosta, nie będzie reagować żądań toodata hello bramy. W związku z tym skonfigurować przed zainstalowaniem bramy hello planu zasilania odpowiednie hello komputera. Jeśli maszyna hello jest skonfigurowany toohibernate, instalacja bramy hello wyświetla komunikat.
* Ponieważ działanie kopiowania odbywa się na określonej częstotliwości, hello użycia zasobów (procesora CPU, pamięci) na maszynie hello następuje także hello sam wzorca z szczytowe i czas bezczynności. Wykorzystanie zasobów zależy również od silnie hello ilość danych, jest przenoszony. W przypadku wielu kopii zadania w toku, widoczny użycia zasobów, do góry w godzinach szczytu. Technicznie wystarcza hello minimalnej konfiguracji wymienione powyżej, może okazać toohave konfiguracji więcej zasobów niż hello minimalnej konfiguracji w zależności od określonego obciążenia dla ruchu danych.

Należy wziąć pod uwagę następujące hello podczas konfigurowania i korzystania z bramy zarządzania danymi:

* Na jednym komputerze można zainstalować tylko jedno wystąpienie bramy zarządzania danymi.
* Pojedyncza brama służy do lokalnego źródła danych.
* Możesz połączyć wiele bram na różnych komputerach toohello tego samego źródła danych lokalnych.
* W czasie konfigurowania bramy dla tylko jednego obszaru roboczego. Obecnie Usługa bramy nie można udostępniać między obszarów roboczych.
* Istnieje możliwość skonfigurowania wielu bram dla jednego obszaru roboczego. Na przykład może być toouse bramy, która jest tooyour połączonych źródeł danych testu podczas tworzenia i bramy produkcji, gdy wszystko jest gotowe toooperationalize.
* Brama Hello toobe na powitania sam komputer jako źródło danych hello nie jest konieczne. Ale pozostaje bliżej toohello źródła danych przyspiesza hello dla źródła danych toohello tooconnect bramy hello. Zalecamy zainstalowanie bramy hello na maszynie, która różni się od hello jednego źródła danych lokalne powitania hostów, dzięki czemu hello bramy i źródła danych nie konkurują o zasoby.
* Jeśli masz już bramy zainstalowanej na komputerze, obsługująca scenariusze usługi Power BI lub fabryki danych Azure, należy zainstalować oddzielnej bramy dla usługi Azure Machine Learning na innym komputerze.

  > [!NOTE]
  > Nie można uruchomić bramy zarządzania danymi i bramy usługi Power BI na powitania tym samym komputerze.
  >
  >
* Należy hello toouse brama zarządzania danymi dla usługi Azure Machine Learning, nawet jeśli używana jest usługa Azure ExpressRoute innych danych. Źródło danych należy traktować jako źródło danych lokalnych (który znajduje się za zaporą) nawet jeśli używasz usługi ExpressRoute. Użyj hello brama zarządzania danymi tooestablish łączność między uczenia maszynowego i hello źródła danych.

Szczegółowe informacje dotyczące wymagań wstępnych instalacji, kroki instalacji i wskazówki dotyczące rozwiązywania problemów można znaleźć w artykule hello [brama zarządzania danymi](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Transfer danych przychodzących danych z lokalnej bazy danych programu SQL Server do usługi Azure Machine Learning
W tym przewodniku będzie skonfigurować bramę zarządzania danymi w obszarze roboczym usługi Azure Machine Learning, jest skonfigurowana, a następnie przeczytaj danych z lokalną bazą danych programu SQL Server.

> [!TIP]
> Przed rozpoczęciem należy wyłączyć blokowanie wyskakujących okienek w przeglądarce dla `studio.azureml.net`. Jeśli używasz przeglądarki Google Chrome hello, Pobierz i zainstaluj jedną hello kilku dostępnych wtyczek w witrynie Google Chrome WebStore [kliknij raz rozszerzenia aplikacji](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Krok 1: Tworzenie bramy
pierwszym krokiem Hello jest toocreate i skonfigurować hello tooaccess bramę lokalną bazą danych SQL.

1. Zaloguj się za[Azure Machine Learning Studio](https://studio.azureml.net/Home/) i hello wybierz obszar roboczy, który ma być toowork.
2. Kliknij przycisk hello **ustawienia** bloku na powitania po lewej, a następnie kliknij przycisk hello **BRAM danych** u góry hello.
3. Kliknij przycisk **nowej bramy danych** u dołu hello hello ekranu.

    ![Nowej bramy danych](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. W hello **nowej bramy danych** okna dialogowego, wprowadź hello **nazwa bramy** i opcjonalnie Dodaj **opis**. Kliknij strzałkę hello na powitania dolnej prawym rogu toogo toohello następnego kroku hello konfiguracji.

    ![Wprowadź nazwę bramy i opis](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. W hello Pobierz i zarejestruj dialogowe bramy danych, Kopiuj hello klucz rejestracji bramy toohello Schowka.

    ![Pobierz i zarejestruj bramę danych](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Jeśli jeszcze nie zostały pobrane i zainstalowane hello brama zarządzania danymi firmy Microsoft, a następnie kliknij przycisk **brama zarządzania danymi pobierania**. Ta ma toothe Microsoft Download Center którym można wybrać wersję bramy hello możesz konieczne, go pobrać i zainstalować ją. Szczegółowe informacje dotyczące wymagań wstępnych instalacji, kroki instalacji i wskazówki dotyczące rozwiązywania problemów można znaleźć w sekcjach początku hello artykułu hello [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Po zainstalowaniu bramy hello hello Menedżera konfiguracji bramy zarządzania danymi będą otwierane i hello **bramy rejestru** zostanie wyświetlone okno dialogowe. Wklej hello **klucz rejestracji bramy** skopiowany toohello Schowka i kliknij przycisk **zarejestrować**.
8. Jeśli masz już zainstalowana brama, uruchom hello Menedżera konfiguracji bramy zarządzania danymi. Kliknij przycisk **Zmień klucz**, Wklej **klucz rejestracji bramy** skopiowane Schowka toohello hello w poprzednim kroku, a następnie kliknij polecenie **OK**.
9. Po zakończeniu instalacji hello hello **bramy rejestru** zostanie wyświetlone okno dialogowe dla Microsoft danych Menedżera konfiguracji bramy zarządzania. Wklej hello klucz rejestracji bramy, który został skopiowany do Schowka hello w poprzednim kroku, a następnie kliknij przycisk **zarejestrować**.

    ![Zarejestruj bramę](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Witaj konfiguracji bramy została ukończona, gdy hello następujące wartości są ustawiane na powitania **Home** kartę w Microsoft danych Menedżera konfiguracji bramy zarządzania:

    * **Nazwa bramy** i **nazwa wystąpienia** są ustawione toohello nazwy hello bramy.
    * **Rejestracja** ustawiono zbyt**zarejestrowanej**.
    * **Stan** ustawiono zbyt**uruchomiono**.
    * pasek stanu Hello na powitania dolnej Wyświetla **połączone tooData usługi bramy zarządzania w chmurze** wraz z zielonym znacznikiem wyboru.

      ![Menedżer bramy zarządzania danymi](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio również aktualizowany po pomyślnej rejestracji hello.

    ![Rejestracja bramy powiodło się](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. W hello **Pobierz i zarejestruj bramę danych** okna dialogowego, kliknij przycisk Ustawienia hello toocomplete znacznik wyboru. Witaj **ustawienia** strona wyświetla stan bramy jako "W trybie Online". W okienku po prawej stronie powitania, stanu i znajdziesz inne przydatne informacje.

    ![Ustawienia bramy](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. W hello Menedżera konfiguracji bramy zarządzania danymi firmy Microsoft przełącznika toohello **certyfikatu** certyfikat hello kartę określone na tej karcie jest używana tooencrypt/odszyfrowywania poświadczenia dla magazynu danych lokalne powitania wskazanym w portalu hello. Ten certyfikat jest hello domyślnego certyfikatu. Firma Microsoft zaleca zmianę tego tooyour własny certyfikat kopii zapasowej w systemie zarządzania certyfikatu. Kliknij przycisk **zmiany** toouse własnego certyfikatu zamiast tego.

    ![Certyfikat bramy zmiany](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (opcjonalnie) Tooenable pełne rejestrowanie, aby rozwiązać problemy z hello bramy, w hello Menedżera konfiguracji bramy zarządzania danymi firmy Microsoft przejść toothe **diagnostyki** i sprawdź hello **włączyć pełne rejestrowanie na potrzeby rozwiązywania problemów** opcji. Witaj rejestrowanie informacji można znaleźć w hello Podgląd zdarzeń systemu Windows w obszarze hello **Dzienniki aplikacji i usług**  - &gt; **brama zarządzania danymi** węzła. Można również użyć hello **diagnostyki** kartę tootest hello połączenia tooan lokalnego źródła danych przy użyciu bramy hello.

    ![Włącz pełne rejestrowanie](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Na tym kończy proces instalacji bramy hello w usłudze Azure Machine Learning.
Użytkownik jest teraz gotowy toouse danych lokalnych.

Można utworzyć i skonfigurować wiele bram w Studio dla każdego obszaru roboczego. Na przykład może być bramy ma źródeł danych testowych tooyour tooconnect podczas projektowania i brama różnych źródeł danych produkcyjnych. Usługa Azure Machine Learning zapewnia tooset elastyczność się wiele bram, w zależności od środowiska firmy. Obecnie nie można udostępnić bramy między obszarami roboczymi i na jednym komputerze można zainstalować tylko jedną bramę. Aby uzyskać więcej informacji, zobacz [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Krok 2: Użyj hello bramy tooread danych z lokalnego źródła danych
Po skonfigurowaniu bramy hello można dodać **i zaimportuj dane** modułu do eksperymentu danych wejściowych hello danych z bazy danych programu SQL Server lokalne powitania.

1. W usłudze Machine Learning Studio, wybierz hello **EKSPERYMENTY** , kliknij pozycję **+ nowy** w hello lewym dolnym rogu i wybierz **pusty eksperyment** (lub wybierz jeden z kilku próbki eksperymenty dostępna).
2. Znajdź i przeciągnij hello **i zaimportuj dane** kanwy eksperymentu toohello modułu.
3. Kliknij przycisk **Zapisz jako** poniżej hello kanwy. Wprowadź nazwę eksperymentu hello "Azure lokalnego programu SQL Server samouczek dotyczący uczenia maszynowego", wybierz obszar roboczy, a następnie kliknij przycisk hello **OK** znacznik wyboru.

   ![Zapisz doświadczenia z nową nazwą](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Kliknij przycisk hello **Importuj dane** tooselect modułu, a następnie w **właściwości** toohello okienko rogu hello kanwy, wybierz "Lokalną bazą danych SQL" hello **źródła danych** Lista rozwijana.
5. Wybierz hello **bramy danych** zainstalowany i zarejestrowany. Można skonfigurować inną bramę, wybierając opcję "(Dodaj nową bramę danych...)".

   ![Wybierz bramę danych dla modułu importowanie danych](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Wprowadź hello SQL **nazwę serwera bazy danych** i **Nazwa bazy danych**, wraz z hello SQL **zapytanie bazy danych** ma tooexecute.
7. Kliknij przycisk **wprowadź wartości** w obszarze **nazwy użytkownika i hasła** i wprowadź swoje poświadczenia bazy danych. Umożliwia zintegrowane uwierzytelnianie systemu Windows lub uwierzytelniania programu SQL Server, w zależności od konfiguracji serwera SQL lokalnie.

   ![Wprowadź poświadczenia bazy danych](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   wiadomość Hello zmiany "wymaganych wartości" za "wartości zestaw" z zielonym znacznikiem wyboru. Wystarczy tooenter hello poświadczenia raz chyba, że zmiany hello bazy danych lub hasła. Usługa Azure Machine Learning certyfikatem hello podane podczas instalacji hello bramy tooencrypt hello poświadczeń w chmurze hello. Azure nigdy nie przechowuje poświadczeń lokalnych bez szyfrowania.

   ![Importowanie właściwości modułu danych](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Kliknij przycisk **Uruchom** toorun hello eksperymentu.

Po zakończeniu eksperymentu hello można zwizualizować dane hello zaimportowane z bazy danych hello klikając portem wyjściowym hello hello **i zaimportuj dane** modułu i wybierając **Visualize**.

Po zakończeniu tworzenia eksperymentu można wdrażać i operacjonalizować model. Przy użyciu hello usługi wykonywania wsadowego, dane z hello: lokalną bazą danych programu SQL Server skonfigurowanych w hello **i zaimportuj dane** modułu zostanie odczytu i będzie używana do oceniania. Za pomocą hello usługę odpowiedzi na żądanie dla oceniania danych lokalnych, firma Microsoft zaleca używanie [dodatek programu Excel](machine-learning-excel-add-in-for-web-services.md) zamiast tego. Obecnie zapisywania tooan lokalnej bazy danych programu SQL Server za pośrednictwem **eksportowanie danych** nie jest obsługiwane zarówno w eksperymentów lub opublikowane w sieci web usługi.
