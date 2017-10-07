---
title: "aaaManage poświadczeń konta magazynu StorSimple dla urządzeń z serii StorSimple 8000 z aktualizacją Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak można użyć hello tooadd strona Konfigurowanie Menedżera urządzeń StorSimple, edycji, usuwania lub obracania hello kluczy zabezpieczeń dla konta magazynu."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Użyj toomanage usługi Menedżer StorSimple urządzenia hello poświadczeń konta magazynu

## <a name="overview"></a>Omówienie

Witaj **konfiguracji** części bloku usługi Menedżer StorSimple urządzenia hello przedstawia wszystkie parametry usługi global service hello, które mogą być tworzone w hello usługi Menedżer StorSimple urządzenia. Te parametry mogą być zastosowane tooall hello urządzenia połączone usługi toohello i obejmują:

* Poświadczenia konta magazynu
* Szablony przepustowości 
* Rekordy kontroli dostępu 

W tym samouczku wyjaśniono, jak tooadd, edytować, usuwać poświadczeń konta magazynu lub Obróć hello kluczy zabezpieczeń dla konta magazynu.

 ![Lista poświadczeń konta magazynu](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Konta magazynu zawierają hello poświadczenia, które hello tooaccess używa urządzenia StorSimple konta magazynu z dostawcy usług w chmurze. W przypadku kont magazynu Microsoft Azure są to poświadczenia, takie jak nazwa konta hello i hello podstawowy klucz dostępu. 

Na powitania **poświadczeń konta magazynu** bloku, wszystkie magazyny kont utworzonych dla hello rozliczeń subskrypcji, które są wyświetlane w formacie tabelarycznym zawierający hello następujących informacji:

* **Nazwa** — Witaj konta toohello nazwa przypisana podczas jego tworzenia.
* **Włączony protokół SSL** — czy hello jest włączony protokół SSL i urządzenia do chmury komunikacja odbywa się za pośrednictwem bezpiecznego kanału hello.
* **Używane przez** — Witaj wiele woluminów przy użyciu konta magazynu hello.

Hello najbardziej typowych zadań toostorage powiązane konta, które mogą być wykonywane są:

* Dodawanie konta magazynu 
* Edytuj konto magazynu 
* Usuwanie konta magazynu 
* Rotacją kluczy kont magazynu 

## <a name="types-of-storage-accounts"></a>Typy kont magazynu

Istnieją trzy typy kont magazynu, które mogą być używane z urządzenia StorSimple.

* **Konta magazynu automatycznie generowanej** — jak nazwa hello sugeruje, ten typ konta magazynu jest generowana automatycznie po utworzeniu hello usługi. toolearn więcej informacji na temat tworzenia tego konta magazynu, zobacz [krok 1: Tworzenie nowej usługi](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) w [wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md). 
* **Konta magazynu w ramach subskrypcji usługi hello** — są to hello kontami magazynu Azure, które są skojarzone z hello tej samej subskrypcji co hello usługi. toolearn więcej informacji na temat sposobu tworzenia tych kont magazynu, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md). 
* **Konta magazynu poza subskrypcji usługi hello** — są to hello kontami magazynu Azure, które nie są skojarzone z usługą i prawdopodobnie hello istniał już przed usługa została utworzona.

## <a name="add-a-storage-account"></a>Dodawanie konta magazynu

Można dodać konto magazynu, podając unikatową przyjazną nazwę i dostępu poświadczenia, które są połączone konta magazynu toohello (z hello określonej chmury dostawcy usług). Istnieje również opcja hello włączenia hello bezpiecznego sockets layer (SSL) trybu toocreate bezpiecznego kanału komunikacji sieciowej między urządzeniami i hello chmury.

Można utworzyć wiele kont dla określonej chmury dostawcy usług. Należy jednak pamiętać, że po utworzeniu konta magazynu nie można zmienić hello dostawcy usług w chmurze.

Przy zapisywaniu hello konta magazynu, usługa hello podejmuje próby toocommunicate przy użyciu dostawcy usługi w chmurze. w tej chwili będą uwierzytelniane poświadczenia Hello oraz hello dostępu materiałów, podane przez użytkownika. Konto magazynu jest tworzony tylko wtedy, gdy hello uwierzytelnianie zakończy się pomyślnie. W przypadku niepowodzenia uwierzytelniania hello następnie pojawi się odpowiedni komunikat o błędzie.

Użyj hello następujące poświadczenia konta magazynu Azure tooadd procedury:

