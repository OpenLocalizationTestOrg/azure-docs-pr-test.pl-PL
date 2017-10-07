---
title: "Witaj aaaDeploy usługi Menedżer StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak toocreate i delete hello usługi Menedżer StorSimple w hello klasycznego portalu Azure, a w tym artykule opisano, jak toomanage hello klucz rejestracji usługi."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Wdrażanie usługi Menedżer StorSimple hello w hello klasycznego portalu Azure

## <a name="overview"></a>Omówienie
Witaj usługi Menedżer StorSimple działa na platformie Microsoft Azure i łączy toomultiple urządzenia StorSimple. Po utworzeniu usługi hello, można użyć toomanage hello urządzenia z hello Microsoft Azure classic portal działającego w przeglądarce. Dzięki temu toomonitor wszystkie urządzenia hello, które są połączone toohello Menedżer StorSimple usługi z jednym centralnym miejscu, w tym samym minimalizując nakładu prac administracyjnych.

Strona docelowa Menedżer StorSimple Hello Wyświetla wszystkie usługi Menedżer StorSimple hello, których można używać toomanage urządzenia magazynujące StorSimple. Dla każdej usługi Menedżer StorSimple na stronie Menedżer StorSimple hello jest prezentowane hello następujących informacji:

* **Nazwa** — hello nazwę, która została przypisana tooyour usługi Menedżer StorSimple, jeśli został on utworzony. **Nie można zmienić nazwy usługi Hello, po utworzeniu hello usługi. Dotyczy to również dla innych jednostek, takich jak urządzenia, kontenery woluminów, woluminów i zasad tworzenia kopii zapasowych, które nie mogą zostać zmienione w hello klasycznego portalu Azure.**
* **Stan** — Witaj stanu usługi hello, który może być **Active**, **tworzenie**, lub **Online**.
* **Lokalizacja** — Witaj lokalizacji geograficznej, w których hello StorSimple urządzenie zostanie wdrożona.
* **Subskrypcja** — Witaj subskrypcji, która jest skojarzona z usługą rozliczeń.

Hello typowych zadań, które mogą być wykonywane za pośrednictwem strony Menedżer StorSimple hello są:

* Tworzenie usługi
* Usuwanie usługi
* Pobierz klucz rejestracji usługi hello
* Wygeneruj ponownie klucz rejestracji usługi hello

Ten przewodnik opisuje sposób tooperform tych zadań.

## <a name="create-a-service"></a>Tworzenie usługi
Użyj hello **szybkie tworzenie** opcję toocreate usługi Menedżer StorSimple, jeśli chcesz toodeploy urządzenia StorSimple. toocreate usługi należy toohave:

* Subskrypcja z umową Enterprise
* Aktywne konto magazynu Microsoft Azure
* Witaj informacji dotyczących rozliczeń, która służy do zarządzania dostępem

Możesz również toogenerate domyślne konto magazynu podczas tworzenia usługi hello.

Jednej usługi można zarządzać wieloma urządzeniami. Jednak urządzenia nie może obejmować wiele usług. Duże przedsiębiorstwa mogą być wielu toowork wystąpienia usługi z różnych subskrypcji, organizacji lub nawet miejsc wdrożenia. Należy pamiętać, że potrzebujesz oddzielnych wystąpień urządzeń serii StorSimple 8000 z toomanage usługi Menedżer StorSimple i tablice wirtualne StorSimple.

> [!IMPORTANT] 
> Jeśli masz nieużywane utworzoną usługę (urządzenie nie wykonano operacji dla tego zasobu) przed tooAugust 2016, nie mogą być zarządzane za pośrednictwem portalu Azure lub klasycznego portalu Azure. Zaleca się tworzenie nowej usługi w hello portalu Azure.

