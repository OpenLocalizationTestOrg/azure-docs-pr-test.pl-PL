---
title: "Konto usługi partia zadań w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate partii zadań Azure konto hello Azure toorun portalu dużych obciążeń równoległe w chmurze hello"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Tworzenie konta usługi partia zadań z hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
>
>

Dowiedz się, jak konto partii zadań Azure toocreate hello [portalu Azure][azure_portal]i wybierz polecenie Właściwości hello konta, które pasują do danego scenariusza obliczeń. Dowiedz się, gdy toofind konta ważne właściwości, takie jak klucze dostępu i adres URL konta.

Dalsze informacje dotyczące konta usługi partia zadań i scenariusze, można znaleźć hello [funkcji — omówienie](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Tworzenie konta usługi Batch

Użyj hello toocreate portalu konta usługi partia zadań w jednym z dwóch hello *puli tryby alokacji*: **partii usługi** tryb lub nowszej hello **subskrypcji użytkownika** tryb, który wymaga więcej Konfiguracja. Aby uzyskać informacje dotyczące tych dwóch trybów, zobacz hello [funkcji — omówienie](batch-api-basics.md#account). Dla funkcji trybu subskrypcji użytkownika hello, zobacz też hello [wpis w blogu](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Tryb usługi Batch



1. Zaloguj się toohello [portalu Azure][azure_portal].
2. Kliknij kolejno opcje **Nowy** > **Obliczenia** > **Usługa Batch**.

    ![Partia hello Marketplace][marketplace_portal]
3. Witaj **nowe konto wsadowe** bloku jest wyświetlany. Patrz opisy hello poniżej poszczególnych elementów bloku.

    ![Tworzenie konta usługi Batch][account_portal]

    a. **Nazwa konta**: Nazwa konta wsadowego hello wybierzesz muszą być unikatowe w hello region platformy Azure, gdzie jest utworzone konto hello (zobacz **lokalizacji** poniżej). Witaj, nazwa konta może zawierać tylko małe litery lub cyfry i musi składać się z 3 do 24 znaków.

    b. **Subskrypcja**: hello subskrypcji, w których hello toocreate konta usługi partia zadań. Jeśli masz tylko jedną subskrypcję, jest ona wybrana domyślnie.

    c. **Tryb alokacji puli**: wybierz **Usługa Batch**.

    c. **Grupa zasobów**: wybierz istniejącą grupę zasobów dla nowego konta usługi Batch. Opcjonalnie można utworzyć nową grupę zasobów.

    d. **Lokalizacja**: hello region platformy Azure, w których hello toocreate konta usługi partia zadań. Tylko regiony hello obsługiwane przez subskrypcji i grupy zasobów są wyświetlane jako opcje.

    e. **Konto magazynu** (opcjonalne): konto usługi Azure Storage ogólnego przeznaczenia skojarzone z kontem usługi Batch. Jest to zalecane w przypadku większości kont usługi Batch. Więcej szczegółów można znaleźć w sekcji [Połączone konto usługi Azure Storage](#linked-azure-storage-account) w dalszej części tego artykułu.

4. Kliknij przycisk **Utwórz** toocreate hello konta.

   Hello portal wskazuje, że wdrożenie jest w toku. Po zakończeniu w obszarze **Powiadomienia** pojawia się powiadomienie **Wdrożenie zakończyło się pomyślnie**.

## <a name="user-subscription-mode"></a>Tryb subskrypcji użytkownika

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Zezwalaj na tooaccess partii zadań Azure hello subskrypcji (jednorazowa operacja)
Podczas tworzenia konta usługi partia zadań pierwszy w trybie użytkownika subskrypcji, należy wykonać następujące kroki tooregister hello subskrypcji z partii. (Jeśli wcześniej została to, Pomiń toohello następnej sekcji).

1. Zaloguj się toohello [portalu Azure][azure_portal].

2. Kliknij przycisk **więcej usług** > **subskrypcje**i kliknij subskrypcję hello ma toouse hello konta usługi partia zadań.

3. W hello **subskrypcji** bloku, kliknij przycisk **(IAM) kontroli dostępu** > **Dodaj**.

    ![Kontrola dostępu do subskrypcji][subscription_access]

4. Na powitania **dodać uprawnienia** bloku, wybierz hello **współautora** roli, wyszukaj hello interfejsu API partii. Wyszukiwania dla każdego z tych parametrów do momentu znalezienia hello interfejsu API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. W przypadku nowszych dzierżaw usługi Azure AD może być używana ta nazwa.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** jest identyfikator hello hello interfejsu API partii. 

5. Po znalezieniu hello interfejsu API partii, zaznacz go i kliknij **zapisać**.

    ![Dodawanie uprawnień usługi Batch][add_permission]

### <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy
W trybie użytkownika subskrypcji usługi Azure key vault jest wymagana należący toothe tej samej grupie zasobów co toobe konta wsadowego hello utworzony. Upewnij się, że grupa zasobów hello znajduje się w regionie, w przypadku partii [dostępne](https://azure.microsoft.com/regions/services/) , które obsługuje subskrypcji.

1. W hello [portalu Azure][azure_portal], kliknij przycisk **nowy** > **bezpieczeństwo i Obsługa tożsamości** > **magazyn kluczy** .

2. W hello **utworzyć magazyn kluczy** bloku, wprowadź nazwę dla magazynu kluczy hello i Utwórz grupę zasobów w regionie powitania dla Twojego konta usługi partia zadań. Pozostaw hello pozostałe ustawienia na wartości domyślne, a następnie kliknij przycisk **Utwórz**.

### <a name="create-a-batch-account"></a>Tworzenie konta usługi Batch

1. W hello [portalu Azure][azure_portal], kliknij przycisk **nowy** > **obliczeniowe** > **usługa partia zadań**.

    ![Partia hello Marketplace][marketplace_portal]
3. Witaj **nowe konto wsadowe** bloku jest wyświetlany. Patrz opisy hello poniżej poszczególnych elementów bloku.

    ![Tworzenie konta usługi Batch][account_portal_byos]

    a. **Nazwa konta**: Nazwa konta wsadowego hello wybierzesz muszą być unikatowe w hello region platformy Azure, gdzie jest utworzone konto hello (zobacz **lokalizacji** poniżej). Witaj, nazwa konta może zawierać tylko małe litery lub cyfry i musi składać się z 3 do 24 znaków.

    b. **Subskrypcja**: Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, który został zarejestrowany z hello usługa partia zadań.

    c. **Tryb alokacji puli**: wybierz pozycję **Subskrypcja użytkownika**.

    d. **Magazyn kluczy**: hello wybierz magazyn kluczy został utworzony dla konta wsadowego w poprzedniej sekcji hello. Opcjonalnie utwórz nowy magazyn kluczy. Po wybraniu hello magazynu, wybierz hello wyboru toogrant partii zadań Azure dostępu toohello magazynu kluczy.

    c. **Grupa zasobów**: hello wybierz grupę zasobów, w którym został utworzony magazyn kluczy hello.

    d. **Lokalizacja**: hello region platformy Azure, w której utworzono hello magazynu kluczy dla konta wsadowego hello.

    e. **Konto magazynu** (opcjonalne): konto usługi Azure Storage ogólnego przeznaczenia skojarzone z kontem usługi Batch. Jest to zalecane w przypadku większości kont usługi Batch. Więcej szczegółów zamieszczono w sekcji [Połączone konto usługi Azure Storage](#linked-azure-storage-account) poniżej.

4. Kliknij przycisk **Utwórz** toocreate hello konta.

   Hello portal wskazuje, że wdrożenie jest w toku. Po zakończeniu w obszarze **Powiadomienia** pojawia się powiadomienie **Wdrożenie zakończyło się pomyślnie**.



## <a name="view-batch-account-properties"></a>Wyświetlanie właściwości konta usługi Batch
Po utworzeniu konta hello, możesz otworzyć hello **bloku konta usługi partia zadań** tooaccess jego ustawienia i właściwości. Za pomocą menu po lewej stronie powitania w bloku konta usługi partia zadań hello są dostępne wszystkie ustawienia konta i właściwości.

![Blok konta usługi Batch w witrynie Azure Portal][account_blade]

* **Adres URL konta wsadowego**: podczas opracowywania aplikacji przy użyciu hello [API partii](batch-apis-tools.md#azure-accounts-for-batch-development), będziesz potrzebować tooaccess adres URL konta wsadowego zasobów. Adres URL konta usługi partia zadań ma hello następującego formatu:

    `https://<account_name>.<region>.batch.azure.com`

![Adres URL konta usługi Batch w portalu][account_url]

* **Klucze dostępu** (tryb usługi partii): tooauthenticate tooyour dostępu do konta usługi partia zadań z aplikacji, musisz mieć klucz dostępu konta. (To ustawienie nie jest dostępne w trybie subskrypcji użytkownika, w którym używasz uwierzytelniania usługi Azure Active Directory).

    tooview lub regenerate kluczy dostępu do konta partii zadań, wprowadź `keys` w menu po lewej stronie powitania **wyszukiwania** w bloku konta usługi partia zadań hello, a następnie wybierz **klucze**.

    ![Klucze konta usługi Batch w witrynie Azure Portal][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Połączone konto usługi Azure Storage

Opcjonalnie możesz połączyć ogólnego przeznaczenia tooyour konta usługi Azure Storage konta usługi partia zadań. Witaj [pakietów aplikacji](batch-application-packages.md) funkcji partii używa magazynu obiektów Blob platformy Azure, podobnie jak hello [.NET konwencje pliku wsadowego](batch-task-output.md) biblioteki. Te funkcje opcjonalne ułatwiają wdrażanie aplikacji hello uruchamianych zadań wsadowych i trwałych danych hello, które oferują.

Zaleca się utworzenie nowego konta usługi Storage do wyłącznego użytku przez konto usługi Batch.

![Tworzenie konta magazynu ogólnego przeznaczenia][storage_account]

> [!NOTE]
> Partia zadań Azure aktualnie obsługuje tylko hello ogólnego przeznaczenia typu konta magazynu. Ten typ konta opisano w kroku 5 [Tworzenie konta magazynu] (../storage/common/storage-create-storage-account.md#create-a-storage-account) w artykule [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Należy zachować ostrożność, gdy trwa ponowne generowanie kluczy dostępu hello połączonego konta magazynu. Generuj tylko jeden klucz konta magazynu, a następnie kliknij przycisk **klucze synchronizacji** na powitania połączone bloku konto magazynu. Zaczekaj 5 minut tooallow hello klucze toopropagate toohello obliczeniowe węzłów w Twojej puli, a następnie ponownie wygenerować i zsynchronizować hello innego klucza, jeśli to konieczne. Jeśli ponownie wygenerować jednocześnie klawisze hello sam czas węzłów obliczeniowych nie będą mogli toosynchronize albo klucza i utracą konta magazynu toohello dostępu.
>
>

![Ponowne generowanie kluczy konta magazynu][4]

## <a name="batch-service-quotas-and-limits"></a>Limity przydziału i limity usługi Batch
Należy pamiętać, że jako z subskrypcją platformy Azure i Azure innych usług, niektóre [przydziały i limity](batch-quota-limit.md) zastosować tooBatch kont. Bieżący przydziałów dla konta usługi partia zadań wyświetlane w portalu hello na koncie hello **właściwości**.

![Limity przydziału konta usługi Batch w witrynie Azure Portal][quotas]



Ponadto wiele te przydziały można zwiększyć po prostu z żądania pomocy technicznej produktu wolnego przesłane w hello portalu Azure. Zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) szczegółowe informacje dotyczące żądania zwiększanie przydziału.

## <a name="other-batch-account-management-options"></a>Inne opcje zarządzania kontem usługi Batch
Ponadto toousing hello portalu Azure, można również tworzyć i zarządzanie kontami partii hello następujący:

* [Polecenia cmdlet programu PowerShell usługi Batch](batch-powershell-cmdlets-get-started.md)
* [Interfejs wiersza polecenia platformy Azure](batch-cli-get-started.md)
* [Batch Management .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>Następne kroki
* Zobacz hello [Przegląd funkcji partii](batch-api-basics.md) toolearn więcej informacji na temat partii pojęcia dotyczące usługi i funkcje. Hello artykule omówiono hello głównej partii zasobów takich jak pule, węzły obliczeniowe, zadań i zadań i zapoznać się z omówieniem hello funkcje usługi, które umożliwiają wykonanie obciążenie obliczeniowe na dużą skalę.
* Dowiedz się podstawy hello opracowanie aplikacji z obsługą usługi partia zadań przy użyciu hello [biblioteki klienta .NET partii](batch-dotnet-get-started.md) lub [Python](batch-python-tutorial.md). Te artykuły wprowadzające informacje pomocne przy działającą aplikację, która używa hello partii usługi tooexecute obciążenia na wielu węzłach obliczeniowych oraz oferuje, za pomocą usługi Azure Storage dla obciążenia pliku tymczasowego i pobierania.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Ponowne generowanie kluczy konta magazynu"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
