---
title: "poświadczenia konta magazynu tablicy wirtualnego StorSimple aaaManage | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak można użyć hello tooadd strona Konfigurowanie Menedżera urządzeń StorSimple, edycji, usuwania lub obracania hello kluczy zabezpieczeń dla poświadczeń konta magazynu skojarzone z hello tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Użyj Menedżera urządzeń StorSimple toomanage poświadczeń konta magazynu dla macierzy wirtualnego StorSimple

## <a name="overview"></a>Omówienie
Witaj **konfiguracji** części bloku usługi Menedżer StorSimple urządzenia hello macierzy wirtualnego StorSimple przedstawia hello usługi global service parametrów, które mogą być tworzone w hello usługi Menedżer StorSimple. Te parametry mogą być zastosowane tooall hello urządzenia połączone usługi toohello i obejmują:

* Poświadczenia konta magazynu
* Rekordy kontroli dostępu
  
  ![Pulpit nawigacyjny usługi Menedżera urządzeń](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

W tym samouczku wyjaśniono, jak można dodać, edytować lub usunąć poświadczeń konta magazynu dla macierzy wirtualne StorSimple. Witaj informacje w tym samouczku dotyczy tylko toohello tablicy wirtualne StorSimple. Informacje dotyczące sposobu kont magazynu toomanage w serii 8000 znajdują się w temacie [Użyj hello toomanage usługi Menedżer StorSimple konta magazynu](storsimple-manage-storage-accounts.md).

Konto magazynu poświadczeń zawierają hello poświadczenia, które hello urządzenie używa tooaccess konta magazynu z dostawcy usług w chmurze. W przypadku kont magazynu Microsoft Azure są to poświadczenia, takie jak nazwa konta hello i hello podstawowy klucz dostępu.

Na powitania **poświadczeń konta magazynu** bloku, wszystkie konta magazynu poświadczeń, które są tworzone dla hello rozliczeń subskrypcji są wyświetlane w formacie tabelarycznym zawierający hello następujących informacji:

* **Nazwa** — Witaj konta toohello nazwa przypisana podczas jego tworzenia.
* **Włączony protokół SSL** — czy hello jest włączony protokół SSL i urządzenia do chmury komunikacja odbywa się za pośrednictwem bezpiecznego kanału hello.
  
  ![Sekcja konfiguracji](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

Hello najbardziej typowe zadania związane z toostorage poświadczenia konta, które można wykonać na powitania **poświadczeń konta magazynu** bloku są:

* Dodawanie poświadczeń konta magazynu
* Edytowanie poświadczeń konta magazynu
* Usuń poświadczenia konta magazynu

## <a name="types-of-storage-account-credentials"></a>Typy poświadczeń konta magazynu
Istnieją trzy typy poświadczeń konta magazynu, które mogą być używane z urządzenia StorSimple.

* **Poświadczenia konta magazynu automatycznie generowanej** — jak nazwa hello sugeruje, ten typ poświadczeń dla konta magazynu jest generowana automatycznie po utworzeniu hello usługi. toolearn więcej informacji na temat sposobu tworzenia poświadczeń dla tego konta magazynu, zobacz [Utwórz nową usługę](storsimple-virtual-array-manage-service.md#create-a-service).
* **poświadczenia konta magazynu w ramach subskrypcji usługi hello** — są to konto magazynu Azure hello poświadczenia, które są skojarzone z hello tej samej subskrypcji co hello usługi. toolearn więcej informacji na temat sposobu tworzenia tych poświadczeń konta magazynu, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).
* **poświadczenia konta magazynu poza subskrypcji usługi hello** — są to hello poświadczeń konta magazynu platformy Azure, które nie są skojarzone z usługą i prawdopodobnie hello istniał już przed usługa została utworzona.

## <a name="add-a-storage-account-credential"></a>Dodawanie poświadczeń konta magazynu
Konfiguracja usługi Menedżer StorSimple urządzenia tooyour poświadczenia magazynu konta można dodać, podając unikatową przyjazną nazwę i dostępu poświadczenia, które są połączone konta magazynu toohello. Istnieje również opcja hello włączenia hello bezpiecznego sockets layer (SSL) trybu toocreate bezpiecznego kanału komunikacji sieciowej między urządzeniami i hello chmury.

Można utworzyć wiele kont dla określonej chmury dostawcy usług. Przy zapisywaniu hello poświadczeń dla konta magazynu, usługa hello podejmuje próby toocommunicate przy użyciu dostawcy usługi w chmurze. poświadczenia Hello i materiał dostępu hello podane są uwierzytelniani w tej chwili. Poświadczenia konta magazynu jest tworzony tylko wtedy, gdy hello uwierzytelnianie zakończy się pomyślnie. W przypadku niepowodzenia uwierzytelniania hello odpowiedni komunikat o błędzie jest wyświetlany.

Użyj hello następujące poświadczenia konta magazynu Azure tooadd procedury:

* tooadd poświadczeń konta magazynu, który ma hello tej samej subskrypcji platformy Azure jako hello usługa Menedżera urządzeń
* tooadd znajduje się poza subskrypcji usługi w Menedżerze urządzeń hello poświadczenia konta magazynu platformy Azure

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd poświadczeń konta magazynu, który ma hello tej samej subskrypcji platformy Azure jako hello usługa Menedżera urządzeń

1. Przejdź tooyour usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji.
3. Kliknij pozycję **Dodaj**.
4. W hello **dodawania konta magazynu** bloku hello następujące:
   
    1. Aby uzyskać **subskrypcji**, wybierz pozycję **bieżącego**.
    2. Podaj nazwę hello konta magazynu Azure.
    3. Wybierz **włączyć** toocreate bezpiecznego kanału komunikacji sieciowej między chmury urządzenia i hello StorSimple. Wybierz **wyłączyć** tylko wtedy, gdy pracujesz w chmurze prywatnej.
    4. Kliknij pozycję **Dodaj**. Użytkownik jest powiadamiany po pomyślnym utworzeniu konta magazynu hello.<br></br>
   
        ![Dodawanie istniejących poświadczeń dla konta magazynu](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd znajduje się poza subskrypcji usługi w Menedżerze urządzeń hello poświadczenia konta magazynu platformy Azure

1. Przejdź tooyour usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji. Ta lista zawiera wszystkie istniejące poświadczeń konta magazynu skojarzone z hello usługi Menedżer StorSimple urządzenia.
3. Kliknij pozycję **Dodaj**.
4. W hello **dodawania konta magazynu** bloku hello następujące:
   
    1. Aby uzyskać **subskrypcji**, wybierz pozycję **innych**.
   
    2. Podaj nazwę hello Twoje poświadczenia konta magazynu platformy Azure.
   
    3. W hello **klucz dostępu do konta magazynu** pole tekstowe, podaj hello podstawowy klucz dostępu dla użytkownika poświadczeń dla konta magazynu platformy Azure. tooget tego klucza, przejdź do usługi Azure Storage toohello wybierz Twoje poświadczenia konta magazynu i kliknij **zarządzania kluczami konta**. Można teraz kopiować hello podstawowy klucz dostępu.
   
    4. tooenable protokołu SSL, kliknij przycisk hello **włączyć** toocreate przycisk bezpiecznego kanału komunikacji sieciowej między chmury usługi i hello Menedżera urządzeń StorSimple. Kliknij przycisk hello **wyłączyć** przycisk tylko wtedy, gdy pracujesz w chmurze prywatnej.
   
    5. Kliknij pozycję **Dodaj**. Użytkownik jest powiadamiany po pomyślnym utworzeniu hello poświadczeń dla konta magazynu.

5. nowo utworzony Hello poświadczeń dla konta magazynu jest wyświetlany na hello bloku usługi Menedżer konfigurowania urządzenia StorSimple w obszarze **poświadczeń konta magazynu**.
   
    ![Dodawanie poświadczeń konta magazynu, poza hello subskrypcji usługi w Menedżerze urządzeń](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Edytowanie poświadczeń konta magazynu
Można edytować poświadczeń konta magazynu używane przez urządzenia. Po zmodyfikowaniu poświadczeń konta magazynu, który jest obecnie używany toomodify dostępne pola hello są hello klucz dostępu i hello trybie protokołu SSL dla hello poświadczeń dla konta magazynu. Można podać hello nowy klucz dostępu do magazynu lub zmodyfikować hello **tryb Włącz SSL** wybór i Zapisz ustawienia hello zaktualizowane.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit poświadczeń konta magazynu
1. Przejdź tooyour usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji. Ta lista zawiera wszystkie istniejące poświadczeń konta magazynu skojarzone z hello usługi Menedżer StorSimple urządzenia.
3. Hello listy tabelarycznej poświadczeń konta magazynu wybierz, a następnie kliknij dwukrotnie ikonę hello konta, które ma toomodify.
4. W poświadczeń dla konta magazynu hello **właściwości** bloku hello następujące:
   
   1. Jeśli to konieczne, można zmodyfikować hello **Włącz SSL** wybór trybu.
   2. Możesz wybrać tooregenerate klucze dostępu do poświadczeń konta magazynu. Aby uzyskać więcej informacji, zobacz [ponownie wygenerować kluczy konta magazynu hello](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Podaj klucz poświadczeń konta magazynu hello nowe. W przypadku konta magazynu Azure jest hello podstawowy klucz dostępu.
   3. Kliknij przycisk **zapisać** u góry hello hello **właściwości** ustawienia hello toosave bloku. Aktualizowanie ustawień Hello na powitania **poświadczeń konta magazynu** bloku.
      
      ![Edytowanie poświadczeń konta magazynu](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Usuń poświadczenia konta magazynu
> [!IMPORTANT]
> Poświadczenia konta magazynu można usunąć tylko wtedy, gdy nie jest używany. Jeśli poświadczenia konta magazynu jest używana, użytkownik jest powiadamiany.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete poświadczeń konta magazynu
1. Przejdź tooyour usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji. Ta lista zawiera wszystkie istniejące poświadczeń konta magazynu skojarzone z hello usługi Menedżer StorSimple urządzenia.
3. Hello listy tabelarycznej poświadczeń konta magazynu wybierz, a następnie kliknij dwukrotnie ikonę hello konta, które ma toodelete.
4. W poświadczeń dla konta magazynu hello **właściwości** bloku hello następujące:
   
   1. Kliknij przycisk **usunąć** toodelete hello poświadczeń.
   2. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toocontinue z hello usunięcia. Lista tabelarycznym Hello jest zaktualizowane tooreflect hello zmian.
      
      ![Usuń poświadczenia konta magazynu](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Synchronizowanie kluczy dostępu do poświadczeń konta magazynu
Ze względów bezpieczeństwa klucza obrotu często jest to wymagane w centrach danych. Administratora programu Microsoft Azure można ponownie wygenerować lub zmienić klucz podstawowy lub pomocniczy hello bezpośredni dostęp do poświadczeń konta magazynu hello (za pośrednictwem hello usługi Magazyn Microsoft Azure). automatycznie Hello usługi Menedżer StorSimple urządzenia nie widzieć tej zmiany.

tooinform hello usługi Menedżer urządzeń StorSimple hello zmiany, należy usługi Menedżer StorSimple urządzenia hello tooaccess, dostęp do magazynu hello poświadczenia konta, a następnie zsynchronizować klucz podstawowy lub pomocniczy hello (w zależności od tego, który został zmieniony). Następnie usługa Hello pobiera hello najnowszego klucza, szyfruje hello kluczy i wysyła hello zaszyfrowane klucza toohello urządzenia.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>klucze toosynchronize poświadczeń konta magazynu w hello tej samej subskrypcji co usługa hello (tylko wersja Azure)
1. W bloku docelowej usługi hello, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie na stronie powitania **konfiguracji** kliknij **poświadczeń konta magazynu**.
2. Na powitania **poświadczeń konta magazynu** bloku hello listy poświadczeń konta magazynu, wybierz poświadczeń dla konta magazynu hello której klucze, które mają toosynchronize.
3. W hello **właściwości** bloku hello wybrane poświadczeń dla konta magazynu, hello następujące:
   
    1. Kliknij przycisk **więcej**, a następnie kliknij przycisk **klucz dostępu synchronizacji**.
   
    2. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **klucza synchronizacji** toocomplete hello synchronizacji.
    
4. Hello usługi Menedżer StorSimple urządzenia należy tooupdate hello klucz, który wcześniej został zmieniony w hello usługi Magazyn Microsoft Azure. W hello **klucz konta magazynu Synchronizuj** bloku hello podstawowy klucz dostępu został zmieniony (wygenerowano ponownie), kliknij przycisk podstawowym, a następnie kliknij **klucza synchronizacji**. Klucz pomocniczy hello został zmieniony, kliknij przycisk **dodatkowej**, a następnie kliknij przycisk **klucza synchronizacji**.
   
    ![Klucz dostępu do synchronizacji](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

