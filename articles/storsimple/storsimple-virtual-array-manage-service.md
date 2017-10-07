---
title: "aaaDeploy usługi Menedżer urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak toocreate i delete hello usługi Menedżer urządzenia StorSimple w hello portalu Azure, a w tym artykule opisano, jak toomanage hello klucz rejestracji usługi."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Wdrażanie usługi Menedżer StorSimple urządzenia hello tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie

Hello usługi Menedżer StorSimple urządzenie działa w systemie Microsoft Azure i łączy toomultiple urządzenia StorSimple. Po utworzeniu usługi hello, można użyć toomanage hello urządzenia z hello Microsoft Azure portalu działającego w przeglądarce. Dzięki temu toomonitor usługi wszystkie urządzenia hello, które są połączone toohello Menedżera urządzeń StorSimple z jednym centralnym miejscu, w tym samym minimalizując nakładu prac administracyjnych.

Witaj typowe zadania pokrewne tooa usługi Menedżer StorSimple urządzenia są:

* Tworzenie usługi
* Usuwanie usługi
* Pobierz klucz rejestracji usługi hello
* Wygeneruj ponownie klucz rejestracji usługi hello

W tym samouczku opisano, jak tooperform z hello poprzednich zadań. Hello informacje zawarte w tym artykule jest stosowane tylko tablice wirtualnego tooStorSimple. Aby uzyskać więcej informacji na serii StorSimple 8000 Przejdź zbyt[wdrożyć usługę Menedżer StorSimple](storsimple-manage-service.md).

## <a name="create-a-service"></a>Tworzenie usługi

toocreate usługi należy toohave:

* Subskrypcja z umową Enterprise
* Aktywne konto magazynu Microsoft Azure
* Witaj informacji dotyczących rozliczeń, która służy do zarządzania dostępem

Możesz również toogenerate konta magazynu podczas tworzenia usługi hello.

Jednej usługi można zarządzać wieloma urządzeniami. Jednak urządzenia nie może obejmować wiele usług. Duże przedsiębiorstwa mogą być wielu toowork wystąpienia usługi z różnych subskrypcji, organizacji lub nawet miejsc wdrożenia.

> [!NOTE]
> Należy oddzielnego wystąpienia Menedżera urządzeń StorSimple usługi toomanage StorSimple 8000 serii urządzeń i tablice wirtualne StorSimple.


Wykonaj następujące kroki toocreate usługi hello.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Usuwanie usługi

Przed usunięciem usługi, upewnij się, że żadnych podłączonych urządzeń używają go. Jeśli usługa hello jest używany, Dezaktywuj hello podłączone urządzenia. Witaj dezaktywować operacji sever hello połączenie między hello urządzeń i usług hello, ale zachować dane urządzenie hello w chmurze hello.

> [!IMPORTANT]
> Po usunięciu usługi hello operacji nie można cofnąć. Dowolne urządzenie, które zostało przy użyciu usługi hello należy toobe resetowanie, zanim będzie można go używać z inną usługą do ustawień fabrycznych. W tym scenariuszu dane lokalne powitania na powitania urządzenia, a także konfiguracji hello zostaną utracone.
 

Wykonaj następujące kroki toodelete usługi hello.

#### <a name="toodelete-a-service"></a>toodelete usługi

