---
title: aaaManage Twojego konta magazynu StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak można użyć hello tooadd strona Konfigurowanie Menedżera StorSimple, edycji, usuwania lub obracania hello kluczy zabezpieczeń dla konta magazynu."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Użyj toomanage usługi Menedżer StorSimple hello konta magazynu
## <a name="overview"></a>Omówienie
Witaj **Konfiguruj** strona przedstawia wszystkie parametry usługi global service hello, które mogą być tworzone w hello usługi Menedżer StorSimple. Te parametry mogą być zastosowane tooall hello urządzenia połączone usługi toohello i obejmują:

* Konta magazynu 
* Szablony przepustowości 
* Rekordy kontroli dostępu 

W tym samouczku opisano, jak używasz hello **Konfiguruj** strony tooadd, edytowania i usuwania konta magazynu lub Obróć hello kluczy zabezpieczeń dla konta magazynu.

 ![Konfigurowanie strony](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Konta magazynu zawierają hello poświadczenia, które hello urządzenia tooaccess używa konta magazynu z dostawcy usług w chmurze. W przypadku kont magazynu Microsoft Azure są to poświadczenia, takie jak nazwa konta hello i hello podstawowy klucz dostępu. 

Na powitania **Konfiguruj** stronę, wszystkie magazyny kont utworzonych dla hello rozliczeń subskrypcji, które są wyświetlane w formacie tabelarycznym zawierający hello następujących informacji:

* **Nazwa** — Witaj konta toohello nazwa przypisana podczas jego tworzenia.
* **Włączony protokół SSL** — czy hello jest włączony protokół SSL i urządzenia do chmury komunikacja odbywa się za pośrednictwem bezpiecznego kanału hello.
* **Używane przez** — Witaj wiele woluminów przy użyciu konta magazynu hello.

Hello najbardziej typowe zadania związane z toostorage kont, które mogą być wykonywane na powitania **Konfiguruj** są:

* Dodawanie konta magazynu 
* Edytuj konto magazynu 
* Usuwanie konta magazynu 
* Rotacją kluczy kont magazynu 

## <a name="types-of-storage-accounts"></a>Typy kont magazynu
Istnieją trzy typy kont magazynu, które mogą być używane z urządzenia StorSimple.

* **Konta magazynu automatycznie generowanej** — jak nazwa hello sugeruje, ten typ konta magazynu jest generowana automatycznie po utworzeniu hello usługi. toolearn więcej informacji na temat tworzenia tego konta magazynu, zobacz [krok 1: Tworzenie nowej usługi](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) w [wdrażanie lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough.md). 
* **Konta magazynu w ramach subskrypcji usługi hello** — są to hello kontami magazynu Azure, które są skojarzone z hello tej samej subskrypcji co hello usługi. toolearn więcej informacji na temat sposobu tworzenia tych kont magazynu, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md). 
* **Konta magazynu poza subskrypcji usługi hello** — są to hello kontami magazynu Azure, które nie są skojarzone z usługą i prawdopodobnie hello istniał już przed usługa została utworzona.

## <a name="add-a-storage-account"></a>Dodawanie konta magazynu
Można dodać konto magazynu, podając unikatową przyjazną nazwę i dostępu poświadczenia, które są połączone konta magazynu toohello (z hello określonej chmury dostawcy usług). Istnieje również opcja hello włączenia hello bezpiecznego sockets layer (SSL) trybu toocreate bezpiecznego kanału komunikacji sieciowej między urządzeniami i hello chmury.

Można utworzyć wiele kont dla określonej chmury dostawcy usług. Należy jednak pamiętać, że po utworzeniu konta magazynu nie można zmienić hello dostawcy usług w chmurze.

Przy zapisywaniu hello konta magazynu, usługa hello podejmuje próby toocommunicate przy użyciu dostawcy usługi w chmurze. w tej chwili będą uwierzytelniane poświadczenia Hello oraz hello dostępu materiałów, podane przez użytkownika. Konto magazynu jest tworzony tylko wtedy, gdy hello uwierzytelnianie zakończy się pomyślnie. W przypadku niepowodzenia uwierzytelniania hello następnie pojawi się odpowiedni komunikat o błędzie.

