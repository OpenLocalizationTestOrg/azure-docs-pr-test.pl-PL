---
title: "aaaGet wprowadzenie do Eksploratora usługi Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Zarządzanie zasobami usługi Azure Storage za pomocą programu Storage Explorer (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Wprowadzenie do programu Storage Explorer (wersja zapoznawcza)
## <a name="overview"></a>Omówienie
Eksplorator usługi Azure Storage (wersja zapoznawcza) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux. W tym artykule dowiesz się hello różnych sposobów łączenia tooand Zarządzanie kontami magazynu Azure.

![Microsoft Azure Storage Explorer (wersja zapoznawcza)][15]

## <a name="prerequisites"></a>Wymagania wstępne
* [Pobieranie i instalowanie programu Storage Explorer (wersja zapoznawcza)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Połącz z usługą lub kontem magazynu tooa
Eksplorator usługi Storage (wersja zapoznawcza) oferuje kilka możliwości tooconnect toostorage kont. Można na przykład:
* Łączenie kont toostorage skojarzonych z subskrypcjami platformy Azure.
* Podłącz toostorage konta i usługi, które są udostępniane z innych subskrypcji platformy Azure.
* Połącz tooand Zarządzanie magazynem lokalnym przy użyciu hello emulatora magazynu Azure. 

Ponadto można pracować z kontami magazynu na globalnej i krajowej platformie Azure:

* [Połącz tooan subskrypcji platformy Azure](#connect-to-an-azure-subscription): Zarządzanie zasobami magazynu, które należą tooyour subskrypcji platformy Azure.
* [Praca z magazynu lokalnego programowanie](#work-with-local-development-storage): Zarządzanie magazynem lokalnym przy użyciu hello emulatora magazynu Azure.
* [Dołącz magazynu tooexternal](#attach-or-detach-an-external-storage-account): Zarządzanie zasobami magazynu, które należą tooanother subskrypcji platformy Azure lub które są w obszarze national chmury Azure przy użyciu nazwy konta magazynu hello, klucz i punktów końcowych.
* [Dołączanie konta magazynu przy użyciu sygnatury dostępu Współdzielonego](#attach-storage-account-using-sas): Zarządzanie zasobami magazynu, które należą tooanother subskrypcji platformy Azure przy użyciu sygnatury dostępu współdzielonego (SAS).
* [Dołączanie usługi przy użyciu sygnatury dostępu Współdzielonego](#attach-service-using-sas): Zarządzanie określoną usługą magazynu (kontenera obiektów blob, kolejki lub tabeli) należącą tooanother subskrypcji platformy Azure przy użyciu sygnatury dostępu Współdzielonego.

## <a name="connect-tooan-azure-subscription"></a>Połącz tooan subskrypcji platformy Azure
> [!NOTE]
> Jeśli nie masz konta platformy Azure, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Ustawienia konta platformy Azure**.

    ![Ustawienia konta platformy Azure][0]

2. w okienku po lewej stronie powitania Wyświetla wszystkie konta Microsoft hello, który użytkownik został zarejestrowany w usłudze. Konto tooanother tooconnect, wybierz opcję **Dodaj konto**, a następnie wykonaj toosign instrukcje hello za pomocą konta Microsoft, który jest skojarzony z co najmniej jedną aktywną subskrypcją platformy Azure.

    >[!NOTE]
    >Łączenie toonational Azure (na przykład platformy Azure w Niemczech, Azure dla instytucji rządowych i Chińskiej wersji platformy Azure za pomocą logowania) nie jest obecnie obsługiwane. Zobacz hello "Dołączanie lub odłączanie konta magazynu zewnętrznego" sekcji opisano sposób kontami magazynu Azure toonational tooconnect.

3. Po pomyślnym zalogowaniu się przy użyciu konta Microsoft, lewo hello okienko jest wypełniana hello subskrypcji platformy Azure skojarzonych z tym kontem. Wybierz hello subskrypcji platformy Azure, które mają toowork z, a następnie wybierz **Zastosuj**. (Wybieranie **wszystkie subskrypcje** przełącza wyświetlaniem wszystkich lub żadnej hello wymienionych subskrypcji platformy Azure.)

    ![Wybieranie subskrypcji platformy Azure][3]  
    w okienku po lewej stronie powitania Wyświetla hello konta magazynu skojarzone z hello wybrane subskrypcje platformy Azure.

    ![Wybrane subskrypcje platformy Azure][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Połączyć subskrypcję Azure stosu tooan

Uzyskać informacje dotyczące łączenia subskrypcji Azure stosu tooan, zobacz [tooan połączenia Eksploratora usługi Storage subskrypcji Azure stosu](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Praca z lokalnym magazynem projektowym
Z Eksploratora usługi Storage (wersja zapoznawcza) można pracować z magazynu lokalnego przy użyciu hello emulatora magazynu Azure. To rozwiązanie umożliwia pisanie kodu oraz testów magazynu bez konieczności posiadania konta magazynu wdrożonego na platformie Azure, ponieważ hello konta magazynu jest emulowane przez Emulator usługi Azure Storage hello.

> [!NOTE]
> Witaj emulatora magazynu Azure jest obecnie obsługiwane tylko dla systemu Windows.
>
>

1. W okienku po lewej stronie powitania z Eksploratora usługi Storage (wersja zapoznawcza), rozwiń węzeł hello **(lokalny i dołączonego)** > **kont magazynu** > **(Programowanie)** węzła.

    ![Węzeł projektowania lokalnego][21]

2. Jeśli hello emulatora magazynu Azure nie został jeszcze zainstalowany, to zostanie wyświetlony monit o toodo tak za pośrednictwem paska informacyjnego. Jeśli zostanie wyświetlony pasek informacyjny hello, wybierz **pobierania hello najnowszej wersji**, a następnie zainstaluj hello emulator.

    ![Monit o pobranie emulatora usługi Azure Storage][22]

3. Po zainstalowaniu emulatora hello można tworzyć i pracować z lokalnych obiektów blob, kolejek i tabel. toolearn jak typ toowork z każdego konta magazynu, zobacz jedną z następujących hello:

    * [Zarządzanie zasobami usługi Azure Blob Storage](vs-azure-tools-storage-explorer-blobs.md)
    * Zarządzanie zasobami magazynu udziału plików platformy Azure: *dostępne wkrótce*
    * Zarządzanie zasobami usługi Azure Queue Storage: *dostępne wkrótce*
    * Zarządzanie zasobami usługi Azure Table Storage: *dostępne wkrótce*

## <a name="attach-or-detach-an-external-storage-account"></a>Dołączanie lub odłączanie konta magazynu zewnętrznego
Z Eksploratora usługi Storage (wersja zapoznawcza) można dołączyć tooexternal kont magazynu, dzięki czemu można łatwo udostępniać konta magazynu. W tej sekcji opisano sposób tooattach too(and detach from) kont magazynu zewnętrznego.

### <a name="get-hello-storage-account-credentials"></a>Uzyskiwanie poświadczeń konta magazynu hello
tooshare konta magazynu zewnętrznego, hello właściciela tego konta musi najpierw uzyskać poświadczenia hello (nazwa konta i klucz) dla konta hello, a następnie udostępnić te informacje osobie hello, którzy chcą tooattach toothat (zewnętrznego) konta. Można uzyskać poświadczeń konta magazynu hello za pośrednictwem portalu Azure hello hello następujący:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Wybierz pozycję **Przeglądaj**.

3. Wybierz pozycję **Konta usługi Storage**.

4. Na powitania **kont magazynu** bloku, wybierz hello żądanego konta magazynu.

5. Na powitania **ustawienia** bloku hello wybranego konta magazynu, wybierz **klucze dostępu**.

    ![Opcja Klucze dostępu][5]

6. Na powitania **klucze dostępu** bloku, hello kopiowania **nazwy konta magazynu** i **klucz1** wartości do użycia podczas dołączania konta magazynu toohello.

    ![Klawisze dostępu][6]

### <a name="attach-tooan-external-storage-account"></a>Dołączanie konta magazynu zewnętrznego tooan
konta magazynu zewnętrznego tooan tooattach, należy nazwę hello konta i klucz. sekcja "Poświadczeń konta magazynu hello Get" Hello wyjaśniono, jak te wartości z tooobtain hello portalu Azure. Jednak w portalu hello klucz konta hello jest nazywany **klucz1**. Dlatego w przypadku, gdy Eksploratora usługi Storage (wersja zapoznawcza) wprowadza się klucza konta, możesz wprowadzić hello **klucz1** wartości.

1. W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.

    ![Opcja magazynu tooAzure połączenia][23]

2. W hello **połączyć tooAzure magazynu** okna dialogowego należy określić klucz konta hello (hello **klucz1** wartość z zakresu od hello portalu Azure), a następnie wybierz **dalej**.

    > [!NOTE]
    > Możesz wprowadzić parametry połączenia magazynu hello z konta magazynu Azure national. Na przykład tooconnect tooAzure Niemcy kont magazynu, wprowadź następujące toohello podobne parametry połączenia: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<klucz_konta_magazynu>
    >* EndpointSuffix=core.cloudapi.de
    
    >Można pobrać ciągu połączenia hello z hello Azure portalu w hello sam sposób, jak opisano w hello sekcji "Uzyskiwanie poświadczeń konta magazynu hello".

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. W hello **Dołącz zewnętrzną usługę Storage** okno dialogowe, w hello **nazwa konta** , wprowadź nazwę konta magazynu hello, określ odpowiednie ustawienia, a następnie wybierz **dalej**.

    ![Okno dialogowe Dołączanie zewnętrznej usługi Storage][8]

4. W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji. Toochange cokolwiek, zaznacz **ponownie** i wprowadzić ustawienia hello potrzebne. 

5. Wybierz przycisk **Połącz**.

6. Po pomyślnym połączeniu konta magazynu zewnętrznego hello jest wyświetlana z **(zewnętrzne)** dołączana nazwa konta magazynu toohello.

    ![Wynik łączenia tooan konta magazynu zewnętrznego][9]

### <a name="detach-from-an-external-storage-account"></a>Odłączanie konta magazynu zewnętrznego
1. Kliknij prawym przyciskiem myszy konto magazynu zewnętrznego hello mają toodetach, a następnie wybierz **Detach**.

    ![Opcja odłączenia magazynu][10]

2. Komunikat potwierdzający hello, wybierz **tak** tooconfirm hello odłączenie konta magazynu zewnętrznego hello.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Dołączanie konta magazynu przy użyciu sygnatury dostępu współdzielonego
[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) umożliwia Witaj, Administratorze subskrypcji platformy Azure przyznać konta magazynu tymczasowego dostępu tooa bez konieczności tooprovide poświadczenia subskrypcji platformy Azure.

tooillustrate w tym scenariuszu, załóżmy, że ten Użytkownik_a jest administratorem subskrypcji platformy Azure i Użytkownik_a chce tooaccess Użytkownik_b tooallow konta magazynu przez ograniczony czas z określonymi uprawnieniami:

1. Użytkownik_a generuje sygnatury dostępu Współdzielonego (składającą się z hello parametry połączenia dla konta magazynu hello) na określoną godzinę okresu i hello potrzebne uprawnienia.

2. Użytkownik_a udziałów hello sygnatury dostępu Współdzielonego osobie hello (w naszym przykładzie Użytkownik_b), którzy chcą konta magazynu toohello dostępu.  

3. Użytkownik_b korzysta z konta toohello tooattach Eksploratora usługi Storage (wersja zapoznawcza), który należy tooUserA za pomocą hello dostarczony sygnatury dostępu Współdzielonego.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Uzyskiwanie sygnatury dostępu Współdzielonego hello konta, które chcesz tooshare
1. W Eksploratorze usługi Storage (wersja zapoznawcza), kliknij prawym przyciskiem myszy konto magazynu hello chcesz udostępnić, a następnie wybierz **Uzyskaj sygnaturę dostępu współdzielonego**.

    ![Opcja menu kontekstowego Uzyskaj sygnaturę dostępu współdzielonego][13]

2. W hello **sygnatura dostępu współdzielonego** oknie dialogowym Określ przedział czasu hello i uprawnienia, które hello konta, a następnie wybierz **Utwórz**.

    ![Okno dialogowe uzyskiwania sygnatury dostępu współdzielonego][14]  
    Witaj **sygnatura dostępu współdzielonego** otwiera okno dialogowe i wyświetla hello sygnatury dostępu Współdzielonego.

3. Dalej toohello **ciąg połączenia**, wybierz pozycję **kopiowania** toocopy go Schowka toohello, a następnie wybierz **Zamknij**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Dołączanie toohello udostępnionego konta przy użyciu hello SAS
1. W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.

    ![Opcja magazynu tooAzure połączenia][23]

2. W hello **połączyć tooAzure magazynu** okno dialogowe, określ ciąg połączenia hello, a następnie wybierz **dalej**.

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji. Wybierz zmiany toomake **ponownie**i wprowadź ustawienia hello. 

4. Wybierz przycisk **Połącz**.

5. Po dołączeniu go hello konto magazynu zostanie wyświetlony z **(SAS)** dołączany toohello nazwę konta, który został dostarczony.

    ![Wynik konto podłączone tooan przy użyciu sygnatury dostępu Współdzielonego][17]

## <a name="attach-a-service-by-using-an-sas"></a>Dołączanie usługi przy użyciu sygnatury dostępu współdzielonego
sekcja "Dołącz konto magazynu przy użyciu sygnatury dostępu Współdzielonego" Hello wyjaśniono, jak administrator subskrypcji Azure mogą udzielać dostępu konta magazynu tymczasowego dostępu tooa generowania i udostępniając sygnatury dostępu Współdzielonego dla konta magazynu hello. Podobnie można wygenerować sygnaturę dostępu współdzielonego dla określonej usługi (kontenera obiektów blob, kolejki lub tabeli) w ramach konta magazynu.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Generowanie sygnatury dostępu Współdzielonego dla usługi hello, które mają tooshare
W tym kontekście usługa może być kontenerem, kolejką lub tabelą obiektów blob. Witaj toogenerate sygnatury dostępu Współdzielonego dla wymienionych usług, zobacz:

* [Pobierz hello SAS dla kontenera obiektów blob](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Pobierz hello sygnatury dostępu Współdzielonego dla udziału plików: *wkrótce*
* Pobierz hello sygnatury dostępu Współdzielonego dla kolejki: *wkrótce*
* Pobierz hello sygnatury dostępu Współdzielonego dla tabeli: *wkrótce*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Dołączanie usługi przy użyciu hello sygnatury dostępu Współdzielonego konta toohello udostępnionych
1. W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.

    ![Opcja magazynu tooAzure połączenia][23]

2. W hello **połączyć tooAzure magazynu** okno dialogowe, określ hello identyfikatora URI połączenia SAS, a następnie wybierz **dalej**.

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji. Wybierz zmiany toomake **ponownie**i wprowadź ustawienia hello. 

4. Wybierz przycisk **Połącz**.

5. Po dołączeniu go hello nowo dołączona usługa zostanie wyświetlona w obszarze hello **(usługa SAS)** węzła.

    ![Wynik dołączanie tooa udostępnione usługi przy użyciu sygnatury dostępu Współdzielonego][20]

## <a name="search-for-storage-accounts"></a>Wyszukiwanie kont magazynu
Jeśli masz długą listę kont magazynu, szybko toolocate określone konto magazynu jest pole wyszukiwania hello toouse u góry hello hello w lewym okienku.

Podczas wpisywania w polu wyszukiwania hello hello lewe okienko wyświetla hello magazynu kont, które pasuje do wartości wyszukiwania hello wprowadzono toothat punktu. Na przykład wyszukiwania dla wszystkie magazyny kont, których nazwa zawiera **tarcher** jest wyświetlany w obszarze powitania po zrzut ekranu:

![Wyszukiwanie kont magazynu][11]

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie zasobami usługi Azure Blob Storage przy użyciu programu Storage Explorer (wersja zapoznawcza)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