1. Przejdź za**wszystkie zasoby**. Wyszukiwanie usługi Menedżer StorSimple urządzenia. Wybierz usługę hello, że chcesz toodelete.
   
    ![Wybierz toodelete usługi](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Przejdź tooensure pulpitu nawigacyjnego usługi tooyour istnieją nie urządzeń połączonych toohello usługi. Jeśli nie ma żadnych urządzeń zarejestrowanych w usłudze tej usługi, pojawi się także efekt toohello komunikat transparentu. Kliknij polecenie **Usuń**.
   
    ![Usuwanie usługi](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** hello powiadomienia o potwierdzenie. 
   
    ![Potwierdź usunięcie usługi](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Może upłynąć kilka minut, aż toobe usługi hello usunięte. Po hello usługa jest pomyślnie usunięte, otrzymasz powiadomienie.
   
    ![Usunięcie usługi powiodło się](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

Lista Hello usług zostanie odświeżona.

 ![Zaktualizowaną listę usług](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Pobierz klucz rejestracji usługi hello
Po pomyślnym utworzeniu usługi należy tooregister urządzenie StorSimple przy użyciu usługi hello. tooregister pierwszego urządzenia StorSimple, będzie konieczne hello klucz rejestracji usługi. tooregister dodatkowych urządzeń z istniejącej usługi StorSimple, konieczne będzie zarówno klucz rejestracji hello, jak i klucz szyfrowania danych usługi hello, (który jest generowany na powitania pierwszego urządzenia podczas rejestracji). Aby uzyskać więcej informacji na temat klucza szyfrowania danych usługi hello, zobacz [zabezpieczenia usługi StorSimple](storsimple-security.md). Klucz rejestracji hello można uzyskać, uzyskując dostęp do hello **klucze** bloku dla usługi.

Wykonaj powitania po klucz rejestracji usługi hello tooget czynności.

#### <a name="tooget-hello-service-registration-key"></a>klucz rejestracji usługi hello tooget
1. W hello **Menedżera urządzeń StorSimple** bloku Przejdź zbyt**zarządzania &gt;**  **klucze**.
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. W hello **klucze** zostanie wyświetlony blok, klucz rejestracji usługi. Skopiuj klucz rejestracji hello za pomocą ikony kopiowania hello. 

Klucz rejestracji usługi hello należy przechowywać w bezpiecznym miejscu. Należy tego klucza, a także klucz szyfrowania danych usługi hello tooregister dodatkowych urządzeń z tą usługą. Po uzyskaniu klucza rejestracji usługi hello, konieczne będzie tooconfigure urządzenia za pośrednictwem hello środowiska Windows PowerShell dla StorSimple interfejsu.

## <a name="regenerate-hello-service-registration-key"></a>Wygeneruj ponownie klucz rejestracji usługi hello
Należy tooregenerate klucz rejestracji usługi, jeśli są wymagane tooperform obrotu klucza lub jeśli zmieniono hello listy administratorów usługi. Podczas ponownego generowania klucza hello, nowy klucz hello jest używany tylko do celów rejestracji kolejnych urządzeń. przez ten proces nie dotyczy to urządzeń Hello, które zostały już zarejestrowane.

Wykonaj hello następujące kroki tooregenerate klucz rejestracji usługi.

#### <a name="tooregenerate-hello-service-registration-key"></a>klucz rejestracji usługi hello tooregenerate
1. W hello **Menedżera urządzeń StorSimple** bloku Przejdź zbyt**zarządzania &gt;**  **klucze**.
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. W hello **klucze** bloku, kliknij przycisk **ponownie wygenerować**.
   
   ![Kliknij przycisk regenerate](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. W hello **klucz rejestracji usługi Regenerate** bloku, przejrzyj hello Akcja wymagana, gdy hello klucze są generowane. Wszystkie urządzenia kolejnych hello, które są zarejestrowane z tą usługą użyje hello nowy klucz rejestracji. Kliknij przycisk **ponownie wygenerować** tooconfirm. Po zakończeniu rejestracji hello, otrzymasz powiadomienie.
   
   ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Pojawi się nowy klucz rejestracji usługi.
   
    ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Skopiuj ten klucz i zapisać go do rejestracji żadnych nowych urządzeń z tą usługą.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[wprowadzenie](storsimple-virtual-array-deploy1-portal-prep.md) tablicą wirtualne StorSimple.
* Dowiedz się, jak za[administrowania urządzenia StorSimple](storsimple-ova-web-ui-admin.md).

