---
title: woluminy aaaManage na tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Zawiera opis hello Menedżera urządzeń StorSimple i jak toouse on toomanage woluminach macierzy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Użyj Menedżera urządzeń StorSimple usługi toomanage woluminy na powitania tablicy wirtualnego StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać woluminach macierzy wirtualnego StorSimple.

Witaj usługi Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello. Dodanie toomanaging udziałów i woluminów można użyć tooview usługi Menedżer StorSimple urządzenia hello i zarządzanie urządzeniami, wyświetlanie alertów i wyświetlić i zarządzanie zasad tworzenia kopii zapasowych i hello katalogu kopii zapasowej.

## <a name="volume-types"></a>Typy woluminu

Woluminy StorSimple można:

* **Przypięty lokalnie**: dane w tych woluminów pozostaje w macierzy hello przez cały czas i nie zostaną przeniesione toohello chmury.
* **Do warstwy**: dane w tych woluminów mogą zostaną przeniesione toohello chmury. Podczas tworzenia woluminu warstwowego około 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello. Na przykład jeśli udostępniane wolumin 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych. Z kolei oznacza to, że jeśli zabraknie wszystkie lokalne powitania miejsce na urządzeniu hello nie można dostarczać wolumin warstwowy (ponieważ hello 10% wymaganych na lokalne powitania warstwa nie będzie dostępna).

### <a name="provisioned-capacity"></a>Udostępnione pojemności
Można znaleźć w poniższej tabeli dla maksymalnej pojemności udostępnione dla każdego typu woluminu toohello.

| **Identyfikator limit**                                       | **Limit**     |
|------------------------------------------------------------|---------------|
| Minimalny rozmiar woluminu warstwowego                            | 500 GB        |
| Maksymalny rozmiar woluminu warstwowego                            | 5 TB          |
| Minimalny rozmiar woluminu przypiętego lokalnie                    | 50 GB         |
| Maksymalny rozmiar woluminu przypiętego lokalnie                    | 500 GB        |

## <a name="hello-volumes-blade"></a>Witaj woluminów bloku
Witaj **woluminów** menu w bloku podsumowania usługi StorSimple Wyświetla hello listę woluminów magazynu dla danej tablicy StorSimple i pozwala toomanage je.

