---
title: "Dostosowywanie wskazówki dotyczące wydajności Data Lake magazynu Storm aaaAzure | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wskazówki dotyczące wydajności Storm Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Wskazówki dotyczące Storm w usłudze HDInsight i usługi Azure Data Lake Store dostrajania wydajności

Zrozumienie hello czynników, które należy uwzględnić podczas dostrajaniu hello topologii Azure Storm. Na przykład jest ważne toounderstand hello właściwości hello pracy przez elementach spout hello i hello elementów bolt (czy pracy hello jest we/wy lub pamięci). W tym artykule omówiono szereg wytycznych, w tym Rozwiązywanie typowych problemów z dostrajania wydajności.

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Klaster Azure HDInsight** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.
* **Uruchomiony klaster Storm w usłudze Data Lake Store**. Aby uzyskać więcej informacji, zobacz [Storm w usłudze HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Wytyczne dotyczące usługi Data Lake Store dostrajania wydajności**.  Koncepcje ogólne wydajności dla [wskazówki dostrajania wydajności magazynu Lake danych](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Dostosuj hello równoległość topologii hello

Może być możliwe tooimprove wydajności przez zwiększa współbieżności hello hello tooand We/Wy z usługi Data Lake Store. Topologii Storm ma zestaw konfiguracji określające równoległości hello:
* Liczba procesów roboczych (pracowników hello jest rozmieszczana równomiernie wzdłuż hello maszyn wirtualnych).
* Liczba wystąpień Moduł wykonujący elementy spout.
* Liczba wystąpień Moduł wykonujący bolt.
* Liczba zadań spout.
* Liczba zadań bolt.

Na przykład w klastrze z 4 maszyn wirtualnych i 4 procesów roboczych, modułów 32 spout i 32 spout zadania i 256 modułów bolt i 512 bolt zadań, należy wziąć pod uwagę następujące hello:

Każdy przełożonego, który jest węzłem procesu roboczego, ma pojedynczego procesu roboczego procesu (JVM). maszyny wirtualnej Java. Ten proces JVM zarządza 4 wątków spout i 64 wątki bolt. W każdym wątku zadania są uruchamiane sekwencyjnie. Z hello powyższej konfiguracji każdy wątek spout ma 1 zadań, a każdy wątek bolt ma 2 zadania.

Poniżej przedstawiono różne składniki zaangażowane hello Storm, i ich wpływ na powitania stopień równoległości, do których masz:
* Witaj węzła głównego (o nazwie Nimbus w Storm) jest używane toosubmit zadania i zarządzać nimi. Te węzły nie mają wpływu na powitania stopień równoległości.
* Witaj przełożonego węzłów. W usłudze HDInsight odpowiada węzła procesu roboczego tooa maszyny Wirtualnej platformy Azure.
* zadania procesu roboczego Hello są Storm procesów uruchomionych w hello maszyn wirtualnych. Każde zadanie procesu roboczego odpowiada tooa wystąpienie maszyny wirtualnej Java. STORM dystrybuuje hello liczba procesów roboczych należy określić węzłów procesu roboczego toohello możliwie najbardziej równomiernie.
* Spout i wystąpienia modułu wykonującego dla elementów bolt. Każde wystąpienie modułu wykonującego odpowiada wątku tooa działających w hello pracowników (JVMs).
* Zadania STORM. Są to logiczne zadań, czy każdy z tych wątków wykonywania. Nie ma to wpływu hello stopień równoległości, dlatego należy ocenić, czy potrzebujesz wielu zadań na moduł wykonujący.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Uzyskać najlepszą wydajność hello z usługi Data Lake Store

Podczas pracy z usługą Data Lake Store, można uzyskać najlepszą wydajność hello, jeśli hello następujące:
* Połączenie małe dołącza do większych rozmiarów (najlepiej 4 MB).
* Wykonaj dowolną liczbę jednoczesnych żądań, jak to możliwe. Ponieważ każdy wątek bolt robi blokowania odczytów, ma toohave gdzieś w zakresie hello 8 12 wątków na podstawowe. Dzięki temu hello kart Sieciowych i hello również wykorzystania Procesora. Większe maszyny Wirtualnej umożliwia więcej jednoczesnych żądań.  

### <a name="example-topology"></a>Przykład topologii

Załóżmy, że masz klaster węzła procesu roboczego 8 z maszyny Wirtualnej Azure D13v2. Ta maszyna wirtualna ma 8 rdzeni, więc między hello 8 węzłów procesu roboczego, masz 64 rdzenie całkowitej.

Załóżmy, że jak 8 wątków bolt na podstawowe. Podany 64 rdzenie oznacza to, że chcemy 512 całkowita bolt wystąpienia modułu wykonującego (to znaczy wątki). W takim przypadku Załóżmy, że możemy zaczynać się jeden JVM dla maszyny Wirtualnej i głównie używane hello wątku współbieżność w hello JVM tooachieve współbieżności. Oznacza to, że potrzebujemy 8 zadania procesu roboczego (jeden na maszynie Wirtualnej platformy Azure), a 512 modułów bolt. W takiej konfiguracji Storm próbuje toodistribute hello pracowników równomiernie między węzłami procesów roboczych (znanej także jako węzły przełożonego), zapewniając każdego węzła procesu roboczego 1 maszyny wirtualnej Java. Teraz w ramach kontrolerów hello Storm podejmie próbę modułów hello toodistribute równomiernie między kontrolerów, nadanie każdej przełożonego (to znaczy JVM) 8 wątkami każdego.

## <a name="tune-additional-parameters"></a>Dostosuj dodatkowych parametrów
Po umieszczeniu Topologia podstawowa hello, można rozważyć opcję tootweak wszystkie parametry hello:
* **Liczba JVMs na węzła procesu roboczego.** Jeśli masz struktury dużej ilości danych (na przykład tabeli odnośników) hosta w pamięci, każdej maszyny wirtualnej Java wymaga osobnej kopii. Alternatywnie można użyć hello struktury danych przez wiele wątków, jeśli masz mniej JVMs. Dla operacji We/Wy hello bolt hello liczba JVMs nie powoduje tyle różnica jako hello liczba wątków, dodane w tych JVMs. Dla uproszczenia jest toohave dobrym rozwiązaniem, jeden JVM na proces roboczy. W zależności od czynności użytkownika bolt lub aplikacji, jakie przetwarzania można wymagać, chociaż może być konieczne toochange ten numer.
* **Liczba modułów spout.** Ponieważ hello poprzedniego przykładu używa elementów bolt do zapisywania tooData Lake Store, liczba hello elementach spout nie jest bezpośrednio odpowiednich toohello bolt wydajności. Jednak w zależności od ilości hello przetwarzania lub we/wy wykonywane w hello spout jest dobrym pomysłem tootune hello spouts najlepszą wydajność. Upewnij się, że masz wystarczająco dużo elementach spout toobe tookeep stanie hello elementów bolt zajęty. stawki dane wyjściowe Hello elementach spout hello powinna być zgodna hello przepływność hello elementów bolt. Rzeczywista konfiguracja Hello zależy od hello spout.
* **Liczba zadań.** Każdy bolt działa jako pojedynczy wątek. Dodatkowe zadania na bolt nie zawierają żadnych dodatkowych współbieżności. Hello tylko, gdy są one korzyści jest, jeśli procesu z potwierdzeniem krotki hello ma dużą część czasu wykonywania bolt. Jest toogroup dobrym rozwiązaniem, które wiele krotek do większych Dołącz przed wysłaniem potwierdzenia z hello bolt. Tak w większości przypadków wielu zadań stanowią żadne dodatkowe korzyści.
* **Lokalny lub losowa grupowania.** Jeśli to ustawienie jest włączone, spójne kolekcje są wysyłane toobolts w hello sam proces roboczy. Pozwala to ograniczyć wywołania między procesami komunikacji i sieci. Jest to zalecane w przypadku większości topologii.

Ten scenariusz podstawowy jest dobry punkt wyjścia. Test z własnych hello tootweak danych poprzedzających parametry tooachieve optymalną wydajność.

## <a name="tune-hello-spout"></a>Spout hello dostroić

Można zmodyfikować następujące ustawienia tootune hello spout hello.

- **Limit czasu krotki: topology.message.timeout.secs**. To ustawienie określa hello czas wiadomość ma toocomplete i odbierać potwierdzenia, zanim zostanie uznane za nie powiodło się.

- **Maksymalna liczba pamięci dla procesu roboczego: worker.childopts**. To ustawienie umożliwia określenie dodatkowych parametrów wiersza polecenia toohello Java pracowników. Witaj najczęściej używane ustawienia w tym miejscu jest XmX, określającą JVM hello maksymalna ilość pamięci przydzielona tooa stosu.

- **Spout maksymalna liczba oczekujących: topology.max.spout.pending**. To ustawienie określa liczbę hello krotek, które mogą być w locie (nie została jeszcze potwierdzone we wszystkich węzłach w topologii hello) na wątek spout w dowolnym momencie.

 Toodo dobrej obliczenia jest tooestimate hello rozmiar każdego z spójnych kolekcji. Następnie ustalić ma ilość pamięci spout jednego wątku. Witaj całkowitej ilości pamięci przydzielony wątek tooa, podzielona przez wartość ta powinien zapewnić hello górna granica spout max hello oczekujących parametru.

## <a name="tune-hello-bolt"></a>Dostosuj hello bolt
Podczas pisania tooData Lake Store, ustaw rozmiar zasady synchronizacji (bufor po stronie klienta hello) too4 MB. Opróżnianie lub hsync() następnie odbywa się tylko wtedy, gdy rozmiar buforu hello hello na tę wartość. Sterownik usługi Data Lake Store Hello na proces roboczy hello maszyny Wirtualnej automatycznie wykonuje to buforowania, chyba że jawnie przeprowadzić hsync().

bolt Data Lake magazynu Storm domyślne Hello ma parametr zasady synchronizacji rozmiar (fileBufferSize) może być używane tootune tego parametru.

W topologii/O wykonujących toohave dobrym rozwiązaniem jest każdy wątek bolt zapisu pliku własnych tooits i tooset zasadę rotacji pliku (fileRotationSize). Gdy hello plik osiągnie określony rozmiar, strumienia hello automatycznie jest opróżniany, i jest zapisywany nowy plik. zalecany rozmiar pliku obrotu Hello jest 1 GB.

### <a name="handle-tuple-data"></a>Dojście spójnej kolekcji danych

W Storm spout utrzymuje krotki tooa dopóki jawnie zostaje potwierdzony przez hello bolt. Jeśli krotka odczytane przez hello bolt, ale nie został jeszcze potwierdzony, hello spout nie może mieć trwale do zaplecza usługi Data Lake Store. Po krotka zostaje potwierdzony, hello spout można zagwarantować trwałości hello bolt i następnie można usunąć hello źródła danych z dowolnego źródła jest odczycie.  

Aby uzyskać najlepszą wydajność w usłudze Data Lake Store, mieć hello bolt buforu 4 MB danych spójnej kolekcji. Następnie należy napisać toohello zakończenia usługi Data Lake Store ponownie jako jeden zapis 4 MB. Po hello danych został pomyślnie zapisany toohello magazynu (przez wywołanie hflush()) hello bolt można potwierdzić hello danych wstecz toohello spout. To jest przykład Witaj, jakie podane tutaj ma dla elementów bolt. Jest również dopuszczalne toohold większej liczby krotek przed wywołanie hflush() hello i hello krotek potwierdzone. Jednak zwiększa hello liczbę spójnych kolekcji w locie hello spout musi toohold, czy w związku z tym zwiększa hello ilość pamięci wymaganej dla maszyny wirtualnej Java.

> [!NOTE]
Aplikacje mogą mieć krotek tooacknowledge wymaganie, częściej (w rozmiarach danych mniej niż 4 MB) dla innych nieefektywna —. Jednak, który może mieć wpływ na hello we/wy przepływności toohello magazynu zaplecza. Starannie porównać tej zależności względem wydajności operacji We/Wy hello bolt.

Szybkość odbierania hello krotek nie dużych tak toofill długo trwa hello buforu 4 MB należy rozważyć łagodzenie to przez:
* Zmniejszanie hello liczby elementów bolt, dlatego są mniej toofill buforów.
* Mających zasady oparte na czasie lub na podstawie liczby, gdzie jest hflush() wyzwalane co x opróżnienia lub co milisekund y i krotek hello zgromadzonych wykonanej do tej pory są potwierdzone Wstecz.

Pamiętaj, że w takim przypadku przepływności hello jest niższa, ale z powolne częstość występowania zdarzeń, maksymalna przepustowość nie jest celem największych hello mimo to. Te czynniki pomóc w zmniejszeniu hello całkowity czas potrzebny tooflow spójnej kolekcji, za pomocą magazynu toohello. Może być niezależnie od tego, jeśli chcesz, aby w czasie rzeczywistym procesu, nawet w przypadku występowania zdarzeń niski. Należy także zauważyć, czy Jeśli częstotliwość krotki przychodzących jest niska, należy zmienić parametr topology.message.timeout_secs hello, tak krotek hello nie upłynął limit czasu, gdy są one pobierania buforowane lub przetworzone.

## <a name="monitor-your-topology-in-storm"></a>Monitorowanie topologii w Storm  
Topologii jest uruchomiona, można go monitorować w interfejsie użytkownika Storm hello. Poniżej przedstawiono toolook głównych parametry hello na:

* **Opóźnienie wykonywania procesu całkowitej.** Jest to hello Średni czas po jednej krotce toobe emitowane przez hello spout, przetwarzane przez hello bolt i potwierdzone.

* **Bolt łączny czas oczekiwania procesu.** Jest to hello średniego czasu poświęcanego przez krotki hello na powitania bolt, dopóki nie odbierze potwierdzenia.

* **Całkowita liczba bolt wykonać opóźnienia.** Jest to średnia hello czasu poświęcanego przez bolt hello w hello wykonania metody.

* **Liczba błędów.** Odnosi się toohello liczbę spójnych kolekcji, które zakończyły się niepowodzeniem toobe całkowicie przetworzone przed limitu czasu.

* **Pojemność.** Jest to miara jest obciążenie systemu. Jeśli ta liczba jest 1, tak szybko, jak w pracy z elementów bolt. Jeśli jest mniejszy niż 1, należy zwiększyć równoległości hello. Jeśli jest większa niż 1, zmniejszenie równoległości hello.

## <a name="troubleshoot-common-problems"></a>Rozwiązywanie typowych problemów
Poniżej przedstawiono kilka typowych scenariuszy rozwiązywania problemów.
* **Limit czasu jest wiele spójnych kolekcji.** Szukaj w każdym węźle toodetermine topologii hello, gdzie to "wąskie gardło" hello. Hello Najczęstszą przyczyną tego błędu jest czy elementów bolt hello nie są możliwe tookeep się o elementach spout hello. Prowadzi to tootuples zapychaniem hello buforów wewnętrzny podczas przetwarzania toobe oczekiwania. Należy rozważyć, zwiększ wartość limitu czasu hello lub Zmniejsz hello spout max oczekujące.

* **Istnieje opóźnienie wykonywania wysokiej całkowita proces, ale opóźnienie procesu niski bolt.** W tym przypadku jest to możliwe, że krotki hello nie są przyjęte wystarczająco szybko. Sprawdź, czy istnieje wystarczająca liczba acknowledgers. Inną możliwością jest, że są one oczekujących w kolejce hello zbyt długo, zanim hello bolts start przetwarzania ich. Zmniejsz hello spout max oczekujące.

* **Brak wysokiej bolt wykonania opóźnienia.** Oznacza to, że metoda metody execute() hello Twojej bolt trwa zbyt długo. Optymalizuj kod hello, lub sprawdź rozmiary zapisu i opróżnić zachowanie.

### <a name="data-lake-store-throttling"></a>Ograniczenia przepustowości usługi Data Lake Store
Jeśli naciśniesz hello limity przepustowości udostępniane przez usługi Data Lake Store, mogą występować niepowodzeń zadań. Zapoznaj się z dziennikami zadań dla ograniczania błędy. Możesz zmniejszyć równoległości hello przez zwiększenie rozmiaru kontenera.    

toocheck, jeśli są pobierania ograniczane możesz, Włącz rejestrowanie po stronie klienta hello debugowania hello:

1. W **Ambari** > **Storm** > **Config** > **zaawansowane storm-procesu roboczego log4j**, Zmień  **&lt;główny poziom = "info"&gt;**  za**&lt;główny poziom = "debug"&gt;**. Ponownie uruchomić usługę wszystkich hello węzłów/hello konfiguracji tootake efekt.
2. Topologii Storm hello Monitor loguje węzłów procesu roboczego (w obszarze /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;portu&gt;/worker.log) dla usługi Data Lake Store ograniczania wyjątków.

## <a name="next-steps"></a>Następne kroki
Dostrajanie wydajności dla Storm może być przywoływany w [ten blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Dla toorun dodatkowe przykładowe [pokazanego w serwisie GitHub](https://github.com/hdinsight/storm-performance-automation).