* tooadd poświadczeń konta magazynu, który ma hello tej samej subskrypcji platformy Azure jako hello usługa Menedżera urządzeń
* tooadd znajduje się poza subskrypcji usługi w Menedżerze urządzeń hello poświadczenia konta magazynu platformy Azure

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd poświadczeń dla konta magazynu Azure poza subskrypcji usługi Menedżer StorSimple urządzenia hello

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji. Ta lista zawiera wszystkie istniejące poświadczeń konta magazynu skojarzone z hello usługi Menedżer StorSimple urządzenia.
3. Kliknij pozycję **Dodaj**.
4. W hello **dodać poświadczeń konta magazynu** bloku hello następujące:
   
    1. Aby uzyskać **subskrypcji**, wybierz pozycję **innych**.
   
    2. Podaj nazwę hello Twoje poświadczenia konta magazynu platformy Azure.
   
    3. W hello **klucz dostępu do konta magazynu** pole tekstowe, podaj hello podstawowy klucz dostępu dla użytkownika poświadczeń dla konta magazynu platformy Azure. tooget tego klucza, przejdź do usługi Azure Storage toohello wybierz Twoje poświadczenia konta magazynu i kliknij **zarządzania kluczami konta**. Można teraz kopiować hello podstawowy klucz dostępu.
   
    4. tooenable protokołu SSL, kliknij przycisk hello **włączyć** toocreate przycisk bezpiecznego kanału komunikacji sieciowej między chmury usługi i hello Menedżera urządzeń StorSimple. Kliknij przycisk hello **wyłączyć** przycisk tylko wtedy, gdy pracujesz w chmurze prywatnej.
   
    5. Kliknij pozycję **Dodaj**. Użytkownik jest powiadamiany po pomyślnym utworzeniu hello poświadczeń dla konta magazynu.

5. nowo utworzony Hello poświadczeń dla konta magazynu jest wyświetlany na hello bloku usługi Menedżer konfigurowania urządzenia StorSimple w obszarze **poświadczeń konta magazynu**.
   


## <a name="edit-a-storage-account"></a>Edytuj konto magazynu

Można edytować konto magazynu, który jest używany przez kontener woluminów. Po zmodyfikowaniu konta magazynu, który jest obecnie używany hello tylko pola toomodify dostępne jest hello klucz dostępu dla konta magazynu hello. Można podać hello nowy klucz dostępu do magazynu i Zapisz ustawienia hello zaktualizowane.

