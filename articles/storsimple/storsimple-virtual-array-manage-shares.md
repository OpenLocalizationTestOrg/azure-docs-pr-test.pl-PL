---
title: "udostępnia tablicy wirtualnego StorSimple aaaManage | Dokumentacja firmy Microsoft"
description: "Zawiera opis hello Menedżera urządzeń StorSimple i jak toouse on toomanage udziałów na tablica wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Użyj udziałów toomanage usługi Menedżer StorSimple urządzenia hello na powitania tablicy wirtualnego StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać udziałami w macierzy wirtualne StorSimple.

Witaj usługi Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello. Dodanie toomanaging udziałów i woluminów można użyć tooview usługi Menedżer StorSimple urządzenia hello i zarządzanie urządzeniami, wyświetlanie alertów, zarządzania zasad tworzenia kopii zapasowych oraz zarządzania hello katalogu kopii zapasowej.

## <a name="share-types"></a>Typy udziału

Udziały StorSimple można:

* **Przypięty lokalnie**: dane w tych udziałach pozostaje w macierzy hello przez cały czas i nie zostaną przeniesione toohello chmury.
* **Do warstwy**: dane w tych udziałach można zostaną przeniesione toohello chmury. Podczas tworzenia udziału warstwowych około 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello. Na przykład jeśli udostępniane udziału 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych. Z kolei oznacza to, że jeśli zabraknie wszystkie lokalne powitania miejsce na urządzeniu hello nie można dostarczać warstwowych udziału (ponieważ hello 10% wymaganych na lokalne powitania warstwa nie będzie dostępna).

### <a name="provisioned-capacity"></a>Udostępnione pojemności

Można znaleźć w poniższej tabeli dla maksymalnej pojemności udostępnione dla każdego typu udziału toohello.

| **Identyfikator limit** | **Limit** |
| --- | --- |
| Minimalny rozmiar udziału warstwowych |500 GB |
| Maksymalny rozmiar udziału warstwowych |20 TB |
| Minimalny rozmiar udziału przypiętych lokalnie |50 GB |
| Maksymalny rozmiar udziału przypiętych lokalnie |2 TB |

## <a name="hello-shares-blade"></a>Witaj udziałów bloku

Witaj **udziałów** menu w bloku podsumowania usługi StorSimple Wyświetla listę hello udziałów magazynu w danej macierzy StorSimple i pozwala toomanage je.

