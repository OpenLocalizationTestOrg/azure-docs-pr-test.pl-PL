---
title: "Usługi Azure Data Lake Tools: Użycia usługi Azure Data Lake Tools dla programu Visual Studio Code | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak narzędzia toouse Azure Data Lake Tools dla Visual Studio Code toocreate, testowanie i uruchamianie skryptów U-SQL. "
Keywords: "VScode, usługi Azure Data Lake Tools, lokalnego uruchamiania lokalnego debugowania, debugowania lokalnego pliku magazynu w wersji zapoznawczej, Przekaż toostorage ścieżki"
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
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Użyj usługi Azure Data Lake Tools dla programu Visual Studio Code

Dowiedz się, jak narzędzia toouse Azure Data Lake Tools dla toocreate programu Visual Studio (kod VS), testowanie i uruchamianie skryptów U-SQL. informacje Hello jest również objęte powitania po wideo:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Wymagania wstępne

Narzędzia Data Lake Tools można zainstalować na powitania platformach obsługiwanych przez kod programu VS. Hello obsługiwane platformy to Windows, Linux lub MacOS. Witaj na różnych platformach mają hello następujące wymagania wstępne:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Dodaj hello java.exe ścieżka toohello środowiska zmiennej ścieżki systemu. Instrukcje konfiguracji można znaleźć [jak ustawić lub zmienić zmiennej systemowej Path hello?]( https://www.java.com/download/help/path.xml). Ścieżka Hello jest tooC:\Program Files\Java\jdk1.8.0_77\jre\bin podobne.
    - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (zalecamy Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall hello kodu, wprowadź następujące polecenie hello:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - Pakiet deb hello tooupdate źródło, wprowadź hello następującego polecenia:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, wprowadź następujące polecenie hello:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 nie jest obsługiwane. Całkowicie przed zainstalowaniem 4.2.x, należy odinstalować wersję 4.6.  

        - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Aby uzyskać instrukcje instalacji, zobacz hello [Linux 64-bitowe instrukcje instalacji Java]( https://java.com/en/download/help/linux_x64_install.xml) strony.
        - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp). Aby uzyskać instrukcje instalacji, zobacz hello [Linux 64-bitowe instrukcje instalacji Java](https://java.com/en/download/help/mac_install.xml) strony.
    - [Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Instalowania narzędzi Data Lake Tools

Po zainstalowaniu wymagań wstępnych hello można zainstalować narzędzi Data Lake Tools dla programu VS kodu.

**tooinstall narzędzi Data Lake Tools**

1. Otwórz kod programu Visual Studio.
2. Wybierz kombinację klawiszy Ctrl + P, a następnie wprowadź następujące polecenie hello:
```
ext install usql-vscode-ext
```
Można wyświetlić listę rozszerzeń kodu programu Visual Studio. Jeden z nich jest **Azure Data Lake Tools**.

3. Wybierz **zainstalować** dalej zbyt**Azure Data Lake Tools**. Po kilku sekundach hello **zainstalować** przycisk zmiany zbyt**Załaduj ponownie**.
4. Wybierz **Załaduj ponownie** tooactivate hello rozszerzenia.
5. Wybierz **OK** tooconfirm. Azure Data Lake Tools można zobaczyć w hello **rozszerzenia** okienka.
    ![Narzędzia Data Lake Tools dla okienka rozszerzenia kodu programu Visual Studio](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Aktywacja usługi Azure Data Lake Tools
Utwórz nowy plik .usql lub Otwórz istniejący .usql tooactivate hello rozszerzenie. 

## <a name="connect-tooazure"></a>Połącz tooAzure

Można było skompilować i uruchomić skrypty U-SQL w usługi Data Lake Analytics, należy połączyć tooyour konto platformy Azure.

**tooconnect tooAzure**

1.  Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety. 
2.  Wprowadź **ADL: logowania**. informacje logowania Hello jest wyświetlana w hello **dane wyjściowe** okienka.

    ![Data Lake Tools dla Visual Studio Code polecenia palety](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![narzędzi Data Lake Tools dla Visual Studio Code informacji o logowaniu urządzenia](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Wybierz kombinację klawiszy Ctrl + kliknięcie hello adres URL logowania: https://aka.ms/devicelogin tooopen hello logowania strony sieci Web. Wprowadź kod hello **G567LX42V** w polu tekstowym hello, a następnie wybierz **Kontynuuj**.

   ![Narzędzia Data Lake Tools dla Visual Studio Code logowania Wklej kod](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Wykonaj toosign instrukcje hello w z hello strony sieci Web. Po nawiązaniu połączenia nazwa konta usługi Azure zostanie wyświetlony na pasku stanu hello w hello lewym dolnym rogu hello **kodzie VS** okna. 

    > [!NOTE] 
    > Jeśli konto ma dwa składniki włączone, zalecane jest użycie z telefonu uwierzytelniania, a nie za pomocą numeru PIN.

toosign, wprowadź polecenie hello **ADL: wylogowania**.

## <a name="list-your-data-lake-analytics-accounts"></a>Lista kont usługi Data Lake Analytics

połączenie hello tootest, Pobierz listę kont usługi Data Lake Analytics.

**konta usługi Data Lake Analytics hello toolist w ramach Twojej subskrypcji platformy Azure**

1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.
2. Wprowadź **ADL: listy kont**. Witaj konta są wyświetlane w hello **dane wyjściowe** okienka.

## <a name="open-hello-sample-script"></a>Otwórz hello przykładowy skrypt
Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: Otwórz przykładowy skrypt**. Zostanie otwarte inne wystąpienie tego przykładu. Można również edytować, skonfigurować i przesłać skrypt w tym wystąpieniu.

## <a name="work-with-u-sql"></a>Praca z języka U-SQL

Języku U-SQL należy otworzyć plików U-SQL lub toowork folderu.

**tooopen folderu projektu U-SQL**

1. Visual Studio Code, zaznacz hello **pliku** menu, a następnie wybierz **Otwórz Folder**.
2. Określ folder, a następnie wybierz **wybierz Folder**.
3. Wybierz hello **pliku** menu, a następnie wybierz **nowy**. Plik bez tytułu-1 jest dodawany toohello projektu.
4. Wprowadź powitania po kod do pliku hello bez tytułu 1:

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

    Witaj skrypt tworzy plik departments.csv z niektórych danych zawartych w folderze/Output hello.

5. Zapisz plik hello jako **myUSQL.usql** w hello otworzyć folderu. Plik konfiguracji adltools_settings.json jest także dodawane toohello projektu.
4. Otwórz i skonfiguruj adltools_settings.json hello następujące właściwości:

    - Konto: Konta Data Lake Analytics w ramach Twojej subskrypcji platformy Azure.
    - Baza danych: Baza danych przy użyciu tego konta. Domyślnie Hello **wzorca**.
    - Schemat: Schemat w bazie danych. Domyślnie Hello **dbo**.
    - Ustawienia opcjonalne:
        - Priorytet: hello priorytet jest zakres od 1 too1000 z 1 hello najwyższy priorytet. Witaj, wartość domyślna to **1000**.
        - Równoległość: zakres równoległości hello jest z 1 too150. Witaj, wartość domyślna to hello równoległości maksymalny dozwolony na koncie usługi Azure Data Lake Analytics. 
        
        > [!NOTE] 
        > Jeśli ustawienia hello są nieprawidłowe, wartości domyślne hello są używane.

    ![Narzędzia Data Lake Tools dla Visual Studio Code pliku konfiguracji](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Obliczeniowe, to konto usługi Data Lake Analytics potrzebne toocompile i uruchamianie zadań U-SQL. Należy skonfigurować konto komputera hello przed możesz skompilować i uruchomić zadań U-SQL.
    
Po zapisaniu konfiguracji hello hello konta, bazę danych i schemat informacje są wyświetlane na pasku stanu hello w hello lewym dolnym rogu hello odpowiedni plik .usql. 
 
 
W porównaniu tooopening plik, po otwarciu folderu, które można wykonywać następujące czynności:

- Użyj pliku CodeBehind. W trybie pojedynczego pliku hello związane z kodem nie jest obsługiwane.
- Przy użyciu pliku konfiguracji. Po otwarciu folderu hello skryptów w hello folder roboczy udostępniać pojedynczym pliku konfiguracji.


Witaj skryptu U-SQL kompiluje zdalnie za pośrednictwem hello usługi Data Lake Analytics. Podczas wystawiania hello **skompilować** polecenia, konto usługi Data Lake Analytics tooyour jest wiadomości powitania skryptu U-SQL. Później Visual Studio Code odbiera hello wynik kompilacji. Powodu toohello kompilacji zdalnej Visual Studio Code wymaga, wyświetlić listę informacji hello tooconnect tooyour konto usługi Data Lake Analytics hello pliku konfiguracji.

**skrypt toocompile U-SQL**

1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety. 
2. Wprowadź **ADL: kompilowania skryptu**. Witaj kompilacji wyniki są wyświetlane na powitania **dane wyjściowe** okna. Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: kompilowania skryptu** zadania toocompile U-SQL. Wynik kompilacji Hello jest wyświetlana w hello **dane wyjściowe** okienka.
 

**skrypt toosubmit U-SQL**

1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety. 
2. Wprowadź **ADL: przesłać zadania**.  Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: Prześlij zadanie**. 

Po przesłaniu zadania skryptu U-SQL hello przesyłanie dzienników pojawia się w hello **dane wyjściowe** okna w kodzie VS. Jeśli hello przesyłanie zakończy się pomyślnie, również zostanie wyświetlony adres URL zadania hello. Adres URL zadania hello można otworzyć w stan zadania w czasie rzeczywistym hello tootrack przeglądarki sieci web.

dane wyjściowe hello tooenable hello szczegóły zadania, ustaw **jobInformationOutputPath** w hello **vs kod hello u-sql_settings.json** pliku.
 
## <a name="use-a-code-behind-file"></a>Przy użyciu pliku CodeBehind

Plik CodeBehind jest pliku C# skojarzonego z jednego skryptu U-SQL. W pliku CodeBehind hello można zdefiniować tooUDO skryptu w wersji dedykowanej, UDA, UDT i funkcji zdefiniowanej przez użytkownika. Witaj UDO, UDA UDT i funkcji zdefiniowanej przez użytkownika można bezpośrednio w skrypcie hello bez rejestrowania najpierw hello zestawu. Hello pliku CodeBehind jest umieszczany w hello sam folder jako jego komunikacji równorzędnej pliku skryptu U-SQL. Jeśli skrypt hello nosi nazwę xxx.usql, kodem hello nosi nazwę jako xxx.usql.cs. Jeśli usuniesz ręcznie pliku CodeBehind hello, hello CodeBehind funkcja jest wyłączona dla jego skojarzony skrypt U-SQL. Aby uzyskać więcej informacji na temat pisania kodu klienta dla skryptu U-SQL, zobacz [pisania i przy użyciu niestandardowego kodu w języku U-SQL: funkcje zdefiniowane przez użytkownika]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

toosupport związane z kodem, możesz otworzyć folderu roboczego. 

**toogenerate pliku CodeBehind**

1. Otwórz plik źródłowy. 
2. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.
3. Wprowadź **ADL: generowanie kodu**. Plik CodeBehind jest tworzony w hello sam folder. 

Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: generowanie kodu za**. 

toocompile i przesłać skrypt U-SQL przy użyciu pliku CodeBehind jest hello tak samo jak plik skryptu, autonomiczny hello U-SQL.

Witaj następujące dwa zrzuty ekranu pokazują plik CodeBehind i jego skojarzony plik skryptu U-SQL:
 
![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Plik skryptu narzędzi Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Korzystanie z zestawów

Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).

Korzystanie z narzędzi Data Lake Tools tooregister kod niestandardowy zestawów, w katalogu Data Lake Analytics hello.

**tooregister zestawu**

Można zarejestrować zestawu hello za pośrednictwem hello **ADL: Zarejestruj zestawu** lub **ADL: Zarejestruj zestawu za pomocą konfiguracji** poleceń.

**tooregister za pośrednictwem hello ADL: polecenie zarejestrować zestawu**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.
2.  Wprowadź **ADL: zarejestrować zestawu**. 
3.  Określ ścieżkę zestawu lokalne powitania. 
4.  Wybierz konto usługi Data Lake Analytics.
5.  Wybierz bazę danych.

Wyniki: hello portal jest otwarty w przeglądarce i wyświetla procesu rejestracji zestawu hello.  

Inny hello tootrigger wygodny sposób **ADL: Zarejestruj zestawu** polecenia to plik dll hello tooright kliknij w Eksploratorze plików. 

**tooregister jednak hello ADL: Zarejestruj zestawu za pomocą polecenia konfiguracji**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.
2.  Wprowadź **ADL: zarejestrować zestawu za pomocą konfiguracji**. 
3.  Określ ścieżkę zestawu lokalne powitania. 
4.  Plik JSON Hello jest wyświetlany. Przejrzyj i Edytuj zależności zestawu hello i parametry zasobu, jeśli to konieczne. Instrukcje są wyświetlane w hello **dane wyjściowe** okna. tooproceed toohello rejestrowania zestawów, Zapisz plik JSON hello (Ctrl + S).

![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Zależności zestawu: automatycznie wykrywa Azure Data Lake Tools czy hello DLL ma zależności. zależności Hello są wyświetlane w pliku JSON powitania po ich wykryciu. 
>- Zasoby: Można przekazać biblioteki DLL zasobów (na przykład txt, .png i .csv) jako część hello zestawu rejestracji. 

Inny sposób tootrigger hello **ADL: Zarejestruj zestawu za pomocą konfiguracji** polecenia to plik dll hello tooright kliknij w Eksploratorze plików. 

Pokazuje Hello następującego kodu U-SQL, jak toocall zestawu. W przykładzie hello jest nazwą zestawu hello *testu*.

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
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Wykaz usługi Data Lake Analytics hello dostępu

Po podłączeniu tooAzure służy hello następujące kroki tooaccess hello U-SQL katalogu.

**tooaccess hello Azure Data Lake Analytics metadanych**

1.  Wybierz kombinację klawiszy Ctrl + Shift + P, a następnie wprowadź **ADL: listy tabel**.
2.  Wybierz jedno z kont usługi Data Lake Analytics hello.
3.  Wybierz jedną z bazy danych usługi Data Lake Analytics hello.
4.  Wybierz jedną z hello schematów. Widać hello listy tabel.

## <a name="view-data-lake-analytics-jobs"></a>Widok Data Lake Analytics zadania

**zadania usługi Data Lake Analytics tooview**
1.  Otwórz hello polecenia palety (Ctrl + Shift + P) i wybierz **ADL: Pokaż zadania**. 
2.  Wybierz usługi Data Lake Analytics lub konta lokalnego. 
3.  Poczekaj na listę zadań hello hello tooappear konta.
4.  Wybierz zadanie z listy zadań, narzędzi Data Lake Tools otwiera hello szczegóły zadania w portalu Azure hello i wyświetla plik informacji o zadaniu hello w kodzie VS.

![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Integracja magazynu usługi Azure Data Lake

Można użyć poleceń usługi Azure Data Lake Storage, aby:
 - Przeglądaj hello Azure Data Lake Storage zasobów. 
 - Plik usługi Azure Data Lake Storage hello podglądu.  
 - Przekaż hello pliku bezpośrednio tooAzure usługi Data Lake Storage w kodzie VS. 

### <a name="list-hello-storage-path"></a>Ścieżki do magazynu hello listy 
Można wyświetlić listę hello ścieżki do magazynu za pośrednictwem palety polecenia hello lub kliknij prawym przyciskiem myszy.

**ścieżki do magazynu hello toolist za pośrednictwem hello polecenia palety**

1.  Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: ścieżka magazynu listy**.

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Wybierz użytkownika preferowany sposób wyświetlania list hello ścieżki do magazynu. Używa tego przejścia **wprowadź ścieżkę** jako przykład.

    ![Narzędzia Data Lake Tools dla Visual Studio Code ścieżki do magazynu hello toolist jednokierunkowej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS kod chroni hello odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics. Na przykład: ss tt /.
    >- Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy hello z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    >- Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    
3. Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz więcej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Wybierz **więcej** toolist więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Wprowadź ścieżkę do magazynu Azure. Na przykład/output.

    ![Narzędzia Data Lake Tools dla Visual Studio Code Wprowadź ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Wyniki: hello palety polecenie wyświetla informacje o ścieżce hello na podstawie wpisów.

    ![Narzędzia Data Lake Tools dla Visual Studio Code lista wyników ścieżki magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Ścieżka względna toolist hello jest za pośrednictwem hello wygodny sposób kliknij prawym przyciskiem myszy menu kontekstowego.

**Kliknij prawym przyciskiem myszy toolist hello ścieżki do magazynu za pośrednictwem**

1.  Kliknij prawym przyciskiem myszy tooselect ciąg ścieżki hello **ścieżki do magazynu listy**.

       ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Wybrana ścieżka względna Hello jest wyświetlana w hello polecenia palety.

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybrane ścieżki względnej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Wyniki: hello palety polecenie wyświetla listę hello folderów i plików dla bieżącej ścieżki hello.

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy z bieżącej ścieżki hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Plik magazynu hello podglądu
Można wyświetlić podgląd pliku magazynu hello za pośrednictwem palety polecenia hello lub kliknij prawym przyciskiem myszy.

**Plik magazynu hello toopreview za pomocą hello polecenia palety**

1.  Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: Podgląd pliku magazynu**.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wyświetlić podgląd pliku magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy kont](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Wybierz **więcej** toolist więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Wprowadź ścieżkę do magazynu Azure lub pliku. Na przykład /output/SearchLog.txt.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę do magazynu i](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Wyniki: hello palety polecenie wyświetla informacje o ścieżce hello na podstawie wpisów.

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Kliknij prawym przyciskiem myszy toolist hello ścieżki do magazynu za pośrednictwem**

1.  toopreview pliku, ścieżka pliku powitania kliknij prawym przyciskiem myszy.

   ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Wyniki: Kod VS Wyświetla hello Podgląd wyników hello pliku.

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Przekazywanie pliku 

Możesz przekazać pliki, wprowadzając polecenia hello **ADL: Przekaż plik** lub **ADL: Przekaż plik przy użyciu konfiguracji**.

**pliki tooupload jednak hello ADL: Przekaż plik — polecenie**
1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety lub kliknij prawym przyciskiem myszy hello edytora skryptów, a następnie wprowadź **Przekaż plik**.
2.  Witaj tooupload pliku, wprowadź ścieżkę lokalną.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę lokalną](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Wybierz jeden z sposobów hello ścieżki do magazynu hello listy. Używa tego przejścia **wprowadź ścieżkę** jako przykład.

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS kod chroni hello odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics. Na przykład: ss tt /.
    >- Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy hello z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.
    >- Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.

4. Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.

    ![Narzędzia Data Lake Tools dla Visual Studio Code magazynu, kliknij prawym przyciskiem myszy](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Wprowadź ścieżkę do magazynu Azure. Na przykład: / output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Znajdź ścieżki magazynu Azure. Wybierz **Wybierz bieżący folder**.

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz folder](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Wyniki: hello **dane wyjściowe** okno wyświetla stan przekazywania pliku hello.

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**pliki tooupload jednak hello ADL: Przekaż plik za pomocą polecenia konfiguracji**
1.  Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety lub kliknij prawym przyciskiem myszy hello edytora skryptów, a następnie wprowadź **Przekaż plik przy użyciu konfiguracji**.
2.  VS kod przedstawia plik JSON. Można wprowadzić ścieżki do plików i przekazywania wielu plików na powitania tym samym czasie. Instrukcje są wyświetlane w hello **dane wyjściowe** okna. tooproceed tooupload hello plik, Zapisz plik JSON hello (Ctrl + S).

       ![Ścieżka pliku narzędzia Data Lake Tools dla Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Wyniki: hello **dane wyjściowe** okno wyświetla stan przekazywania pliku hello.

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Innym tooupload sposób toostorage pliku jest za pośrednictwem hello menu Pełna ścieżka pliku hello lub ścieżkę względną hello plik w Edytorze skryptów powitania kliknij prawym przyciskiem myszy. Wprowadź ścieżkę do pliku lokalnego hello, a następnie wybierz konto hello. Witaj **dane wyjściowe** okno wyświetla stan przekazywania hello. 

### <a name="open-azure-storage-explorer"></a>Eksplorator usługi Storage Azure Otwórz
Możesz otworzyć **Eksploratora usługi Storage Azure** wprowadzając polecenie hello **ADL: Otwórz Eksploratora usługi sieci Web Azure Storage** lub wybierając z menu kontekstowego powitania kliknij prawym przyciskiem myszy.

**tooopen Eksploratora usługi Storage platformy Azure**

1. Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.
2. Wprowadź **Otwórz Eksploratora usługi Storage Azure Web** lub kliknij prawym przyciskiem myszy na ścieżkę względną lub pełną ścieżkę hello na powitania edytora skryptów, a następnie wybierz **Otwórz Eksploratora usługi Storage Azure Web**.
3. Wybierz konto usługi Data Lake Analytics.

Narzędzia Data Lake Tools otwiera ścieżki do magazynu Azure hello hello portalu Azure. Plik hello ścieżkę i Podgląd hello hello sieci Web można znaleźć.

### <a name="local-run-and-local-debug-for-windows-users"></a>Przebieg lokalny i lokalny debugowania dla systemu Windows użytkownicy
Uruchamiania lokalnego skryptu U-SQL sprawdza danych lokalnych i weryfikuje skrypt lokalnie, zanim kodu jest opublikowane tooData Lake Analytics. Umożliwia funkcji debugowania lokalnego Hello możesz toocomplete hello następujące zadania, zanim Twój kod przesłane tooData Lake Analytics: 
- Debugowanie programu C# związane z kodem. 
- Przejrzyj kroki hello kodu. 
- Sprawdź poprawność skrypt lokalnie.

Aby uzyskać instrukcje dotyczące przebiegu lokalnego i debugowania lokalnego, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Dodatkowe funkcje

Narzędzia Data Lake Tools dla programu VS kodu obsługuje hello następujące funkcje:

-   Funkcja automatycznego uzupełniania IntelliSense: sugestie są wyświetlane w wyskakujące wokół elementów, takich jak słowa kluczowe, metod i zmiennych. Inne ikony reprezentują różne typy obiektów hello:

    - Scala — typ danych
    - Typ danych złożonych
    - Wbudowanych typów
    - Klasy i kolekcji .NET
    - Wyrażenia języka C#
    - Funkcje UDF wbudowane C#, obiektów udo i UDAAGs 
    - Funkcje języka U-SQL
    - Funkcją okienkową U-SQL
 
    ![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   Funkcja automatycznego uzupełniania w metadanych usługi Data Lake Analytics IntelliSense: narzędzi Data Lake Tools pobiera informacje metadanych usługi Data Lake Analytics hello lokalnie. funkcja IntelliSense Hello automatycznie wypełni obiektów, w tym hello bazy danych, schematu, tabeli, widoku, funkcji zwracającej tabelę, procedury i zestawów języka C# z hello metadanych usługi Data Lake Analytics.
 
    ![Narzędzia Data Lake Tools dla programu Visual Studio kodu IntelliSense metadanych](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Znacznik błąd IntelliSense: narzędzi Data Lake Tools podkreśla hello edytowanie błędy U-SQL i C#. 
-   Najważniejsze funkcje Składnia: narzędzi Data Lake Tools używa elementów toodifferentiate różne kolory, takich jak zmienne, słowa kluczowe, typ danych i funkcji. 

    ![Zawiera opis narzędzi Data Lake Tools dla Visual Studio Code składni](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Następne kroki

- Dla przebiegu lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).
- Aby — wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).



