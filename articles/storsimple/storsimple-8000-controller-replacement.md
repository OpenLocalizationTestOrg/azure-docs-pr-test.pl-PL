---
title: "kontrolera urządzenia z serii StorSimple 8000 aaaReplace | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooremove i Zastąp jeden lub oba moduły kontroler na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Zastąp modułu kontroler na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Ten samouczek wyjaśnia sposób tooremove i Zastąp jeden lub oba modułów kontrolera w urządzeniu StorSimple. Zawiera omówienie również hello bazowy logikę sytuacji wymiany hello jednym lub dwoma kontrolera.

> [!NOTE]
> Wcześniejsze tooperforming zastępczy kontrolera, zaleca się zawsze aktualizują kontrolera oprogramowania układowego toohello najnowszej wersji.
> 
> tooprevent urządzenia StorSimple tooyour uszkodzenia, nie wysuwania hello kontrolera, dopóki hello LED są wyświetlane jako jedną z następujących hello:
> 
> * Wszystkie świateł są wyłączone.
> * LED 3 ![zielona ikona znacznika wyboru](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), i ![między czerwona ikona](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) miga, a LED 0 i LED 7 **ON**.


Witaj w poniższej tabeli przedstawiono hello obsługiwane kontrolera zastępczy scenariusze.