![Udziałów bloku](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Udział składa się z szeregu atrybuty:

* **Nazwa udziału** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello udziału.
* **Stan** — może być w trybie online lub offline. Jeśli udział jest w trybie offline, użytkownicy udziału hello nie będą mogli tooaccess go.
* **Typ** — wskazuje, czy udział hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.
* **Pojemność** — określa ilość hello danych używana jako porównaniu toohello łączna ilość danych, które mogą być przechowywane w udziale hello.
* **Opis elementu** — ustawienie opcjonalne pomaga opisano hello udziału.
* **Uprawnienia** -udziału toohello uprawnienia systemu plików NTFS hello, którymi można zarządzać za pomocą Eksploratora Windows.
* **Kopia zapasowa** — w przypadku, gdy z hello tablicy wirtualnego StorSimple, wszystkie udziały są włączane automatycznie do kopii zapasowej.

![Udostępnia szczegóły](./media/storsimple-virtual-array-manage-shares/share-details.png)

Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:

* Dodawanie udziału
* Modyfikowanie udziału
* Przełącz do trybu offline udziału
* Usuń udział

## <a name="add-a-share"></a>Dodawanie udziału

1. Witaj StorSimple podsumowania bloku usługi, kliknij **+ Dodaj udział** z hello paska poleceń. Spowoduje to otwarcie zapasowej hello **Dodaj udział** bloku.

    ![Dodaj udział](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. W hello **Dodaj udział** bloku hello następujące:
   
    1. W hello **nazwa udziału** wprowadź unikatową nazwę udziału użytkownika. Nazwa Hello musi być ciągiem o długości 3 znaków too127.

    2. Opcjonalny **opis** hello udziału. Opis Hello pomoże zidentyfikować hello właścicieli udziału.

    3. W hello **typu** listy rozwijanej listy, określ, czy toocreate **warstwowego** lub **przypięty lokalnie** udziału. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **przypięty lokalnie udziału**. Dla wszystkich innych danych wybierz **warstwowego** udziału.

    4. W hello **pojemności** Określ rozmiar hello hello udziału. Udział warstwowych musi wynosić od 500 GB do 20 TB i przypiętych lokalnie udziału musi należeć do zakresu od 50 GB i 2 TB.

    5. W hello **ustawioną domyślną pełne uprawnienia** pola, należy przypisać hello uprawnienia toohello użytkownika lub grupy hello, który uzyskuje dostęp do tego udziału. Określ nazwę hello hello użytkownika lub grupy użytkowników hello w  _john@contoso.com_  format. Zalecane jest użycie tooaccess uprawnienia użytkownika grupy (zamiast jednego użytkownika) tooallow admin te udziały. Po przypisaniu hello uprawnienia w tym miejscu, następnie można toomodify Eksploratora plików te uprawnienia.
3. Po zakończeniu konfigurowania udziału użytkownika, kliknij przycisk **Utwórz**. Udział zostanie utworzony z hello określonych ustawień i otrzymają powiadomienie. Domyślnie kopia zapasowa będzie można włączyć hello udziału.
4. tooconfirm, który hello udziału został został pomyślnie utworzony, przejdź do pozycji toohello **udziałów** bloku. Udostępnianie wymienionych hello powinna zostać wyświetlona.
   
    ![Sukces tworzenia udziału](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Modyfikowanie udziału

Zmodyfikuj udział, gdy będziesz potrzebować toochange hello opis udziału hello. Brak właściwości udziału można zmodyfikować po utworzeniu udziału hello.

#### <a name="toomodify-a-share"></a>toomodify udziału

1. Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się udział chcesz, możesz toomodify.
2. **Wybierz** hello opis bieżącego hello tooview udziału, a następnie zmodyfikować go.
3. Zapisz zmiany, klikając hello **zapisać** paska poleceń. Określony ustawienia będą stosowane i zostanie wyświetlone powiadomienie.
   
    ![ Edytuj udziału](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Przełącz do trybu offline udziału

Może być konieczne tootake udział w trybie offline podczas planowania toomodify albo go usunąć go. Jeśli udział jest w trybie offline, nie jest dostępny do odczytu i zapisu. Konieczne będzie tootake hello udziału w tryb offline na hoście hello, a także na urządzeniu hello.

#### <a name="tootake-a-share-offline"></a>tootake udziału w trybie offline

1. Upewnij się, że udział ten hello zagrożona nie jest używana przed przełączeniem do trybu offline.
2. Przełącz hello udziału w tablicy hello w trybie offline, wykonując następujące kroki hello:
   
    1. Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello tablicy wirtualnych, na których hello znajduje się udział chcesz, możesz tootake w trybie offline.

    2. **Wybierz** hello udziału i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **przełączyć do trybu offline**.
     
        ![Udostępnij w trybie offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Przejrzyj informacje hello w hello **przełączyć do trybu offline** bloku i potwierdzenie akceptacji hello operacji. Kliknij przycisk **przełączyć do trybu offline** tootake hello udziału w trybie offline. Zostanie wyświetlone powiadomienie hello operacji w toku.

    4. tooconfirm, który hello udziału została wykonana pomyślnie toohello w trybie offline, przejdź do pozycji **udziałów** bloku. Powinny pojawić się status hello hello udziału w trybie offline.

## <a name="delete-a-share"></a>Usuń udział

> [!IMPORTANT]
> Tylko wtedy, gdy jest w trybie offline, można usunąć udziału.


Wykonaj następujące kroki toodelete udział hello.

#### <a name="toodelete-a-share"></a>toodelete udziału

1. Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy w udziale hello, które chcesz toodelete znajduje się.
2. **Wybierz** hello udziału i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **usunąć**.
   
    ![Usuń udział](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Sprawdź stan hello udziału hello ma toodelete. Jeśli chcesz toodelete udziału hello nie jest w trybie offline, przejść do trybu offline najpierw. Wykonaj kroki hello w [Przełącz do trybu offline udział](#take-a-share-offline).
4. Po wyświetleniu monitu o potwierdzenie w hello **usunąć** bloku, Zaakceptuj potwierdzenie hello i kliknij przycisk **usunąć**. udział Hello zostanie usunięte i hello **udziałów** bloku listą udziałów w tablicy wirtualnego hello hello zaktualizowane.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[sklonować udziału StorSimple](storsimple-virtual-array-clone.md).