Menedżer zasobów kont magazynu utworzonych w portalu Azure również są obsługiwane z StorSimple. Witaj Menedżera zasobów kont magazynu nie pojawi się na liście rozwijanej hello do wyboru podczas próby toocreate kontener woluminów hello tylko magazyn kont utworzonych w hello klasycznego portalu Azure zostaną wyświetlone. Menedżer zasobów konta magazynu należy toobe dodane przy użyciu tooadd procedury hello konta magazynu opisane poniżej.

> [!NOTE]
> Procedura Hello dodawania konta magazynu różni się pod względem wersji oprogramowania StorSimple hello są używane. Należy się toofollow hello prawidłowe procedury dla danej wersji StorSimple.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Edytuj konto magazynu
Można edytować konto magazynu, który jest używany przez kontener woluminów. Po zmodyfikowaniu konta magazynu, który jest obecnie używany hello tylko pola toomodify dostępne jest hello klucz dostępu dla konta magazynu hello. Można podać hello nowy klucz dostępu do magazynu i Zapisz ustawienia hello zaktualizowane.

#### <a name="tooedit-a-storage-account"></a>tooedit konta magazynu
1. Strona docelowa usługi hello, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij **Konfiguruj**.
2. Kliknij przycisk **Dodawanie/edytowanie konta magazynu**.
3. W hello **Dodawanie/edytowanie konta magazynu** okno dialogowe:
   
   1. W polu listy rozwijanej hello **kont magazynu**, wybrać istniejące konto, które chcesz toomodify. Może to także dotyczyć hello kontach magazynu, które zostały automatycznie generowane, gdy usługa hello najpierw została utworzona.
   2. Jeśli to konieczne, można zmodyfikować hello **Włącz tryb SSL** zaznaczenia.
   3. Możesz wybrać toorotate kluczy dostępu konta magazynu. Zobacz [klucza obrotu kont magazynu](#key-rotation-of-storage-accounts) uzyskać więcej informacji dotyczących sposobu tooperform klucza obrotu.
   4. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave hello ustawienia. Ustawienia Hello zostaną zaktualizowane na powitania **Konfiguruj** strony. Kliknij przycisk **zapisać** toosave hello nowo zaktualizowano ustawienia.
      
      ![Edytuj konto magazynu](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Usuwanie konta magazynu
> [!IMPORTANT]
> Konto magazynu można usunąć tylko wtedy, gdy nie jest on używany przez kontener woluminów. Jeśli konto magazynu jest używana przez kontener woluminów, najpierw usuń kontener woluminów hello, a następnie usuń hello skojarzone konto magazynu.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete konta magazynu
1. Na powitania strona docelowa usługi Menedżer StorSimple, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij **Konfiguruj**.
2. Witaj tabelarycznych listy kont magazynu umieść kursor nad konta hello, że chcesz toodelete.
3. Ikona usuwania (**x**) będą wyświetlane w hello extreme prawej kolumnie dla tego konta magazynu. Kliknij przycisk hello **x** ikonę toodelete hello poświadczeń.
4. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toocontinue z hello usunięcia. Hello tabelarycznej listę zostaną zaktualizowane tooreflect hello zmiany.

## <a name="key-rotation-of-storage-accounts"></a>Rotacją kluczy kont magazynu
Ze względów bezpieczeństwa klucza obrotu często jest to wymagane w centrach danych. 

> [!NOTE]
> Hello następujących kluczowych informacji i hello obrotu procedury zastosować tooMicrosoft tylko konta magazynu platformy Azure. Jeśli korzystasz z innego dostawcy usług w chmurze, można zarządzać klucze konta magazynu za pośrednictwem pulpitu nawigacyjnego tego dostawcy.
> 
> 

Każda subskrypcja Microsoft Azure może mieć co najmniej jeden skojarzone konta magazynu. kontami toothese dostępu Hello jest kontrolowana przez hello subskrypcji i klucze dostępu dla każdego konta magazynu. 

Podczas tworzenia konta magazynu Microsoft Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane do uwierzytelniania podczas uzyskiwania dostępu do konta magazynu hello. Mając dwa klucze dostępu do magazynu umożliwia tooregenerate hello kluczy bez przeszkód tooyour magazynu usługi i usługa toothat dostępu. Witaj klucz, który jest aktualnie używany jest hello *głównej* klucz kopii zapasowej klucza i hello jest hello tooas określonego *dodatkowej* klucza. Gdy urządzenia Microsoft Azure StorSimple uzyskuje dostęp do dostawcy usługi w chmurze magazynu należy podać jedną z tych dwóch kluczy.

## <a name="what-is-key-rotation"></a>Co to jest rotacją kluczy?
Zazwyczaj aplikacji używać, tylko jednej hello tooaccess kluczy danych. Po upływie pewnego czasu program może przełączyć się toousing hello drugi klucz aplikacji. Po przełączeniu klucza pomocniczego toohello aplikacji, można wycofać hello pierwszy klucz, a następnie wygeneruj nowy klucz. Za pomocą dwóch kluczy hello w ten sposób umożliwia danych toohello dostępu do aplikacji bez jakiegokolwiek przestoju.

klucze konta magazynu Hello zawsze są przechowywane w usłudze hello w postaci zaszyfrowanej. Jednak te można zresetować za pośrednictwem hello usługi Menedżer StorSimple. Usługa Hello można pobrać hello klucz podstawowy i klucz pomocniczy dla hello wszystkich kont magazynu w hello tej samej subskrypcji, w tym kont utworzonych w hello usługi magazynu, a także konta magazynu domyślne hello generowane podczas hello usługi Menedżer StorSimple Usługa najpierw została utworzona. Hello usługi Menedżer StorSimple będzie zawsze pobiera klucze z hello klasycznego portalu Azure i przechowywać je w sposób zaszyfrowany.

## <a name="rotation-workflow"></a>Obracanie przepływu pracy
Administratora programu Microsoft Azure można ponownie wygenerować lub zmienić klucz podstawowy lub pomocniczy hello bezpośredni dostęp do konta magazynu hello (za pomocą hello usługi Magazyn Microsoft Azure). automatycznie Hello usługi Menedżer StorSimple nie widzieć tej zmiany.

usługi Menedżer StorSimple hello tooinform hello zmiany, konieczne będzie tooaccess hello usługi Menedżer StorSimple, uzyskać dostęp do konta magazynu hello, a następnie zsynchronizować klucz podstawowy lub pomocniczy hello (w zależności od tego, który został zmieniony). Następnie usługa Hello pobiera hello najnowszego klucza, szyfruje hello kluczy i wysyła hello zaszyfrowane klucza toohello urządzenia.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize klucze kont magazynu w hello tej samej subskrypcji co usługa hello (tylko wersja Azure)
1. Na powitania **usług** kliknij przycisk hello **Konfiguruj** kartę.
2. Kliknij przycisk **Dodawanie/edytowanie konta magazynu**.
3. Okno dialogowe hello hello następujące:
   
   1. Wybierz hello konto magazynu z kluczem hello, które mają toosynchronize. klucze konta magazynu Hello są szyfrowane, gdy są one wyświetlane.
   2. Hello usługi Menedżer StorSimple należy tooupdate hello klucz, który wcześniej został zmieniony w hello usługi Magazyn Microsoft Azure. Jeśli hello podstawowy klucz dostępu została zmieniona (wygenerowano ponownie), kliknij przycisk **zsynchronizować klucz podstawowy**. Klucz pomocniczy hello został zmieniony, kliknij przycisk **synchronizowanie klucza pomocniczego**.
      
      ![Synchronizowanie kluczy](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize kluczy dla konta magazynu poza hello subskrypcji usługi
1. Na powitania **usług** kliknij przycisk hello **Konfiguruj** kartę.
2. Kliknij przycisk **Dodawanie/edytowanie konta magazynu**.
3. Okno dialogowe hello hello następujące:
   
   1. Wybierz hello konto magazynu z kluczem dostępu hello, które mają tooupdate.
   2. Konieczne będzie klucz dostępu do magazynu hello tooupdate w hello usługi Menedżer StorSimple. W takim przypadku można wyświetlić klucz dostępu do magazynu hello. Wprowadź nowy klucz hello w hello **klucz dostępu do konta magazynu**y pole. 
   3. Zapisz zmiany. Należy teraz zaktualizować klucz dostępu konta magazynu.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-security.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