| Case | Scenariusza wymiany | Odpowiednie procedury |
|:--- |:--- |:--- |
| 1 |Jeden kontroler jest w stanie niepowodzenia, hello inny kontroler dobrej kondycji i aktywne. |[Pojedynczy kontroler zastępczy](#replace-a-single-controller), która opisuje hello [logiki zastępuje pojedynczy kontroler](#single-controller-replacement-logic), oraz hello [zamienne](#single-controller-replacement-steps). |
| 2 |Zarówno kontrolery hello nie powiodło się i wymaga zastąpienia. Podstawa montażowa Hello, dysków i obudowy dysku są w dobrej kondycji. |[Zastąpienie podwójną kontrolera](#replace-both-controllers), która opisuje hello [logiki zastępczy podwójną kontrolera](#dual-controller-replacement-logic), oraz hello [zamienne](#dual-controller-replacement-steps). |
| 3 |Kontrolery hello tego samego urządzenia lub z różnych urządzeń są zamienione. Podstawa montażowa Hello, dysków i obudów dysków są w dobrej kondycji. |Zostanie wyświetlony komunikat alertu niezgodność miejsca. |
| 4 |Jeden kontroler Brak i hello innych kontrolera kończy się niepowodzeniem. |[Zastąpienie podwójną kontrolera](#replace-both-controllers), która opisuje hello [logiki zastępczy podwójną kontrolera](#dual-controller-replacement-logic), oraz hello [zamienne](#dual-controller-replacement-steps). |
| 5 |Nie ma jednego lub obu kontrolerów. Nie można uzyskać dostępu hello urządzenia za pośrednictwem konsoli szeregowej hello lub komunikacji zdalnej programu Windows PowerShell. |[Skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) procedury wymiany ręczne kontrolera. |
| 6 |kontrolery Hello mają wersję różnych kompilacji, która może być:<ul><li>Kontrolery mają wersję innego oprogramowania.</li><li>Kontrolery mają wersję innego oprogramowania układowego.</li></ul> |W przypadku różnych wersji oprogramowania kontrolera hello logiki zastępczy hello wykrycia, że i aktualizacje hello wersję oprogramowania na powitania zastępczego kontrolera.<br><br>Jeśli wersje oprogramowania układowego kontrolera hello są różne, a jest stara wersja oprogramowania układowego hello **nie** automatycznie możliwej alertu zostanie wyświetlony komunikat w hello portalu Azure. Należy skanowania w poszukiwaniu aktualizacji i zainstaluj aktualizacje oprogramowania układowego hello.</br></br>Wersje oprogramowania układowego kontrolera hello są różne, stara wersja oprogramowania układowego hello jest automatycznie możliwej hello kontrolera zastępczy logiki wykryje to i po uruchomieniu kontrolera hello oprogramowania układowego hello zostanie automatycznie zaktualizowana. |

Należy tooremove modułu kontrolera, jeśli nie powiodło się. Jeden lub oba moduły kontrolera hello może zakończyć się niepowodzeniem, co może spowodować zastąpienie pojedynczy kontroler lub zastąpienie podwójną kontrolera. Procedury wymiany i hello logiki je można znaleźć w następującej hello:

* [Wymiana jednego kontrolera](#replace-a-single-controller)
* [Zastąp obu kontrolerów](#replace-both-controllers)
* [Usuwanie kontrolera](#remove-a-controller)
* [Wstaw kontrolera](#insert-a-controller)
* [Zidentyfikuj kontroler active hello na urządzeniu](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Przed usunięcie i zastąpienie kontrolera, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Zastąp jednego kontrolera
Gdy jeden z kontrolerów hello dwa na urządzeniu Microsoft Azure StorSimple hello nie powiodła się, jest uszkodzona lub brakuje, należy tooreplace pojedynczy kontroler.

### <a name="single-controller-replacement-logic"></a>Pojedynczy kontroler zastępczy logiki
W zastąpienia pojedynczy kontroler najpierw należy usunąć hello kontrolera nie powiodło się. (hello pozostałych kontroler na urządzeniu hello jest hello active.) Po włożeniu hello zastępczego kontrolera hello są wykonywane następujące akcje:

1. Witaj zastępczego kontrolera natychmiast rozpoczyna komunikacji z urządzeniem StorSimple hello.
2. Migawki hello wirtualnego dysku twardego (VHD) dla kontrolera active hello jest kopiowana na powitania zastępczego kontrolera.
3. migawki Hello jest modyfikowany, aby po uruchomieniu hello zastępczego kontrolera z tym dyskiem VHD zostanie rozpoznany jako kontroler wstrzymania.
4. Po zakończeniu modyfikacji hello hello zastępczego kontrolera zostanie uruchomione jako hello rezerwy kontrolera.
5. Uruchamiając obu kontrolerów hello klastra hello przejściu do trybu online.

### <a name="single-controller-replacement-steps"></a>Pojedynczy kontroler zastępczy kroki
Wykonaj następujące kroki w przypadku awarii jednego z kontrolerów hello w urządzeniu Microsoft Azure StorSimple hello. (hello innego kontrolera musi być aktywne i uruchomiona. Zarówno kontrolery się nie powieść lub nieprawidłowe działanie, przejdź zbyt[kontrolera dwa zastąpienia kroki](#dual-controller-replacement-steps).)

> [!NOTE]
> Ona potrwać 30 – 45 minut hello toorestart kontrolera i całkowicie odzyskać z hello pojedynczy kontroler zastępczy procedury. Łączny czas całej procedury hello, w tym dołączanie kable hello Hello jest około 2 godziny.


#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove modułu pojedynczy kontroler nie powiodło się
1. W hello Azure portalu, przejdź do pozycji toohello usługi Menedżer urządzeń StorSimple, kliknij przycisk **urządzeń**, a następnie kliknij nazwę hello hello urządzenia, które mają toomonitor.
2. Przejdź za**Monitor > kondycji sprzętu**. Stan Hello kontrolera 0 i kontrolera 1 powinien być czerwony, co wskazuje błąd.
   
   > [!NOTE]
   > Witaj nie powiodło się kontroler w zastępuje pojedynczy kontroler jest zawsze wstrzymania.
   
3. Użyj rysunek 1 i powitania po modułu nie powiodło się kontrolera hello toolocate tabeli.
   
    ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-controller-replacement/IC740994.png)
   
    **Rysunek 1** urządzenia StorSimple z powrotem
   
   | Etykieta | Opis |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Kontrolera 0 |
   | 4 |Kontrolera 1 |
4. Na powitania kontrolera nie powiodło się Usuń wszystkie kable sieciowe hello połączone z hello danych portów. Jeśli używasz modelu 8600 także usunąć powitalne kabli SAS, które łączyć hello kontrolera toohello EBOD kontrolera.
5. Wykonaj kroki hello w [usunąć kontroler](#remove-a-controller) tooremove hello kontrolera nie powiodło się.
6. Usunięto zastąpienie fabryki hello instalacji w hello sam gniazdo, z którego hello kontrolera nie powiodło się. Spowoduje to zainicjowanie hello pojedynczy kontroler zastępczy logiki. Aby uzyskać więcej informacji, zobacz [jednego kontrolera zastępczy logiki](#single-controller-replacement-logic).
7. Podczas hello pojedynczy kontroler zastępczy logiki kontynuowana w tle hello, ponownie połącz kable hello. Zająć tooconnect szczególną uwagę, który wszystkie kable hello dokładnie hello one zostały połączone przed hello zastąpienie tak samo.
8. Po ponownym uruchomieniu kontrolera hello, sprawdź hello **stan kontrolera** i hello **klastra stan** w hello Azure tooverify portalu, który hello kontrolera jest wstecz tooa dobrej kondycji i jest w trybie rezerwy.

> [!NOTE]
> Jeśli monitorowanych urządzeń hello za pośrednictwem konsoli szeregowej hello, gdy kontroler hello jest odzyskiwanie z procedury wymiany hello może zostać wyświetlony wielokrotne ponowne uruchomienie. Przedstawionej menu konsoli szeregowej hello następnie wiadomo o ukończeniu hello zastąpienia. Jeśli hello menu nie zostanie wyświetlone w ciągu dwóch godzin początkowych hello kontrolera zastąpienia, skontaktuj się z [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).
>
> Począwszy od aktualizacji 4, można również użyć polecenia cmdlet hello `Get-HCSControllerReplacementStatus` w interfejsie programu Windows PowerShell hello hello urządzenia toomonitor hello stanu proces zmiany hello kontrolera.
> 

## <a name="replace-both-controllers"></a>Zastąp obu kontrolerów
Gdy obu kontrolerów na urządzeniu Microsoft Azure StorSimple hello nie powiodło się, jest uszkodzona lub brakuje, należy tooreplace obu kontrolerów. 

### <a name="dual-controller-replacement-logic"></a>Podwójna kontrolera zastępczy logiki
W zastąpienia podwójną kontrolera najpierw usuń obu kontrolerów nie powiodło się, a następnie wstawić zamian. Po dwóch kontrolerów zastępczy hello są wstawiane, hello są wykonywane następujące akcje:

1. Hello zastępczego kontrolera w gnieździe 0 sprawdza następujące hello:
   
   1. Jest on przy użyciu bieżącej wersji hello oprogramowania układowego i oprogramowania?
   2. Jest on częścią klastra hello?
   3. Jest uruchomiony kontroler równorzędnej hello i się w klastrze?
      
      Jeśli żaden z tych warunków nie jest spełniony, kontrolera hello szuka hello najnowsze tworzenia codziennej kopii zapasowej (znajdujące się w hello **nonDOMstorage** na dysku w S). Kontroler Hello kopiuje hello najnowszą migawkę hello wirtualnego dysku twardego z kopii zapasowej hello.
2. Kontroler Hello gniazda 0 używa tooimage migawki hello, sama.
3. W tym samym czasie kontroler hello do gniazda 1 czeka obrazowania hello toocomplete kontrolera 0 i rozpocząć.
4. Po uruchomieniu kontrolera 0 kontrolera 1 wykryje klastra hello utworzone przez kontrolera 0, który wyzwala hello pojedynczy kontroler zastępczy logiki. Aby uzyskać więcej informacji, zobacz [jednego kontrolera zastępczy logiki](#single-controller-replacement-logic).
5. Później będzie działać zarówno kontrolery i klastra hello przejdzie w tryb online.

> [!IMPORTANT]
> Następujących zastąpienia podwójną kontrolera po skonfigurowaniu urządzenia StorSimple hello bardzo ważne jest wykonanie ręcznego tworzenia kopii zapasowej hello urządzenia. Codzienne kopie zapasowe konfiguracji urządzenia nie są wyzwalane dopiero po upływie 24 godzin. Praca z [Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake ręcznego tworzenia kopii zapasowej urządzenia.


### <a name="dual-controller-replacement-steps"></a>Kroki zastępczy podwójną kontrolera
Ten przepływ pracy jest wymagany, gdy oba hello kontrolerów w urządzeniu Microsoft Azure StorSimple nie powiodło się. Taka sytuacja może wystąpić w centrum danych, w której układ chłodzenia hello przestanie działać, a w związku z tym obu kontrolerów hello się nie powieść w krótkim czasie. W zależności od tego, czy urządzenia StorSimple hello jest wyłączona, czy używasz 8600 i model 8100 innego zestawu kroków jest wymagana.

> [!IMPORTANT]
> Ona potrwać godzinę too1 45 minut hello toorestart kontrolera i całkowicie odzyskać z podwójnym kontrolerem procedury zastąpienia. Całkowity czas całej procedury hello, w tym dołączanie kable hello Hello jest około 2,5 godzin.

#### <a name="tooreplace-both-controller-modules"></a>tooreplace zarówno modułów kontrolera
1. Witaj urządzenia jest wyłączona, Pomiń ten krok i przejdź toohello następnego kroku. Urządzenie hello jest włączone, wyłącz hello urządzenia.
   
   1. Jeśli używasz modelu 8600 Wyłącz obudowa głównej hello pierwszy, a następnie wyłącz hello EBOD obudowy.
   2. Zaczekaj, aż urządzenie hello został całkowicie zamknięty. Wszystkie hello LED w hello obu hello urządzenia będą wyłączone.
2. Usuń wszystkie hello kable sieciowe, które są połączone toohello danych portów. Jeśli używasz modelu 8600 także usunąć powitalne kabli SAS, które łączyć hello głównej obudowa toohello EBOD obudowy.
3. Usuń obu kontrolerów z hello urządzenia StorSimple. Aby uzyskać więcej informacji, zobacz [usunąć kontroler](#remove-a-controller).
4. Najpierw Wstaw hello fabryki zastąpienia dla kontrolera 0, a następnie Wstaw kontrolera 1. Aby uzyskać więcej informacji, zobacz [Wstaw kontrolera](#insert-a-controller). Spowoduje to zainicjowanie hello kontrolera dwa zastąpienia logiki. Aby uzyskać więcej informacji, zobacz [kontrolera dwa zastąpienia logiki](#dual-controller-replacement-logic).
5. Podczas hello kontrolera zastępczy logiki kontynuowana w tle hello, ponownie połącz kable hello. Zająć tooconnect szczególną uwagę, który wszystkie kable hello dokładnie hello one zostały połączone przed hello zastąpienie tak samo. Zobacz hello szczegółowe instrukcje dotyczące modelu w hello kabel sekcji urządzenia [zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md) lub [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md).
6. Włącz hello urządzenia StorSimple. Jeśli używasz modelu 8600:
   
   1. Upewnij się, że tego hello obudowa EBOD jest włączona na pierwszy.
   2. Poczekaj, aż hello obudowa EBOD jest uruchomiona.
   3. Włącz hello obudowa podstawowego.
   4. Po hello pierwszy kontroler ponownym uruchomieniu i jest w dobrej kondycji, hello system zostanie uruchomiona.
      
      > [!NOTE]
      > Jeśli monitorowanych urządzeń hello za pośrednictwem konsoli szeregowej hello, gdy kontroler hello jest odzyskiwanie z procedury wymiany hello może zostać wyświetlony wielokrotne ponowne uruchomienie. Po wyświetleniu menu konsoli szeregowej hello następnie wiadomo o ukończeniu hello zastąpienia. Jeśli hello menu nie zostanie wyświetlone w ciągu godziny 2,5 początkowych hello kontrolera zastąpienia, skontaktuj się z [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).
     
## <a name="remove-a-controller"></a>Usuwanie kontrolera
Użyj hello następujące procedury tooremove modułu uszkodzony kontroler z urządzenia StorSimple.

> [!NOTE]
> następujące ilustracje Hello są przeznaczone dla kontrolera 0. Dla kontrolera 1 te będzie można cofnąć.


#### <a name="tooremove-a-controller-module"></a>tooremove modułu kontrolera
1. Ujmij zatrzaśnięcia modułu hello między thumb i wskazującym.
2. Ostrożnie zmieścić Twojej thumb i wskazującym razem toorelease hello kontrolera zatrzaśnięcia.
   
    ![Zwalnianie zatrzaśnięcia kontrolera](./media/storsimple-controller-replacement/IC741047.png)
   
    **Rysunek 2** zwolnienie zatrzaśnięcia kontrolera
3. Użyj zatrzaśnięcia hello jako kontroler dojście tooslide hello poza hello obudowy.
   
    ![Przedłużanie kontrolera poza obudowy](./media/storsimple-controller-replacement/IC741048.png)
   
    **Rysunek 3** kontrolera hello ruchomej poza hello obudowy

## <a name="insert-a-controller"></a>Wstaw kontrolera
Użyj hello następujące procedury tooinstall modułu dostarczone przez fabrykę kontrolera, po usunięciu błędny modułu z urządzenia StorSimple.

#### <a name="tooinstall-a-controller-module"></a>tooinstall modułu kontrolera
1. Sprawdź toosee w przypadku dowolnego toohello uszkodzenia łączników interfejsu. Nie należy instalować hello modułu, jeśli dowolne numerów PIN łącznika hello są uszkodzone lub psia.
2. Moduł kontrolera hello slajdów w obudowie hello podczas zatrzaśnięcia hello pełni jest zwalniany.
   
    ![Przedłużanie kontrolera do podstawy](./media/storsimple-controller-replacement/IC741053.png)
   
    **Rysunek 4** ruchomej kontrolera w obudowie hello
3. Modułem kontrolera hello wstawiony rozpoczyna zamykanie zatrzaśnięcia hello podczas kontynuowanie toopush hello kontrolera modułu w obudowie hello. Zatrzaśnięcia Hello zastosują tooguide hello kontrolera w miejscu.
   
    ![Zamykanie zatrzaśnięcia kontrolera](./media/storsimple-controller-replacement/IC741054.png)
   
    **Rysunek 5** zamknięcie hello zatrzaśnięcia kontrolera
4. Wszystko będzie gotowe, gdy zatrzaśnięcia hello zostanie zablokowany na miejscu. Witaj **OK** LED powinno być teraz na.
   
   > [!NOTE]
   > Too5 minut dla kontrolera hello i hello LED tooactivate może potrwać.
  
5. tooverify że zastępczy hello zakończyła się powodzeniem, w hello portalu Azure Przejdź tooyour urządzenia, a następnie przejdź zbyt**Monitor** > **kondycji sprzętu**i upewnij się, że oba kontrolera 0 i kontrolera 1 są w dobrej kondycji (stan jest zielony).

## <a name="identify-hello-active-controller-on-your-device"></a>Zidentyfikuj kontroler active hello na urządzeniu
Istnieje wiele sytuacji, takie jak zastąpienie rejestracji lub kontrolera urządzenia po raz pierwszy, wymagających toolocate hello aktywnym kontrolerze na urządzeniu StorSimple. Kontroler active Hello przetwarza wszystkie hello oprogramowania układowego i sieci operacje dysków. Można użyć dowolnego hello następujące metody tooidentify hello aktywnym kontrolerze:

* [Użyj hello Azure tooidentify portalu hello active kontrolera](#use-the-azure-portal-to-identify-the-active-controller)
* [Użyj środowiska Windows PowerShell dla StorSimple tooidentify hello active kontrolera](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Sprawdź kontrolera active tooidentify hello hello urządzenia fizycznego](#check-the-physical-device-to-identify-the-active-controller)

Każdy z tych procedur jest opisane w dalszej części.

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a>Użyj hello Azure tooidentify portalu hello active kontrolera
W portalu Azure Witaj, przejdź tooyour urządzenia, a następnie zbyt**Monitor** > **kondycji sprzętu**i przewiń toohello **kontrolerów** sekcji. W tym miejscu można sprawdzić, który kontroler jest aktywny.

![Zidentyfikuj kontroler active w portalu Azure](./media/storsimple-controller-replacement/IC752072.png)

**Rysunek 6** aktywnym kontrolerze hello przedstawiający portal Azure

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Użyj środowiska Windows PowerShell dla StorSimple tooidentify hello active kontrolera
Gdy uzyskujesz dostęp do urządzenia za pośrednictwem konsoli szeregowej hello, zobaczy komunikat transparentu. wiadomości powitania Transparent zawiera urządzenia podstawowe informacje, takie jak hello model, nazwę, wersję zainstalowanego oprogramowania i stanu hello kontrolera, które uzyskują dostęp do. następujące obraz powitania przedstawiono przykład komunikat transparentu:

![Komunikat transparentu szeregowe](./media/storsimple-controller-replacement/IC741098.png)

**Rysunek 7** komunikat transparentu przedstawiający kontrolera 0 jako aktywny

Można użyć toodetermine komunikat transparentu hello, czy kontroler hello są połączone toois aktywnych lub pasywnych.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Sprawdź kontrolera active tooidentify hello hello urządzenia fizycznego
tooidentify hello aktywnym kontrolerze urządzenia, Znajdź LED hello niebieski powyżej hello dane 5 portu hello obu hello obudowa podstawowego.

Jeśli migotania tego LED hello kontrolera jest aktywna i hello inny kontroler jest w stanie wstrzymania. Użyj następującego diagram hello i tabeli jako pomoc.

![Urządzenia IDE głównej obudowa z porty danych](./media/storsimple-controller-replacement/IC741055.png)

**Rysunek 8** obu głównej obudowa z portami danych i monitorowania LED

| Etykieta | Opis |
|:--- |:--- |
| 1-6 |DANE 0 – 5 porty sieciowe |
| 7 |Niebieski LED |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).