#### <a name="tooedit-a-storage-account"></a>tooedit konta magazynu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. W hello **konfiguracji** kliknij **poświadczeń konta magazynu**.

    ![Poświadczenia konta magazynu](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. W hello **poświadczeń konta magazynu** bloku, z listy hello poświadczeń konta magazynu, wybierz opcję i kliknij jeden mają tooedit hello. 

3. Można zmodyfikować hello **Włącz SSL** zaznaczenia. Możesz również kliknąć **więcej...**  , a następnie wybierz **toorotate klucza dostępu synchronizacji** kluczy dostępu konta magazynu. Przejdź za[klucza obrotu kont magazynu](#key-rotation-of-storage-accounts) uzyskać więcej informacji dotyczących sposobu tooperform klucza obrotu. Po zmodyfikowaniu ustawień powitania kliknij **zapisać**. 

    ![Zapisywanie poświadczeń konta magazynu edytowany](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. 

    ![Potwierdzenie zmiany](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

Ustawienia Hello będą aktualizowane i zapisywane dla konta magazynu. 

## <a name="delete-a-storage-account"></a>Usuwanie konta magazynu

> [!IMPORTANT]
> Konto magazynu można usunąć tylko wtedy, gdy nie jest on używany przez kontener woluminów. Jeśli konto magazynu jest używana przez kontener woluminów, najpierw usuń kontener woluminów hello, a następnie usuń hello skojarzone konto magazynu.

#### <a name="toodelete-a-storage-account"></a>toodelete konta magazynu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. W hello **konfiguracji** kliknij **poświadczeń konta magazynu**.

2. Witaj tabelarycznych listy kont magazynu umieść kursor nad konta hello, że chcesz toodelete. Kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke, a następnie kliknij przycisk **usunąć**.

    ![Usuń poświadczenia konta magazynu](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toocontinue z hello usunięcia. Hello tabelarycznej listę zostaną zaktualizowane tooreflect hello zmiany.

    ![Potwierdzenie usunięcia](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Rotacją kluczy kont magazynu

Ze względów bezpieczeństwa klucza obrotu często jest to wymagane w centrach danych. Każda subskrypcja Microsoft Azure może mieć co najmniej jeden skojarzone konta magazynu. kontami toothese dostępu Hello jest kontrolowana przez hello subskrypcji i klucze dostępu dla każdego konta magazynu. 

Podczas tworzenia konta magazynu Microsoft Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane do uwierzytelniania podczas uzyskiwania dostępu do konta magazynu hello. Mając dwa klucze dostępu do magazynu umożliwia tooregenerate hello kluczy bez przeszkód tooyour magazynu usługi i usługa toothat dostępu. Witaj klucz, który jest aktualnie używany jest hello *głównej* klucz kopii zapasowej klucza i hello jest hello tooas określonego *dodatkowej* klucza. Gdy urządzenia Microsoft Azure StorSimple uzyskuje dostęp do dostawcy usługi w chmurze magazynu należy podać jedną z tych dwóch kluczy.

## <a name="what-is-key-rotation"></a>Co to jest rotacją kluczy?

Zazwyczaj aplikacji używać, tylko jednej hello tooaccess kluczy danych. Po upływie pewnego czasu program może przełączyć się toousing hello drugi klucz aplikacji. Po przełączeniu klucza pomocniczego toohello aplikacji, można wycofać hello pierwszy klucz, a następnie wygeneruj nowy klucz. Za pomocą dwóch kluczy hello w ten sposób umożliwia danych toohello dostępu do aplikacji bez jakiegokolwiek przestoju.

klucze konta magazynu Hello zawsze są przechowywane w usłudze hello w postaci zaszyfrowanej. Jednak te można zresetować za pośrednictwem hello usługi Menedżer StorSimple urządzenia. Usługa Hello można pobrać hello klucz podstawowy i klucz pomocniczy dla hello wszystkich kont magazynu w hello tej samej subskrypcji, w tym kont utworzonych w hello usługi magazynu, a także konta magazynu domyślne hello generowane podczas hello Menedżer urządzenia StorSimple Usługa najpierw został utworzony. Hello usługi Menedżer StorSimple urządzenia będzie zawsze pobiera klucze z hello klasycznego portalu Azure i przechowywać je w sposób zaszyfrowany.

## <a name="rotation-workflow"></a>Obracanie przepływu pracy

Administratora programu Microsoft Azure można ponownie wygenerować lub zmienić klucz podstawowy lub pomocniczy hello bezpośredni dostęp do konta magazynu hello (za pomocą hello usługi Magazyn Microsoft Azure). automatycznie Hello usługi Menedżer StorSimple urządzenia nie widzieć tej zmiany.

tooinform hello usługi Menedżer urządzeń StorSimple hello zmiany, konieczne będzie usługi Menedżer StorSimple urządzenia hello tooaccess, uzyskać dostęp do konta magazynu hello, a następnie zsynchronizować klucz podstawowy lub pomocniczy hello (w zależności od tego, który został zmieniony). Następnie usługa Hello pobiera hello najnowszego klucza, szyfruje hello kluczy i wysyła hello zaszyfrowane klucza toohello urządzenia.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>toosynchronize klucze kont magazynu w hello tej samej subskrypcji co hello usługi 
1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. W hello **konfiguracji** kliknij **poświadczeń konta magazynu**.
2. Witaj tabelarycznej listę kont magazynu, kliknij hello jedną, które mają toomodify. 

    ![Synchronizowanie kluczy](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Kliknij przycisk **... Więcej** , a następnie wybierz **toorotate klucza dostępu synchronizacji**.   

    ![Synchronizowanie kluczy](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Hello usługi Menedżer StorSimple urządzenia należy tooupdate hello klucz, który wcześniej został zmieniony w hello usługi Magazyn Microsoft Azure. Jeśli hello podstawowy klucz dostępu została zmieniona (wygenerowano ponownie), wybierz **głównej** klucza. Jeśli hello klucz pomocniczy został zmieniony, wybierz **dodatkowej** klucza. Kliknij przycisk **klucza synchronizacji**.
      
      ![Synchronizowanie kluczy](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Po klucz hello pomyślnie sycnhronized, otrzymasz powiadomienie.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize kluczy dla konta magazynu poza hello subskrypcji usługi
1. Na powitania **usług** kliknij przycisk hello **Konfiguruj** kartę.
2. Kliknij przycisk **Dodawanie/edytowanie konta magazynu**.
3. Okno dialogowe hello hello następujące:
   
   1. Wybierz hello konto magazynu z kluczem dostępu hello, które mają tooupdate.
   2. Konieczne będzie klucz dostępu do magazynu hello tooupdate w hello usługi Menedżer StorSimple urządzenia. W takim przypadku można wyświetlić klucz dostępu do magazynu hello. Wprowadź nowy klucz hello w hello **klucz dostępu do konta magazynu** pole. 
   3. Zapisz zmiany. Należy teraz zaktualizować klucz dostępu konta magazynu.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-8000-security.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

