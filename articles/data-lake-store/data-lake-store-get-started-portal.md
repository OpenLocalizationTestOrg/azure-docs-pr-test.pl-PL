---
title: "wprowadzenie do usługi Data Lake Store aaaUse tooget portalu Azure | Dokumentacja firmy Microsoft"
description: "Użyj hello Azure toocreate portalu konta usługi Data Lake Store i wykonywać podstawowe operacje w hello usługi Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Wprowadzenie do usługi Azure Data Lake Store za pomocą hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Dowiedz się, jak toouse hello Azure toocreate portalu konta usługi Azure Data Lake Store i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md).

Hello następujące dwa klipy wideo zawierają hello tych samych informacji, zgodnie z opisem w tym artykule:

* [Tworzenie konta usługi Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Zarządzanie danymi w usłudze Data Lake Store za pomocą hello Eksploratora danych](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Tworzenie konta usługi Azure Data Lake Store

1. Zaloguj się na nowy toohello [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **NOWY**, pozycję **Dane i magazyn**, a następnie pozycję **Azure Data Lake Store**. Przeczytaj informacje hello w hello **Azure Data Lake Store** bloku, a następnie kliknij przycisk **Utwórz** w hello lewym dolnym rogu bloku hello.
3. W hello **Nowa usługa Data Lake Store** bloku, podaj wartości hello, jak pokazano w powitania po zrzut ekranu:
   
    ![Tworzenie nowego konta usługi Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Tworzenie nowego konta usługi Azure Data Lake")
   
   * **Nazwa**. Wprowadź unikatową nazwę hello konta usługi Data Lake Store.
   * **Subskrypcja**. Wybierz subskrypcję hello, pod którym ma zostać toocreate nowe konto usługi Data Lake Store.
   * **Grupa zasobów**. Wybierz istniejącą grupę zasobów lub hello **Utwórz nowy** toocreate opcji, jeden. Grupa zasobów to kontener, który zawiera powiązane zasoby dla aplikacji. Aby uzyskać więcej informacji, zobacz [Grupy zasobów na platformie Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Lokalizacja**: Wybierz lokalizację, w której ma konto usługi Data Lake Store hello toocreate.
   * **Ustawienia szyfrowania**. Dostępne są trzy opcje:
     
     * **Nie włączaj szyfrowania**.
     * **Użyj klucz zarządzanych przez usługę Azure Data Lake**.  Jeśli chcesz toomanage Azure Data Lake — magazyn kluczy szyfrowania.
     * **Wybierz klucze z usługi Azure Key Vault**. Możesz wybrać istniejącą usługę Azure Key Vault lub utworzyć nową usługę Key Vault. klucze hello toouse z magazynu kluczy, należy przypisać uprawnienia dla konta usługi Azure Data Lake Store tooaccess hello Azure Key Vault hello. Witaj instrukcje, zobacz [przypisać uprawnienia tooAzure Key Vault](#assign-permissions-to-azure-key-vault).
       
        ![Szyfrowanie usługi Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Szyfrowanie usługi Data Lake Store")
       
        Kliknij przycisk **OK** w hello **ustawienia szyfrowania** bloku.

        Aby uzyskać więcej informacji, zobacz [Szyfrowanie danych w usłudze Azure Data Lake Store](./data-lake-store-encryption.md).

4. Kliknij przycisk **Utwórz**. Jeśli została wybrana opcja toopin hello konta toohello w pulpicie nawigacyjnym, nastąpi powrót toohello pulpitu nawigacyjnego i wyświetlany postęp hello obsługi konta usługi Data Lake Store. Raz hello konta usługi Data Lake Store jest administracyjnie, pojawi się blok konta hello.

Konto usługi Data Lake Store możesz również utworzyć za pomocą szablonów usługi Azure Resource Manager. Te szablony są dostępne na stronie [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store):

- Bez szyfrowania danych: [wdróż konto usługi Azure Data Lake Store bez szyfrowania danych](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Z szyfrowaniem danych przy użyciu usługi Data Lake Store: [wdróż konto usługi Data Lake Store z szyfrowaniem (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Z szyfrowaniem danych przy użyciu usługi Azure Key Vault: [wdróż konto usługi Data Lake Store z szyfrowaniem (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>Przypisz uprawnienia tooAzure magazyn kluczy
Jeśli klucze z usługi Azure Key Vault tooconfigure szyfrowania jest używany na powitania konta usługi Data Lake Store, należy skonfigurować dostęp między hello konto usługi Data Lake Store i konta usługi Azure Key Vault hello. Wykonaj hello, więc po toodo czynności.

1. Użycie kluczy z hello Azure Key Vault hello bloku hello konta usługi Data Lake Store jest wyświetlane ostrzeżenie u góry hello. Kliknij przycisk hello ostrzeżenie tooopen hello **skonfigurować uprawnienia do magazynu kluczy** bloku.
   
    ![Szyfrowanie usługi Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Szyfrowanie usługi Data Lake Store")
2. Blok Hello zawiera dwie opcje tooconfigure dostęp.
   
   * W pierwszej opcji powitania kliknij **Udziel uprawnień** tooconfigure dostępu. Pierwsza opcja Hello jest włączona tylko wtedy, gdy użytkownik hello, który utworzył konto usługi Data Lake Store hello jest również administratora dla hello Azure Key Vault.
   * Witaj druga opcja to toorun: hello polecenia cmdlet programu PowerShell wyświetlane w bloku hello. Należy toobe właściciela hello hello Azure Key Vault lub uprawnienia hello możliwości toogrant hello Azure Key Vault. Po uruchomieniu polecenia cmdlet hello wróć toohello bloku i kliknij przycisk **włączyć** tooconfigure dostępu.

## <a name="createfolder"></a>Tworzenie folderów w ramach konta usługi Azure Data Lake Store
Można tworzyć foldery w Twojej toomanage konta usługi Data Lake Store i przechowywania danych.

1. Otwórz utworzone konto usługi Data Lake Store hello. W okienku po lewej stronie powitania kliknij **Przeglądaj**, kliknij przycisk **usługi Data Lake Store**, a następnie w bloku Data Lake Store hello, kliknij hello nazwę konta, pod którym ma zostać toocreate folderów. Jeśli przypięty hello konta toohello w tablicy startowej, kliknij Kafelek konta.
2. W bloku konta usługi Data Lake Store kliknij pozycję **Eksplorator danych**.
   
    ![Tworzenie folderów na koncie usługi Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Tworzenie folderów na koncie usługi Data Lake Store")
3. W bloku konta usługi Data Lake Store, kliknij przycisk **nowy Folder**, wprowadź nazwę dla nowego folderu hello, a następnie kliknij przycisk **OK**.
   
    ![Tworzenie folderów na koncie usługi Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Tworzenie folderów na koncie usługi Data Lake Store")
   
    Witaj nowo utworzony folder znajduje się na powitania **Eksploratora danych** bloku. Foldery możesz zagnieżdżać do dowolnego poziomu.
   
    ![Tworzenie folderów na koncie usługi Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Tworzenie folderów na koncie usługi Data Lake")

## <a name="uploaddata"></a>Przekaż konto usługi Data Lake Store tooAzure danych
Możesz przekazać tooan Twojego danych konta usługi Azure Data Lake Store bezpośrednio na powitania tooa lub na poziomie folderu głównego utworzonego w ramach konta hello. W hello następującego zrzutu ekranu, wykonaj tooupload kroki hello podfolder tooa pliku z hello **Eksploratora danych** bloku. Na tym zrzucie ekranu plik hello jest podfolder przekazane tooa pokazano hello nawigacji (zaznaczony czerwonym prostokątem).

Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Przekazywanie danych](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Przekazywanie danych")

## <a name="properties"></a>Właściwości i Akcje dostępne na powitania przechowywanych danych
Kliknij przycisk hello nowo dodany plik tooopen hello **właściwości** bloku. Witaj właściwości skojarzone z pliku hello i hello akcje, które można wykonywać na powitania pliku są dostępne w tym bloku. Można także skopiować toofile pełną ścieżkę hello na koncie usługi Azure Data Lake Store wyróżniane w polu hello red w powitania po zrzut ekranu:

![Właściwości danych hello](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "właściwości na powitania danych")

* Kliknij przycisk **Podgląd** toosee Podgląd pliku hello bezpośrednio z przeglądarki hello. Można określić format hello również hello podglądu. Kliknij przycisk **Podgląd**, kliknij przycisk **Format** w hello **podglądu pliku** bloku w hello **Format podglądu pliku** bloku Określ hello opcje, takie jako liczba wierszy toodisplay kodowanie toouse, toouse ogranicznik itp.
  
  ![Format podglądu pliku](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Format podglądu pliku")
* Kliknij przycisk **Pobierz** toodownload hello pliku tooyour komputera.
* Kliknij przycisk **Zmień nazwę pliku** toorename hello pliku.
* Kliknij przycisk **Usuń plik** toodelete hello pliku.

## <a name="secure-your-data"></a>Zabezpieczanie danych
Możesz zabezpieczyć hello dane przechowywane na koncie usługi Azure Data Lake Store za pomocą usługi Azure Active Directory i kontroli dostępu (ACL). Aby uzyskać instrukcje dotyczące toodo, który zobacz [Zabezpieczanie danych w usłudze Azure Data Lake Store](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Usuwanie konta usługi Azure Data Lake Store
Kliknij konto usługi Azure Data Lake Store z bloku Data Lake Store z toodelete **usunąć**. Akcja hello tooconfirm, będziesz tooenter zostanie wyświetlony monit o nazwę hello hello konta, które chcesz toodelete. Wprowadź nazwę hello hello konta, a następnie kliknij przycisk **usunąć**.

![Usuwanie konta usługi Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Usuwanie konta usługi Data Lake")

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Dostęp do dzienników diagnostycznych usługi Data Lake Store](data-lake-store-diagnostic-logs.md)

