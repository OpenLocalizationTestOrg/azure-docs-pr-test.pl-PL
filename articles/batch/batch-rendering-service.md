---
title: "aaaUse hello renderowania usługi partia zadań Azure usługa toorender w chmurze hello | Dokumentacja firmy Microsoft"
description: "Renderuj zadania na maszynach wirtualnych platformy Azure bezpośrednio z programu Maya z opłatami za użycie."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Rozpoczynanie pracy z hello renderowania partii usługi

usługi Azure partii renderowanie Witaj oferuje możliwości renderowania skali chmury na podstawie użycia płatności. Witaj renderowania partii usługi obsługuje planowanie zadań i Kolejkowanie, zarządzanie błędów i ponownych prób i automatyczne skalowanie dla zadania renderowania. Hello renderowania partii usługi obsługuje Autodesk Maya, 3ds Max i Arnold z obsługą inne aplikacje, które wkrótce. Hello partii wtyczki dla Maya 2017 umożliwia łatwe toostart zadania renderowania na platformie Azure bezpośrednio z pulpitu. 

## <a name="supported-applications"></a>Obsługiwane aplikacje

Witaj renderowania partii usługi obsługuje obecnie hello następujące aplikacje:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Wymagania wstępne

usługi partii renderowanie Witaj toouse potrzebne są:

- [Konto platformy Azure](https://azure.microsoft.com/free/). 
- **Konto usługi Azure Batch.** Aby uzyskać wskazówki dotyczące tworzenia konta usługi partia zadań w hello portalu Azure, zobacz [Tworzenie konta usługi partia zadań z portalu Azure hello](batch-account-create-portal.md).
- **Konto usługi Azure Storage.** zasoby Hello używany do renderowania zadania są przechowywane w usłudze Azure Storage. Konto magazynu możesz utworzyć automatycznie podczas konfigurowania konta usługi Batch. Możesz także użyć istniejącego konta magazynu. toolearn więcej na temat kont magazynu, zobacz [jak toocreate, zarządzania i usuwania konta magazynu w portalu Azure hello](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

Witaj toouse partii wtyczki dla Maya, należy:

- **Maya 2017**
- **Arnold for Maya**

Można również użyć hello [portalu Azure](https://portal.azure.com) pule toocreate maszyn wirtualnych, które są wstępnie skonfigurowane z Maya, 3ds Max i Arnold. Można użyć zadania portalu toomonitor hello i diagnozowania zadania nie powiodło się, pobierając Dzienniki aplikacji i łącząc zdalnie tooindividual maszyn wirtualnych za pomocą protokołu RDP lub SSH.

## <a name="basic-batch-concepts"></a>Podstawowe pojęcia usługi Batch

Przed rozpoczęciem korzystania z usługi partii renderowanie Witaj, jest przydatne toobe poznać kilka koncepcji partii, łącznie z zadań, pul i węzły obliczeniowe. więcej informacji o partii zadań Azure ogólnie rzecz biorąc, zobacz toolearn [uruchamiać obciążenia na bardzo równolegle z instancją](batch-technical-overview.md).

### <a name="pools"></a>Pule

Usługa Batch to usługa platformy do obsługi zadań związanych z intensywnymi obliczeniami, np. renderowania, w oparciu o **pulę** **węzłów obliczeniowych**. Każdy węzeł obliczeniowy w puli jest maszyną wirtualną platformy Azure z systemem Linux lub Windows. 

Aby uzyskać więcej informacji na temat pul partii i węzły obliczeniowe, zobacz hello [puli](batch-api-basics.md#pool) i [węzeł obliczeniowy](batch-api-basics.md#compute-node) sekcje w [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md).

### <a name="jobs"></a>Zadania

Plik wsadowy **zadania** jest kolekcja zadań uruchamianych na powitania obliczeniowe węzłów w puli. Po przesłaniu zadania renderowania partii dzieli zadania hello zadań i rozpowszechnia węzły obliczeniowe toohello zadania hello w hello toorun puli.

Aby uzyskać więcej informacji na temat zadań wsadowych Zobacz hello [zadania](batch-api-basics.md#job) sekcji [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Użyj hello wtyczki dla toosubmit Maya renderowania zadania wsadowego

Z hello partii wtyczki dla Maya możesz przesłać toohello zadania wsadowego renderowania bezpośrednio z Maya usługi. Hello następujące sekcje opisują sposób tooconfigure hello zadania z hello wtyczki i prześlij go. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Obciążenia hello wtyczki w Maya partii

Hello partii wtyczka jest dostępna w [GitHub](https://github.com/Azure/azure-batch-maya/releases). Rozpakuj hello archiwum tooa katalogu. Wtyczka hello można ładować bezpośrednio z hello *azure_batch_maya* katalogu.

dodatek w Maya hello tooload:

1. Uruchom program Maya.
2. Wybierz pozycję **Window (Okno)** > **Settings/Preferences (Ustawienia/preferencje)** > **Plug-in Manager (Menedżer wtyczek)**.
3. Kliknij pozycję **Browse (Przeglądaj)**.
4. Przejdź wybierz tooand *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Uwierzytelnianie konta wsadowego i magazynowania tooyour dostępu

Witaj toouse wtyczki, należy tooauthenticate przy użyciu partii zadań Azure i klucze konta magazynu Azure. tooretrieve klucze Twojego konta:

1. Wtyczki w Maya hello ekranu i wybierz hello **Config** kartę.
2. Przejdź toohello [portalu Azure](https://portal.azure.com).
3. Wybierz **konta usługi partia zadań** z menu po lewej stronie powitania. W razie potrzeby kliknij opcję **Więcej usług** i filtruj według kryterium _Batch_.
4. Znajdź liście hello hello potrzeby konta usługi partia zadań.
5. Wybierz hello **klucze** elementu menu toodisplay swoją nazwę konta, adres URL konta i klucze dostępu:
    - Wklej adres URL konta usługi partia zadań hello do hello **usługi** w hello partii wtyczki.
    - Nazwa konta hello Wklej do hello **konta usługi partia zadań** pola.
    - Klucz podstawowy konta hello Wklej do hello **wsadowego klucz** pola.
7. Wybierz konta magazynu z menu po lewej stronie powitania. W razie potrzeby kliknij opcję **Więcej usług** i filtruj według kryterium _Storage_.
8. Znajdź liście hello hello żądanego konta magazynu.
9. Wybierz hello **klucze dostępu** toodisplay elementu menu hello nazwy konta magazynu i klucze.
    - Nazwa konta magazynu hello Wklej do hello **konta magazynu** w hello partii wtyczki.
    - Klucz podstawowy konta hello Wklej do hello **klucza magazynu** pola.
10. Kliknij przycisk **Uwierzytelnij** tooensure, który hello wtyczki mogą uzyskiwać dostęp do obu kont.

Po zostały pomyślnie uwierzytelniony, ustawia wtyczki hello hello pola Stan zbyt**uwierzytelniany**: 

![Uwierzytelnianie kont usług Batch i Storage](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Konfigurowanie puli pod kątem zadania renderowania

Po uwierzytelnieniu kont usług Batch i Storage skonfiguruj pulę pod kątem zadania renderowania. Wtyczka Hello zapisuje ustawienia między sesjami. Po skonfigurowaniu preferowaną konfigurację, nie trzeba toomodify go, chyba że zmieni się.

Witaj sekcje umożliwia przeprowadzenie hello dostępne opcje dostępne na powitania **przesyłania** karty:

#### <a name="specify-a-new-or-existing-pool"></a>Określanie nowej lub istniejącej puli

toospecify puli na zadanie (job) toorun hello renderowania, wybierz hello **przesyłania** kartę. Ta karta oferuje opcje umożliwiające utworzenie puli lub wybranie istniejącej puli:

- Możesz **automatycznie udostępnić puli dla tego zadania** (opcja domyślna hello). Po wybraniu tej opcji partii tworzy puli hello wyłącznie dla bieżącego zadania hello, i automatycznie usuwa hello puli, gdy zadanie renderowanie Witaj zostanie zakończone. Ta opcja jest najlepsze w przypadku toocomplete zadania pojedynczego renderowania.
- **Ponowne użycie istniejącej puli trwałej**. Jeśli masz istniejącą pulę, który jest w stanie bezczynności, można określić tej puli dla wykonywanym zadaniem renderowanie Witaj, wybierając ją z listy rozwijanej hello. Ponowne użycie trwałego istniejącej puli zapisuje hello czas tooprovision hello puli.  
- **Utworzenie nowej puli trwałej**. Wybranie tej opcji jest tworzona nowa pula uruchomienia zadania hello. Nie usuwa hello puli, gdy zadanie hello zostanie zakończone, dzięki czemu dla przyszłych zadań można użyć go ponownie. Wybierz tę opcję, jeśli masz toorun potrzeby ciągłego, renderowania zadania. Na kolejne zadania, można wybrać **ponownego użycia istniejącej puli trwałe** toouse hello trwałe puli, utworzonej dla hello pierwszego zadania.

![Określanie puli, obrazu systemu operacyjnego, rozmiaru maszyny wirtualnej i licencji](./media/batch-rendering-service/submit.png)

Aby uzyskać więcej informacji dotyczących sposobu naliczania opłat dla maszyn wirtualnych platformy Azure, zobacz hello [często zadawane pytania dotyczące cen Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) i [często zadawane pytania dotyczące cen Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Określ tooprovision obraz powitania systemu operacyjnego

Można określić typu hello węzły obliczeniowe tooprovision toouse obrazu systemu operacyjnego w puli hello na powitania **Env** kartę (Środowisko). Wsadowe obsługuje obecnie hello następujące opcje obrazu renderowania zadania:

|System operacyjny  |Image (Obraz)  |
|---------|---------|
|Linux     |Batch CentOS — wersja zapoznawcza |
|Windows     |Batch Windows — wersja zapoznawcza |

#### <a name="choose-a-vm-size"></a>Wybieranie rozmiaru maszyny wirtualnej

Można określić rozmiaru maszyny Wirtualnej hello na powitania **Env** kartę. Aby uzyskać więcej informacji o dostępnych rozmiarach maszyn wirtualnych, zobacz [Linux VM sizes in Azure (Rozmiary maszyn wirtualnych z systemem Linux na platformie Azure)](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) oraz [Windows VM sizes in Azure (Rozmiary maszyn wirtualnych z systemem Windows na platformie Azure)](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Określ obraz systemu operacyjnego maszyny Wirtualnej hello i rozmiar na karcie Env hello](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Określanie opcji licencjonowania

Można określić licencji hello mają toouse na powitania **Env** kartę. Dostępne są następujące opcje:

- **Maya** — włączona domyślnie.
- **Arnold**, który jest włączony w przypadku wykrycia Arnold jako aparat active renderowanie Witaj w Maya.

 W razie potrzeby toorender przy użyciu własnej licencji można skonfigurować punktu końcowego licencji przez dodanie hello środowisko zmienne toohello tabeli. Być hello domyślne opcje licencjonowania toodeselect się, że jeśli możesz to zrobić.

> [!IMPORTANT]
> Rozliczenie jest wykorzystanie licencji hello uruchomionej maszyny wirtualne w puli hello, nawet jeśli hello maszyn wirtualnych nie obecnie są używane do renderowania. tooavoid dodatków, przejdź toohello **pule** karcie i zmień rozmiar węzłów too0 puli hello aż do uzyskania toorun gotowe zadanie renderowania. 
>
>

#### <a name="manage-persistent-pools"></a>Zarządzanie pulami trwałymi

Możesz zarządzać istniejącej puli trwałego na powitania **pule** kartę. Wybranie pulę z listy hello Wyświetla bieżący stan puli hello hello.

Z hello **pule** kartę, można usunąć puli hello i zmień rozmiar hello liczbę maszyn wirtualnych w puli hello. Można zmienić rozmiar puli tooavoid węzłów too0 ponoszenia kosztów Between obciążeń.

![Wyświetlanie, zmiana rozmiaru i usuwanie pul](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Konfigurowanie zadania renderowania do przesłania

Po określeniu parametrów hello hello puli, które zostanie uruchomione zadanie renderowanie Witaj tak skonfigurować zadanie hello, samej siebie. 

#### <a name="specify-scene-parameters"></a>Określanie parametrów sceny

Hello partii wtyczki wykrywa aparatu renderowania, które aktualnie używany w Maya i wyświetla hello odpowiednie ustawienia na powitania renderowania **przesyłania** kartę. Te ustawienia obejmują hello start ramki, ramki zakończenia prefiks danych wyjściowych i krok ramki. Można zastąpić ustawienia renderowania pliku sceny hello, określając różne ustawienia w hello wtyczki. Zmiany wprowadzane toohello ustawienia dodatku nie są utrwalonego toohello tyłu sceny pliku renderowania ustawień, więc można wprowadzać zmiany na podstawie przez zadanie bez konieczności tooreupload hello sceny pliku.

Wtyczka Hello wyświetli ostrzeżenie, jeśli aparat, które wybrano w Maya renderowanie Witaj nie jest obsługiwane.

Po załadowaniu nowe sceny hello wtyczka jest otwarty, kliknij przycisk hello **Odśwież** przycisk toomake się, że ustawienia hello są aktualizowane.

#### <a name="resolve-asset-paths"></a>Rozpoznawanie ścieżek zasobów

Podczas ładowania wtyczki hello skanuje plik sceny hello odwołań zewnętrznych plików. Te odwołania są wyświetlane w hello **zasoby** kartę. Jeśli nie można rozpoznać ścieżki do którego istnieje odwołanie, hello wtyczki prób toolocate hello pliku w kilku lokalizacje domyślne, w tym:

- Witaj lokalizację pliku sceny hello 
- Witaj bieżącego projektu _sourceimages_ katalogu
- Witaj bieżący katalog roboczy. 

Czy nadal hello zasobów nie zostanie znaleziony, są one dostępne z ikoną ostrzeżenia:

![Brakujące zasoby są wyświetlane z ikoną ostrzeżenia](./media/batch-rendering-service/missing_assets.png)

Jeśli znasz lokalizacji hello pliku nierozpoznane odwołania możesz kliknąć hello ostrzeżenie, że ikona toobe monit tooadd ścieżki wyszukiwania. następnie wtyczki Hello używa tego wyszukaj ścieżkę tooattempt tooresolve wszystkie brakujące zasoby. Liczba dodatkowych ścieżek wyszukiwania nie jest ograniczona.

Po rozpoznaniu odwołania na liście będzie wyświetlana ikona zielonego światła:

![Rozpoznane zasoby są wyświetlane z ikoną zielonego światła](./media/batch-rendering-service/found_assets.png)

Jeśli sceny wymaga innych plików tego dodatku plug-in hello nie wykrył, możesz dodać dodatkowe pliki lub katalogi. Użyj hello **Dodaj pliki** i **Dodaj katalog** przycisków. Po załadowaniu nowe sceny hello wtyczka jest otwarty, należy się tooclick **Odśwież** odwołania tooupdate hello sceny.

#### <a name="upload-assets-tooan-asset-project"></a>Przekaż zasoby tooan zasobów projektu

Po przesłaniu zadanie renderowanie Witaj odwołuje się do plików wyświetlanych w hello **zasoby** kartę są automatycznie przekazane tooAzure magazynu jako projekt zasobów. Możesz również przekazać pliki zasobów hello niezależnie od zadania renderowania, przy użyciu hello **przekazać** przycisk na powitania **zasoby** kartę hello zasobów projektu nazwa została określona w hello **projektu**pola i nosi nazwę po hello bieżącego projektu Maya domyślnie. Po przekazaniu plików zasobów struktura pliku lokalnego hello są zachowywane. 

Po przekazaniu zasoby mogą być przywoływane przez dowolną liczbę zadań renderowania. Wszystkie zasoby przekazane są dostępne tooany zadanie, które odwołuje się do projektu zasobów hello, lub nie są objęte hello sceny. projektu zasobów hello toochange odwołuje się kolejnego zadania, Zmień nazwę hello w hello **projektu** w hello **zasoby** kartę. W przypadku plików, które chcesz tooexclude z przekazywania usunąć ich zaznaczenie za pomocą przycisku hello zielony obok listy hello.

#### <a name="submit-and-monitor-hello-render-job"></a>Prześlij i monitor hello renderowania zadania

Po skonfigurowaniu zadania renderowanie Witaj w hello wtyczki, kliknij przycisk hello **Prześlij zadanie** przycisk na powitania **przesyłania** karcie toosubmit hello zadania tooBatch:

![Prześlij zadanie renderowanie Witaj](./media/batch-rendering-service/submit_job.png)

Można monitorować zadanie, które jest w toku z hello **zadania** kartę na powitania wtyczki. Wybierz zadanie z hello toodisplay hello bieżący stan listy hello zadania. Można także użyć tej toocancel kartę i usuwać zadania, a także toodownload hello wyjść i renderowania dzienniki. 

dane wyjściowe toodownload, zmodyfikuj hello **generuje** katalog docelowy żądany hello tooset pola. Kliknij hello koło zębate ikonę toostart proces w tle, która prowadzi obserwację hello zadania i pobiera dane wyjściowe, zgodnie z jego postępów: 

![Wyświetlanie stanu zadania i pobieranie danych wyjściowych](./media/batch-rendering-service/jobs.png)

Możesz zamknąć Maya bez zakłócania hello proces pobierania.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi partia zadań, zobacz [uruchamiać obciążenia na bardzo równolegle z instancją](batch-technical-overview.md).
