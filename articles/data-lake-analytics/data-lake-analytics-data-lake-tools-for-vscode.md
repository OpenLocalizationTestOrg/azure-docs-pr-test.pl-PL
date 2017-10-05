---
title: "Usługi Azure Data Lake Tools: Użycia usługi Azure Data Lake Tools dla programu Visual Studio Code | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure Data Lake Tools dla Visual Studio Code umożliwia tworzenie, testowanie i uruchamianie skryptów U-SQL. "
Keywords: "VScode, usługi Azure Data Lake Tools, uruchamiania lokalnego debugowania, debugowania lokalnego pliku magazynu w wersji zapoznawczej, lokalnego przekazać do ścieżki do magazynu"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Użyj usługi Azure Data Lake Tools dla programu Visual Studio Code

Dowiedz się, jak używać usługi Azure Data Lake Tools dla programu Visual Studio (kod VS) do tworzenia, testowania i uruchamiać skrypty U-SQL. Informacje są także omówione w poniższym klipie wideo:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Wymagania wstępne

Narzędzia Data Lake Tools można zainstalować na platformach obsługiwanych przez kod programu VS. Obsługiwane platformy to Windows, Linux lub MacOS. Różnych platform zostały spełnione następujące wymagania wstępne:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Dodaj ścieżkę java.exe ścieżki zmiennej środowiskowej systemu. Instrukcje konfiguracji można znaleźć [jak ustawić lub zmienić zmiennej systemowej Path?]( https://www.java.com/download/help/path.xml). Ścieżka jest podobny do C:\Program Files\Java\jdk1.8.0_77\jre\bin.
    - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (zalecamy Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). Aby zainstalować kod, wprowadź następujące polecenie:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - Aby zaktualizować źródła pakietu deb, wprowadź następujące polecenia:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - Aby zainstalować Mono, wprowadź następujące polecenie:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 nie jest obsługiwane. Całkowicie przed zainstalowaniem 4.2.x, należy odinstalować wersję 4.6.  

        - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Aby uzyskać instrukcje instalacji, zobacz [Linux 64-bitowe instrukcje instalacji Java]( https://java.com/en/download/help/linux_x64_install.xml) strony.
        - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Aby uzyskać instrukcje instalacji, zobacz [Linux 64-bitowe instrukcje instalacji Java](https://java.com/en/download/help/mac_install.xml) strony.
    - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Instalowania narzędzi Data Lake Tools

Po zainstalowaniu wymagań wstępnych, można zainstalować narzędzi Data Lake Tools dla programu VS kodu.

**Aby zainstalować narzędzia Data Lake Tools**

1. Otwórz kod programu Visual Studio.
2. Wybierz kombinację klawiszy Ctrl + P, a następnie wprowadź następujące polecenie:
```
ext install usql-vscode-ext
```
Można wyświetlić listę rozszerzeń kodu programu Visual Studio. Jeden z nich jest **Azure Data Lake Tools**.

3. Wybierz **zainstalować** obok **Azure Data Lake Tools**. Po kilku sekundach **zainstalować** przycisku zmienia się na **Załaduj ponownie**.
4. Wybierz **Załaduj ponownie** aktywować rozszerzenia.
5. Wybierz **OK** o potwierdzenie. Widać Azure Data Lake Tools w **rozszerzenia** okienka.
    ![Narzędzia Data Lake Tools dla okienka rozszerzenia kodu programu Visual Studio](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Aktywacja usługi Azure Data Lake Tools
Utwórz nowy plik .usql lub Otwórz istniejący plik .usql aktywować rozszerzenia. 

## <a name="connect-to-azure"></a>Nawiązywanie połączenia z usługą Azure

Można było skompilować i uruchomić skrypty U-SQL w usługi Data Lake Analytics, należy połączyć z kontem platformy Azure.

**Do nawiązania połączenia platformy Azure**

1.  Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia. 
2.  Wprowadź **ADL: logowania**. Informacje logowania są wyświetlane w **dane wyjściowe** okienka.

    ![Data Lake Tools dla Visual Studio Code polecenia palety](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![narzędzi Data Lake Tools dla Visual Studio Code informacji o logowaniu urządzenia](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Wybierz kombinację klawiszy Ctrl + kliknięcie na adres URL logowania: https://aka.ms/devicelogin aby otworzyć stronę logowania w sieci Web. Wprowadź kod **G567LX42V** w polu tekstowym, a następnie wybierz **Kontynuuj**.

   ![Narzędzia Data Lake Tools dla Visual Studio Code logowania Wklej kod](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Postępuj zgodnie z instrukcjami, aby zalogować się w stronę sieci Web. Po nawiązaniu połączenia nazwa konta platformy Azure jest wyświetlana na pasku stanu, w lewym dolnym rogu **kodzie VS** okna. 

    > [!NOTE] 
    > Jeśli konto ma dwa składniki włączone, zalecane jest użycie z telefonu uwierzytelniania, a nie za pomocą numeru PIN.

Aby się wylogować, wprowadź polecenie **ADL: wylogowania**.

## <a name="list-your-data-lake-analytics-accounts"></a>Lista kont usługi Data Lake Analytics

Aby przetestować połączenie, wyświetlenie listy kont usługi Data Lake Analytics.

**Aby wyświetlić listę kont usługi Data Lake Analytics w ramach Twojej subskrypcji platformy Azure**

1. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.
2. Wprowadź **ADL: listy kont**. Konta są wyświetlane w **dane wyjściowe** okienka.

## <a name="open-the-sample-script"></a>Otwórz przykładowy skrypt
Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: Otwórz przykładowy skrypt**. Zostanie otwarte inne wystąpienie tego przykładu. Można również edytować, skonfigurować i przesłać skrypt w tym wystąpieniu.

## <a name="work-with-u-sql"></a>Praca z języka U-SQL

Należy otworzyć plik U-SQL lub folder do pracy w języku U-SQL.

**Aby otworzyć folder projektu U-SQL**

1. W programie Visual Studio Code, wybierz **pliku** menu, a następnie wybierz **Otwórz Folder**.
2. Określ folder, a następnie wybierz **wybierz Folder**.
3. Wybierz **pliku** menu, a następnie wybierz **nowy**. Plik 1 bez tytułu zostanie dodany do projektu.
4. Wprowadź następujący kod do pliku bez tytułu 1:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    Skrypt tworzy plik departments.csv z niektóre dane zawarte w folderze/Output.

5. Zapisz plik jako **myUSQL.usql** w otwartym folderze. Plik konfiguracji adltools_settings.json jest także dodawane do projektu.
4. Otwórz i skonfiguruj adltools_settings.json z następującymi właściwościami:

    - Konto: Konta Data Lake Analytics w ramach Twojej subskrypcji platformy Azure.
    - Baza danych: Baza danych przy użyciu tego konta. Wartość domyślna to **wzorca**.
    - Schemat: Schemat w bazie danych. Wartość domyślna to **dbo**.
    - Ustawienia opcjonalne:
        - Priorytet: Zakres priorytetu jest z zakresu od 1 do 1000 z 1 oznacza najwyższy priorytet. Wartość domyślna to **1000**.
        - Równoległość: Zakres równoległości jest z zakresu od 1 do 150. Wartość domyślna to równoległości maksymalny dozwolony na koncie usługi Azure Data Lake Analytics. 
        
        > [!NOTE] 
        > Jeśli te ustawienia są nieprawidłowe, zostaną użyte wartości domyślne.

    ![Narzędzia Data Lake Tools dla Visual Studio Code pliku konfiguracji](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Obliczeniowe konta usługi Data Lake Analytics jest potrzebny do kompilowanie i uruchamianie zadań U-SQL. Aby można było skompilować i uruchamianie zadań U-SQL, należy skonfigurować konto komputera.
    
Po zapisaniu konfiguracji informacje konta, bazy danych i schematu są wyświetlane na pasku stanu, w lewym dolnym rogu odpowiedni plik .usql. 
 
 
W porównaniu do otwierania pliku, po otwarciu folderu, które można wykonywać następujące czynności:

- Użyj pliku CodeBehind. W trybie pojedynczego pliku CodeBehind nie jest obsługiwane.
- Przy użyciu pliku konfiguracji. Po otwarciu folderu skryptów w folderze roboczym udostępniać pojedynczym pliku konfiguracji.


Skrypt U-SQL kompiluje zdalnie za pomocą usługi Data Lake Analytics. Podczas wystawiania **skompilować** polecenia skryptu U-SQL jest wysyłany do swojego konta usługi Data Lake Analytics. Później Visual Studio Code odbiera wynik kompilacji. Z powodu zdalnej kompilacji programu Visual Studio Code wymaga, wyświetlić listę informacji do łączenia się z kontem usługi Data Lake Analytics w pliku konfiguracji.

**Do kompilowania skryptu U-SQL**

1. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia. 
2. Wprowadź **ADL: kompilowania skryptu**. Zostaną wyświetlone wyniki kompilacji w **dane wyjściowe** okna. Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: kompilowania skryptu** skompilować zadań U-SQL. Wynik kompilacji jest wyświetlana w **dane wyjściowe** okienka.
 

**Aby przesłać skrypt U-SQL**

1. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia. 
2. Wprowadź **ADL: przesłać zadania**.  Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: Prześlij zadanie**. 

Po przesłaniu zadania skryptu U-SQL w dziennikach przesyłania są wyświetlane w **dane wyjściowe** okna w kodzie VS. Jeśli przesyłanie zakończy się pomyślnie, zadanie adres URL pojawia się również. Adres URL zadania można otworzyć w przeglądarce sieci web, aby śledzić stan zadania w czasie rzeczywistym.

Aby włączyć danych wyjściowych szczegóły zadania, ustaw **jobInformationOutputPath** w **vs kod u sql_settings.json** pliku.
 
## <a name="use-a-code-behind-file"></a>Przy użyciu pliku CodeBehind

Plik CodeBehind jest pliku C# skojarzonego z jednego skryptu U-SQL. Skrypt dedykowanych można zdefiniować UDO UDA, UDT i funkcji zdefiniowanej przez użytkownika w pliku CodeBehind. UDO, UDA, UDT i UDF można bezpośrednio w skrypcie bez rejestrowania najpierw zestaw. Plik CodeBehind jest umieszczany w tym samym folderze co jego komunikacji równorzędnej pliku skryptu U-SQL. Jeśli skrypt ma nazwę xxx.usql, jako xxx.usql.cs nosi nazwę CodeBehind. Jeśli ręcznie usuń plik CodeBehind, funkcja CodeBehind jest wyłączona dla jego skojarzony skrypt U-SQL. Aby uzyskać więcej informacji na temat pisania kodu klienta dla skryptu U-SQL, zobacz [pisania i przy użyciu niestandardowego kodu w języku U-SQL: funkcje zdefiniowane przez użytkownika]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

Aby obsługiwać związane z kodem, możesz otworzyć folderu roboczego. 

**Aby wygenerować plik CodeBehind**

1. Otwórz plik źródłowy. 
2. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.
3. Wprowadź **ADL: generowanie kodu**. Plik CodeBehind jest tworzony w tym samym folderze. 

Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: generowanie kodu za**. 

Aby skompilować i przesłać skrypt U-SQL przy użyciu pliku CodeBehind jest taka sama jak z autonomicznego pliku skryptu U-SQL.

Dwa poniższe zrzuty ekranu pokazują plik CodeBehind i jego skojarzony plik skryptu U-SQL:
 
![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Plik skryptu narzędzi Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Korzystanie z zestawów

Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).

Data Lake Tools służy do rejestrowania zestawów niestandardowych kodów w katalogu Data Lake Analytics.

**Można zarejestrować zestawu**

Można zarejestrować zestawu za pomocą **ADL: Zarejestruj zestawu** lub **ADL: Zarejestruj zestawu za pomocą konfiguracji** poleceń.

**Aby zarejestrować za pomocą ADL: polecenie zarejestrować zestawu**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.
2.  Wprowadź **ADL: zarejestrować zestawu**. 
3.  Określ ścieżkę zestawu lokalnego. 
4.  Wybierz konto usługi Data Lake Analytics.
5.  Wybierz bazę danych.

Wyniki: Portal jest otwarty w przeglądarce i przedstawia proces rejestracji zestawu.  

Inny wygodny sposób, aby wyzwolić **ADL: Zarejestruj zestawu** polecenie jest kliknij prawym przyciskiem myszy plik .dll w Eksploratorze plików. 

**Aby zarejestrować jednak ADL: Zarejestruj zestawu za pomocą polecenia konfiguracji**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.
2.  Wprowadź **ADL: zarejestrować zestawu za pomocą konfiguracji**. 
3.  Określ ścieżkę zestawu lokalnego. 
4.  Plik JSON jest wyświetlany. Przejrzyj i Edytuj zależności zestawu i parametry zasobu, jeśli to konieczne. Instrukcje są wyświetlane w **dane wyjściowe** okna. Aby przejść do rejestrowania zestawów, Zapisz (Ctrl + S) w pliku JSON.

![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Zależności zestawu: automatycznie wykrywa Azure Data Lake Tools Określa, czy biblioteka DLL nie ma żadnych zależności. Zależności są wyświetlane w pliku JSON, po ich wykryciu. 
>- Zasoby: Można przekazać biblioteki DLL zasobów (na przykład txt, .png i .csv) jako część zestawu rejestracji. 

Innym sposobem wyzwolenia **ADL: Zarejestruj zestawu za pomocą konfiguracji** polecenie jest kliknij prawym przyciskiem myszy plik .dll w Eksploratorze plików. 

Poniższy kod języka U-SQL przedstawia sposób wywołania zestawu. W przykładzie nazwa zestawu jest *testu*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a>Dostęp do katalogu Data Lake Analytics

Po podłączeniu do platformy Azure, służy następujące kroki, aby uzyskać dostęp do katalogu U-SQL.

**Aby uzyskać dostępu do metadanych usługi Azure Data Lake Analytics**

1.  Wybierz kombinację klawiszy Ctrl + Shift + P, a następnie wprowadź **ADL: listy tabel**.
2.  Wybierz jedno z kont usługi Data Lake Analytics.
3.  Wybierz jedną z bazy danych usługi Data Lake Analytics.
4.  Wybierz jeden ze schematów. Można wyświetlić listę tabel.

## <a name="view-data-lake-analytics-jobs"></a>Widok Data Lake Analytics zadania

**Aby wyświetlić zadania usługi Data Lake Analytics**
1.  Otwórz palety polecenia (Ctrl + Shift + P) i wybierz **ADL: Pokaż zadania**. 
2.  Wybierz usługi Data Lake Analytics lub konta lokalnego. 
3.  Poczekaj na liście zadania konta są wyświetlane.
4.  Wybierz zadanie z listy zadań, narzędzi Data Lake Tools Otwiera szczegóły zadania w portalu Azure i plik informacji o zadaniu jest wyświetlany w kodzie VS.

![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Integracja magazynu usługi Azure Data Lake

Można użyć poleceń usługi Azure Data Lake Storage, aby:
 - Przeglądaj zasoby usługi Azure Data Lake Storage. 
 - Wyświetl podgląd pliku usługi Azure Data Lake Storage.  
 - Przekaż plik bezpośrednio do usługi Azure Data Lake Storage w kodzie VS. 

### <a name="list-the-storage-path"></a>Lista ścieżki do magazynu 
Można wyświetlić listę ścieżki do magazynu za pośrednictwem palety polecenia lub kliknij prawym przyciskiem myszy.

**Aby wyświetlić listę ścieżki magazynu za pomocą polecenia palety**

1.  Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: ścieżka magazynu listy**.

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Wybierz użytkownika preferowany sposób wyświetlania list ścieżki do magazynu. Używa tego przejścia **wprowadź ścieżkę** jako przykład.

    ![Narzędzia Data Lake Tools dla Visual Studio Code jednym ze sposobów listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS kod chroni odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics. Na przykład: ss tt /.
    >- Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    >- Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    
3. Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz więcej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Wybierz **więcej** listy więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Wprowadź ścieżkę do magazynu Azure. Na przykład/output.

    ![Narzędzia Data Lake Tools dla Visual Studio Code Wprowadź ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Wyniki: Palety polecenie wyświetla informacje o ścieżce na podstawie wpisów.

    ![Narzędzia Data Lake Tools dla Visual Studio Code lista wyników ścieżki magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Bardziej wygodne ścieżka względna jest za pośrednictwem menu kontekstowym kliknij prawym przyciskiem myszy.

**Aby wyświetlić listę ścieżki magazynu za pośrednictwem kliknij prawym przyciskiem myszy**

1.  Kliknij prawym przyciskiem myszy ciąg ścieżki, aby wybrać **ścieżki do magazynu listy**.

       ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Wybrana ścieżka względna zostanie wyświetlony w palecie polecenia.

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybrane ścieżki względnej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Wyniki: Palety polecenie wyświetla listę folderów i plików dla bieżącej ścieżki.

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy z bieżącej ścieżki](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a>Podgląd pliku magazynu
Można wyświetlić podgląd pliku magazynu za pośrednictwem palety polecenia lub kliknij prawym przyciskiem myszy.

**Aby wyświetlić podgląd pliku magazynu za pomocą polecenia palety**

1.  Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: Podgląd pliku magazynu**.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wyświetlić podgląd pliku magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy kont](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Wybierz **więcej** listy więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Wprowadź ścieżkę do magazynu Azure lub pliku. Na przykład /output/SearchLog.txt.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę do magazynu i](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Wyniki: Palety polecenie wyświetla informacje o ścieżce na podstawie wpisów.

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Aby wyświetlić listę ścieżki magazynu za pośrednictwem kliknij prawym przyciskiem myszy**

1.  Aby wyświetlić podgląd pliku, kliknij prawym przyciskiem myszy ścieżkę pliku.

   ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Wyniki: Kod VS wyświetla wyniki podglądu pliku.

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Przekazywanie pliku 

Możesz przekazać pliki, wprowadzając polecenia **ADL: Przekaż plik** lub **ADL: Przekaż plik przy użyciu konfiguracji**.

**Aby przekazać pliki jednak ADL: Przekaż plik — polecenie**
1. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia lub kliknij prawym przyciskiem myszy edytora skryptów, a następnie wprowadź **Przekaż plik**.
2.  Można przekazać pliku, wprowadź ścieżkę lokalną.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę lokalną](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Wybierz jeden ze sposobów wyświetlania ścieżki do magazynu. Używa tego przejścia **wprowadź ścieżkę** jako przykład.

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS kod chroni odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics. Na przykład: ss tt /.
    >- Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    >- Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.

4. Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code magazynu, kliknij prawym przyciskiem myszy](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Wprowadź ścieżkę do magazynu Azure. Na przykład: / output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Znajdź ścieżki magazynu Azure. Wybierz **Wybierz bieżący folder**.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz folder](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Wyniki: **dane wyjściowe** okno wyświetla stan przekazywania plików.

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**Aby przekazać pliki jednak ADL: Przekaż plik za pomocą polecenia konfiguracji**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia lub kliknij prawym przyciskiem myszy edytora skryptów, a następnie wprowadź **Przekaż plik przy użyciu konfiguracji**.
2.  VS kod przedstawia plik JSON. Można wprowadzić ścieżki do plików i przekazywania wielu plików jednocześnie. Instrukcje są wyświetlane w **dane wyjściowe** okna. Aby kontynuować, można przekazać pliku, Zapisz (Ctrl + S) w pliku JSON.

       ![Ścieżka pliku narzędzia Data Lake Tools dla Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Wyniki: **dane wyjściowe** okno wyświetla stan przekazywania plików.

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Innym sposobem przekazania pliku do magazynu jest za pomocą menu kliknij prawym przyciskiem myszy na pełną ścieżkę pliku lub ścieżki względnej pliku w Edytorze skryptów. Wprowadź ścieżkę do pliku lokalnego, a następnie wybierz konto. **Dane wyjściowe** okno wyświetla stan przekazywania. 

### <a name="open-azure-storage-explorer"></a>Eksplorator usługi Storage Azure Otwórz
Możesz otworzyć **Eksploratora usługi Storage Azure** przez wprowadzenie polecenia **ADL: Otwórz Eksploratora usługi sieci Web Azure Storage** lub wybierając z menu kontekstowego kliknij prawym przyciskiem myszy.

**Aby otworzyć Eksploratora usługi Storage platformy Azure**

1. Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.
2. Wprowadź **Otwórz Eksploratora usługi Storage Azure Web** lub kliknij prawym przyciskiem myszy na ścieżkę względną lub pełną ścieżkę w Edytorze skryptów, a następnie wybierz **Otwórz Eksploratora usługi Storage Azure Web**.
3. Wybierz konto usługi Data Lake Analytics.

Narzędzia Data Lake Tools otwiera ścieżki do magazynu Azure w portalu Azure. Można znaleźć ścieżki i wyświetlić podgląd pliku z sieci web.

### <a name="local-run-and-local-debug-for-windows-users"></a>Przebieg lokalny i lokalny debugowania dla systemu Windows użytkownicy
Uruchamiania lokalnego skryptu U-SQL sprawdza danych lokalnych i sprawdza poprawność skrypt lokalnie, przed opublikowaniem kodu do usługi Data Lake Analytics. Funkcja debugowania lokalnego umożliwia wykonywanie następujących zadań przed przesłaniem do usługi Data Lake Analytics kodu: 
- Debugowanie programu C# związane z kodem. 
- Kroków opisanych w kodzie. 
- Sprawdź poprawność skrypt lokalnie.

Aby uzyskać instrukcje dotyczące przebiegu lokalnego i debugowania lokalnego, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Dodatkowe funkcje

Narzędzia Data Lake Tools dla programu VS kodu obsługuje następujące funkcje:

-   Funkcja automatycznego uzupełniania IntelliSense: sugestie są wyświetlane w wyskakujące wokół elementów, takich jak słowa kluczowe, metod i zmiennych. Inne ikony reprezentują różnych typów obiektów:

    - Scala — typ danych
    - Typ danych złożonych
    - Wbudowanych typów
    - Klasy i kolekcji .NET
    - Wyrażenia języka C#
    - Funkcje UDF wbudowane C#, obiektów udo i UDAAGs 
    - Funkcje języka U-SQL
    - Funkcją okienkową U-SQL
 
    ![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   Funkcja automatycznego uzupełniania w metadanych usługi Data Lake Analytics IntelliSense: narzędzi Data Lake Tools pobierze lokalnie informacje metadanych usługi Data Lake Analytics. Funkcja IntelliSense automatycznie wypełni obiektów, łącznie z bazy danych, schematu, tabeli, widoku, funkcji zwracającej tabelę, procedury i zestawów języka C# z metadanych usługi Data Lake Analytics.
 
    ![Narzędzia Data Lake Tools dla programu Visual Studio kodu IntelliSense metadanych](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Znacznik błąd IntelliSense: narzędzi Data Lake Tools podkreśla błędy edytowania U-SQL i C#. 
-   Najważniejsze funkcje Składnia: narzędzi Data Lake Tools używa różne kolory do odróżnienia elementów, takich jak zmienne, słowa kluczowe, typ danych i funkcji. 

    ![Zawiera opis narzędzi Data Lake Tools dla Visual Studio Code składni](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Następne kroki

- Dla przebiegu lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).
- Aby — wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).