Wykonaj następujące kroki toocreate usługi hello.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Usuwanie usługi
Przed usunięciem usługi, upewnij się, że żadnych podłączonych urządzeń używają go. Jeśli usługa hello jest używany, Dezaktywuj hello podłączone urządzenia. Witaj dezaktywować operacji sever hello połączenie między hello urządzeń i usług hello, ale zachować dane urządzenie hello w chmurze hello.

> [!IMPORTANT] 
> Po usunięciu usługi hello operacji nie można cofnąć. Dowolne urządzenie, które zostało przy użyciu usługi hello należy toobe resetowanie, zanim będzie można go używać z inną usługą do ustawień fabrycznych. W tym scenariuszu dane lokalne powitania na powitania urządzenia, a także konfiguracji hello zostaną utracone.

Wykonaj następujące kroki toodelete usługi hello.

### <a name="toodelete-a-service"></a>toodelete usługi
1. Na powitania **usługi Menedżer StorSimple** strony, że chcesz toodelete usługi wybierz hello.
2. Kliknij przycisk **usunąć** u dołu hello hello strony.
3. Kliknij przycisk **tak** hello powiadomienia o potwierdzenie. Może upłynąć kilka minut, aż toobe usługi hello usunięte.

## <a name="get-hello-service-registration-key"></a>Pobierz klucz rejestracji usługi hello
Po pomyślnym utworzeniu usługi należy tooregister urządzenie StorSimple przy użyciu usługi hello. tooregister pierwszego urządzenia StorSimple, będzie konieczne hello klucz rejestracji usługi. tooregister dodatkowych urządzeń z istniejącej usługi StorSimple, konieczne będzie zarówno klucz rejestracji hello, jak i klucz szyfrowania danych usługi hello, (który jest generowany na powitania pierwszego urządzenia podczas rejestracji). Aby uzyskać więcej informacji na temat klucza szyfrowania danych usługi hello, zobacz [zabezpieczenia usługi StorSimple](storsimple-security.md). Klucz rejestracji hello można uzyskać, uzyskując dostęp do **klucz rejestracji** na powitania **usług** strony.

Wykonaj powitania po klucz rejestracji usługi hello tooget czynności.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Klucz rejestracji usługi hello należy przechowywać w bezpiecznym miejscu. Należy tego klucza, a także klucz szyfrowania danych usługi hello tooregister dodatkowych urządzeń z tą usługą. Po uzyskaniu klucza rejestracji usługi hello, konieczne będzie tooconfigure urządzenia za pośrednictwem hello środowiska Windows PowerShell dla StorSimple interfejsu.

Aby uzyskać więcej informacji na temat toouse tego klucza, zobacz rejestracji [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Wygeneruj ponownie klucz rejestracji usługi hello
Należy tooregenerate klucz rejestracji usługi, jeśli są wymagane tooperform obrotu klucza lub jeśli zmieniono hello listy administratorów usługi. Podczas ponownego generowania klucza hello, nowy klucz hello jest używany tylko do celów rejestracji kolejnych urządzeń. przez ten proces nie dotyczy to urządzeń Hello, które zostały już zarejestrowane.

Wykonaj hello następujące kroki tooregenerate klucz rejestracji usługi.

### <a name="tooregenerate-hello-service-registration-key"></a>klucz rejestracji usługi hello tooregenerate
1. Na powitania **usługi Menedżer StorSimple** kliknij przycisk **klucz rejestracji**.
2. W hello **klucz rejestracji usługi** okno dialogowe, kliknij przycisk **ponownie wygenerować**.
3. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **OK** toocontinue z hello ponownego wygenerowania.
4. Pojawi się nowy klucz rejestracji usługi.
5. Skopiuj ten klucz i zapisać go do rejestracji żadnych nowych urządzeń z tą usługą.
6. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose tego okna dialogowego.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [procesu wdrażania StorSimple](storsimple-deployment-walkthrough-u2.md).
* Dowiedz się więcej o [Zarządzanie kontem magazynu StorSimple](storsimple-manage-storage-accounts.md).
* Dowiedz się więcej o tym, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).