![Blok woluminów](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Wolumin składa się z szeregu atrybuty:

* **Nazwa woluminu** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello woluminu.
* **Stan** — może być w trybie online lub offline. Jeśli wolumin jest w trybie offline, nie jest widoczne tooinitiators (serwery) dozwoloną dostępu toouse hello woluminu.
* **Typ** — wskazuje, czy wolumin hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.
* **Pojemność** — określa ilość hello danych używana jako porównaniu toohello łączna ilość danych, które mogą być przechowywane przez inicjatora hello (serwer).
* **Kopia zapasowa** — w przypadku, gdy z hello tablicy wirtualnego StorSimple, wszystkie woluminy są włączane automatycznie do utworzenia kopii zapasowej.
* **Połączone hosty** — określa hello inicjatorów (serwerów), które mają prawo dostępu toothis woluminu.

![Szczegóły ilości](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:

* Dodawanie woluminu
* Modyfikowanie woluminu
* Przełącz do trybu offline woluminu
* Usuwanie woluminu

## <a name="add-a-volume"></a>Dodawanie woluminu

1. Witaj StorSimple podsumowania bloku usługi, kliknij **+ Dodaj wolumin** z hello paska poleceń. Spowoduje to otwarcie zapasowej hello **Dodaj wolumin** bloku.
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. W hello **Dodaj wolumin** bloku hello następujące:
   
   * W hello **nazwa woluminu** wprowadź unikatową nazwę dla woluminu. Nazwa Hello musi być ciągiem o długości 3 znaków too127.
   * W hello **typu** listy rozwijanej liście, określ, czy toocreate **warstwowego** lub **przypięty lokalnie** woluminu. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **wolumin przypięty lokalnie**. Dla wszystkich innych danych wybierz **warstwowego** woluminu.
   * W hello **pojemności** Określ rozmiar hello hello woluminu. Wolumin warstwowy musi należeć do zakresu od 500 GB i 5 TB i woluminu przypiętego lokalnie musi należeć do zakresu od 50 GB i 500 GB.
   * * Kliknij przycisk **połączone hosty**, wybierz dostępu formantu rekordu (ACR) odpowiedniego toohello inicjatora iSCSI mają tooconnect toothis woluminu, a następnie kliknij przycisk **wybierz**.
3. tooadd połączonych nowego hosta, kliknij przycisk **Dodaj nowe**, wprowadź nazwę hosta hello i jego iSCSI kwalifikowana nazwa (IQN), a następnie kliknij przycisk **Dodaj**.
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Po zakończeniu konfigurowania woluminu, kliknij przycisk **Utwórz**. Wolumin zostanie utworzony z hello określonych ustawień i otrzymają powiadomienie na powitania pomyślnym utworzeniu hello takie same. Domyślnie kopia zapasowa zostanie włączona dla woluminu hello.
5. tooconfirm, który hello wolumin został toohello został pomyślnie utworzony, przejdź do pozycji **woluminów** bloku. Powinny pojawić się hello woluminu na liście.
   
    ![Powodzenie Tworzenie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Modyfikowanie woluminu

Zmodyfikuj woluminu, gdy będziesz potrzebować toochange hello hostów, które uzyskują dostęp do woluminu hello. Witaj inne atrybuty woluminu nie można zmodyfikować po utworzeniu hello woluminu.

#### <a name="toomodify-a-volume"></a>toomodify woluminu

1. Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się wolumin ma możesz toomodify.
2. **Wybierz** hello woluminu, a następnie kliknij przycisk **połączone hosty** tooview hello aktualnie podłączonego hosta i zmodyfikuj go tooa inny serwer.
   
    ![Edytuj woluminu](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Zapisz zmiany, klikając hello **zapisać** paska poleceń. Określony ustawienia będą stosowane i zostanie wyświetlone powiadomienie.

## <a name="take-a-volume-offline"></a>Przełącz do trybu offline woluminu

Może być konieczne tootake woluminu w trybie offline podczas planowania toomodify albo go usunąć go. Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu. Konieczne będzie tootake hello woluminu w trybie offline na hoście hello, a także na urządzeniu hello.

#### <a name="tootake-a-volume-offline"></a>tootake woluminu w trybie offline

1. Upewnij się, że w woluminie hello nie jest używany przed przełączeniem do trybu offline.
2. Zająć hello woluminu w trybie offline na hoście hello pierwszy. Eliminuje to potencjalne ryzyko uszkodzeniem danych na woluminie hello. Określone kroki można znaleźć toohello instrukcje dotyczące systemu operacyjnego hosta.
3. Po wolumin hello na hoście hello jest w trybie offline, należy podjąć hello woluminu w macierzy hello w trybie offline, wykonując następujące kroki hello:
   
   * Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello tablicy wirtualnych, na których hello znajduje się wolumin ma możesz tootake w trybie offline.
   * **Wybierz** hello woluminu, a następnie kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **przełączyć do trybu offline**.
     
        ![Wolumin w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Przejrzyj informacje hello w hello **przełączyć do trybu offline** bloku i potwierdzenie akceptacji hello operacji. Kliknij przycisk **przełączyć do trybu offline** tootake hello woluminu w trybie offline. Zostanie wyświetlone powiadomienie hello operacji w toku.
   * tooconfirm, który wolumin hello zostało pomyślnie przełączone do trybu offline, przejdź toohello **woluminów** bloku. Stan hello hello woluminu powinien być widoczny jako w trybie offline.
     
       ![Potwierdzenie woluminu w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Usuwanie woluminu

> [!IMPORTANT]
> Wolumin można usunąć tylko wtedy, gdy jest w trybie offline.
> 
> 

Wykonaj następujące kroki toodelete woluminu hello.

#### <a name="toodelete-a-volume"></a>toodelete woluminu

1. Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się wolumin ma możesz toodelete.
2. **Wybierz** hello woluminu, a następnie kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **usunąć**.
   
    ![Usuń wolumin](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Sprawdź stan hello woluminu hello ma toodelete. Jeśli wolumin hello ma toodelete nie jest w trybie offline, przełączyć go w trybie offline hello pierwszą, następujące kroki [Przełącz do trybu offline wolumin](#take-a-volume-offline).
4. Po wyświetleniu monitu o potwierdzenie w hello **usunąć** bloku, Zaakceptuj potwierdzenie hello i kliknij przycisk **usunąć**. Witaj wolumin zostanie usunięte i hello **woluminów** bloku wyświetli hello zaktualizować listę woluminów w tablicy wirtualnego hello.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[sklonować woluminu StorSimple](storsimple-virtual-array-clone.md).

