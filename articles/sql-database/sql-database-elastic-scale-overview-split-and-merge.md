---
title: "aaaMoving danych między bazami danych w chmurze skalowalnych w poziomie | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak odłamków toomanipulate i przenoszenia danych za pośrednictwem usługi hostowanej własnym przy użyciu elastyczne bazy danych interfejsów API."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Przenoszenie danych między skalowanymi bazami danych w chmurze
Jeśli jesteś oprogramowania jako deweloper usługi, i nagle ulega ogromne żądanie w aplikacji, należy tooaccommodate hello wzrostu. Dlatego należy dodać więcej baz danych (odłamków). Jak rozpowszechniać hello danych toohello nowych baz danych bez zakłócania hello integralność danych Użyj hello **narzędzia do scalania podziału** toohello nowych baz danych w bazach danych toomove danych z ograniczeniami.  

Narzędzie do scalania podziału Hello działa jako usługa sieci web platformy Azure. Administratorem lub deweloperem używa narzędzia hello toomove shardlets (dane z niezależnego fragmentu) między różnych baz danych (odłamków). Narzędzie Hello używa niezależnego fragmentu mapy zarządzania toomaintain hello metadanych bazy danych usługi i zapewnić spójne mapowania.

![Omówienie][1]

## <a name="download"></a>Do pobrania
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Dokumentacja
1. [Samouczek narzędzi elastycznej bazy danych scalania podziału](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Konfiguracja zabezpieczeń scalania podziału](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Zagadnienia dotyczące zabezpieczeń scalania podziału](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Zarządzanie mapami fragmentów](sql-database-elastic-scale-shard-map-management.md)
5. [Migrowanie istniejących baz danych tooscale w poziomie](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md)
7. [Elastyczne słownik Narzędzia bazy danych](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Dlaczego warto używać narzędzia do scalania podziału hello?
**Elastyczność**

Aplikacje muszą toostretch elastycznie poza granice hello pojedynczej bazy danych bazy danych SQL Azure. Użyj hello narzędzia toomove danych jako baz danych wymagane toonew przy zachowaniu integralności.

**Toogrow podziału** 

Należy tooincrease ogólną pojemność toohandle dynamiczny rozwój. toodo tak, utwórz jej większą pojemność przez podanie hello danych i przekazując go przyrostowo więcej baz danych do momentu wymagań wydajności są spełnione. To jest przykład głównym funkcji "podział" hello. 

**Scal tooshrink**

Pojemność musi zmniejszać powodu toohello okresach rodzaj działalności. Umożliwia narzędzie Hello można skalować w dół jednostki skalowania toofewer spowalnia biznesowych. Funkcja "merge" Hello w hello elastycznego skalowania usługi scalania podziału obejmuje to wymaganie. 

**Zarządzanie punktami HotSpot przenosząc shardlets**

Z wieloma dzierżawcami na bazę danych Alokacja hello shardlets tooshards może spowodować wąskich gardeł toocapacity na niektórych fragmentów. Wymaga to ponowne przydzielanie shardlets lub przeniesienie toonew shardlets zajęty lub mniej wykorzystywanych fragmentów. 

## <a name="concepts--key-features"></a>Pojęcia dotyczące & najważniejsze funkcje
**Obsługiwana w środowisku klienta usługi**

Scalanie podziału Hello jest dostarczana jako usługa hostowana przez klienta. Należy wdrożyć i obsługi usługi hello w subskrypcji platformy Microsoft Azure. Pakiet Hello, pobierane z NuGet zawiera toocomplete szablonu konfiguracji hello informacje dla określonego wdrożenia. Zobacz hello [samouczek scalania podziału](sql-database-elastic-scale-configure-deploy-split-and-merge.md) szczegółowe informacje. Ponieważ usługa hello jest uruchamiana w Twojej subskrypcji platformy Azure, można kontrolować i skonfigurować większość ustawień zabezpieczeń hello usługi. szablon domyślny Hello obejmuje tooconfigure opcje hello SSL, uwierzytelnianie klienta oparte na certyfikatach, szyfrowania przechowywanych poświadczeń, ochrona systemu DoS i ograniczenia adresów IP. Można znaleźć więcej informacji na temat hello aspekty zabezpieczeń w powitania po dokumentu [konfiguracji zabezpieczeń scalania podziału](sql-database-elastic-scale-split-merge-security-configuration.md).

domyślne Hello wdrożona usługa działa z jednego procesu roboczego i jedną rolę sieci web. Hello maszyna wirtualna A1 rozmiar każdego używa usługi w chmurze Azure. Gdy nie można zmodyfikować te ustawienia podczas wdrażania pakietu hello, można je zmienić po pomyślnym wdrożeniu w hello uruchamiania usługi w chmurze (za pośrednictwem hello portalu Azure). Należy pamiętać, że w tej roli procesu roboczego hello nie mogą być skonfigurowane dla więcej niż jednego wystąpienia przyczyn technicznych. 

**Identyfikator niezależnego fragmentu integracji mapy**

Usługa scalania podziału Hello współdziała z mapy niezależnego fragmentu hello aplikacji hello. Używając toosplit usługi scalania podziału hello lub zakresy scalania lub toomove shardlets między odłamków, hello usługa automatycznie aktualizuje mapy niezależnego fragmentu hello się toodate. toodo tak, usługa hello łączy bazy danych Menedżera mapy niezależnego fragmentu toohello aplikacji hello i obsługuje zakresy i mapowania postęp żądań move podziału/merge. Dzięki temu tej mapy niezależnego fragmentu hello zawsze przedstawia aktualny widok podczas operacji scalania podziału będą. Podzielić, operacje przenoszenia scalania i shardlet są implementowane przez przeniesienie partii shardlets z hello źródłowego niezależnego fragmentu toohello docelowy identyfikator niezależnego fragmentu. Podczas hello shardlet przepływu operacji hello shardlets podmiotu toohello bieżącej partii są oznaczone w trybie offline w mapie niezależnego fragmentu hello i są dostępne na potrzeby połączeń routingu zależne od danych za pomocą hello **OpenConnectionForKey** interfejsu API. 

**Spójne shardlet połączeń**

Po uruchomieniu przepływu danych dla nowej partii shardlets wszystkie podane mapowanie niezależnych zależne od danych routingu połączeń toohello niezależnego fragmentu przechowywania hello shardlet są zabitych i kolejnych połączeń z mapy niezależnego fragmentu hello toohello interfejsów API shardlets te są blokowane podczas Przenoszenie danych Hello jest w toku w kolejności tooavoid niespójności. Shardlets tooother połączeń na powitania sam identyfikator niezależnego fragmentu również pobrać skasowane, ale powiedzie się ponownie od razu przy ponownej próbie. Po przeniesieniu partii hello hello shardlets oznaczonych jako online ponownie dla niezależnych docelowy hello, a hello źródło danych zostanie usunięta z hello niezależnych źródła. Usługa Hello przechodzi przez te czynności dla każdej partii, dopóki wszystkie shardlets zostały przeniesione. To operacji kill połączenia tooseveral podczas trwania hello hello podziału/merge/przeniesienia ukończenie tej operacji.  

**Zarządzanie shardlet dostępności**

Ograniczanie połączenia hello skasowanie toohello bieżącej partii shardlets zgodnie z powyższym opisem ogranicza zakres hello niedostępności partii tooone shardlets naraz. To jest preferowana za pośrednictwem podejście gdzie niezależnych pełną hello pozostanie w trybie offline dla wszystkich jego shardlets podczas trwania operacji dzielenie i scalanie hello. Hello rozmiaru partii, zdefiniowany jako hello liczbę unikatowych shardlets toomove jednocześnie, to parametr konfiguracji. Może być zdefiniowana dla każdej operacji dzielenie i scalanie w zależności od potrzeb aplikacji hello dostępności i wydajności. Należy pamiętać, że hello zakresu, który jest zablokowany na mapie niezależnego fragmentu hello może być większy niż określony rozmiar partii hello. Jest to spowodowane usługi hello wybiera rozmiar zakresu hello tak, aby rzeczywista liczba wartości kluczy dzielenia na fragmenty danych hello hello około dopasowuje rozmiar partii hello. Jest to ważne tooremember w szczególności kluczy słabo wypełnione dzielenia na fragmenty. 

**Magazynu metadanych**

Usługa scalania podziału Hello używa toomaintain bazy danych, stanu i tookeep rejestruje podczas przetwarzania żądania. Użytkownik Hello tworzy tej bazy danych w swoich subskrypcji i zapewnia on hello parametry połączenia w pliku konfiguracji wdrożenia usługi hello hello. Administratorzy z organizacji użytkownika hello umożliwia też łączność toothis postępu żądania tooreview bazy danych i tooinvestigate szczegółowe informacje na temat potencjalnych błędów.

**Rozpoznawanie dzielenia na fragmenty**

Usługa scalania podziału Hello oddzieli (1) podzielonej tabel, tabele odwołań (2) i (3) normalne tabel. Semantyka Hello operacji przenoszenia podziału/merge są zależne od typu hello tabeli hello użyte i są zdefiniowane w następujący sposób: 

* **Tabele podzielonej**: podziału, scalania i operacji przenoszenia przenieść shardlets z niezależnych tootarget źródła. Po pomyślnym ukończeniu hello żądania ogólnego, shardlets te nie są już dostępne w źródle hello. Warto zauważyć, że tabel docelowych hello muszą tooexist na powitania docelowy identyfikator niezależnego fragmentu nie może zawierać danych w poprzednich tooprocessing zakres docelowy hello hello operacji. 
* **Tabele odwołań dla**: tabele odwołań, Podziel hello scalania i przenieść operacje skopiowanie danych hello z hello źródła toohello docelowy identyfikator niezależnego fragmentu. Należy jednak pamiętać, że żadne zmiany wystąpić na powitania niezależnych docelowy dla danej tabeli, jeśli wszystkie wiersze znajduje się już w tej tabeli w celu hello. Tabela Hello ma toobe puste dla dowolnego tabeli odwołania kopiowania tooget operacji przetwarzania.
* **Inne tabele**: inne tabele mogą być obecne na hello źródłowy lub docelowy hello operacji dzielenie i scalanie. Usługa scalania podziału Hello pomija te tabele operacje kopiowania lub przenoszenia danych. Należy jednak pamiętać, że może zakłócać te operacje, w przypadku ograniczenia.

informacje Hello na odwołanie a podzielonej tabele są udostępniane przez hello **SchemaInfo** interfejsów API hello niezależnego fragmentu mapy. Hello poniższy przykład przedstawia hello korzystanie z tych interfejsów API danego niezależnych Mapa menedżera obiektu smm: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

tabele Hello "region" i "uprzywilejowania" są zdefiniowane jako tabele odwołań i zostaną skopiowane z operacji przenoszenia podziału/merge. "klient" i "zamówienia" z kolei są definiowane jako podzielonej tabel. C_CUSTKEY i O_CUSTKEY stanowią hello dzielenia na fragmenty klucza. 

**Integralność referencyjna**

Usługa scalania podziału Hello analizuje zależności między tabelami i używa relacje klucza obcego klucza podstawowego toostage hello operacji przenoszenia tabele odwołań i shardlets. Ogólnie rzecz biorąc tabele odwołań są kopiowane najpierw w kolejności zależności, a następnie shardlets są kopiowane w kolejności ich zależności w ramach każdej partii. Jest to konieczne, aby klucz podstawowy klucz OBCY ograniczenia niezależnych docelowy hello są honorowane jako dociera hello nowych danych. 

**Spójność mapy niezależnego fragmentu i ostatecznego zakończenia**

Hello występowania błędów usługi scalania podziału hello wznawia działania po awarii dowolnego i toocomplete celem jest w toku żądania. Jednak może być sytuacjach nieodwracalny, np. przypadku utracenia lub naruszony naprawić hello docelowy identyfikator niezależnego fragmentu. W tych warunkach niektórych shardlets, które były zaplanowane przenieść toobe mogą nadal tooreside na powitania niezależnych źródła. Usługa Hello gwarantuje, że shardlet mapowania są aktualizowane wyłącznie po hello niezbędne dane zostały pomyślnie skopiowane toohello docelowej. Shardlets są usuwane tylko w źródle powitania po wszystkie swoje dane zostały skopiowane toohello docelowych i mapowania odpowiedniego hello zostały pomyślnie zaktualizowane. operacji usuwania Hello odbywa się w tle hello podczas zakresu hello jest w trybie online na powitania docelowy identyfikator niezależnego fragmentu. Usługa scalania podziału Hello zawsze gwarantuje poprawność mapowania hello przechowywane w mapie niezależnego fragmentu hello.

## <a name="hello-split-merge-user-interface"></a>Interfejs użytkownika scalania podziału Hello
pakiet usługi scalania podziału Hello obejmuje rolę procesu roboczego oraz roli sieci web. rola sieci web Hello jest żądań scalania podziału toosubmit używane w sposób interaktywny. Witaj główne składniki interfejsu użytkownika hello są następujące:

* Typ operacji: typ operacji hello jest przycisku radiowego, która kontroluje hello rodzaj działania wykonywane przez usługę powitania dla tego żądania. Można wybrać hello podziału, scalanie i Przenieś scenariuszy. Można również anulować operację wcześniej zostało przesłane. Można użyć podziału, Scal i Przenieś żądania zakresu niezależnego fragmentu mapowania. Lista niezależnych mapuje tylko operacji przenoszenia pomocy technicznej.
* Mapa niezależnego fragmentu: hello następnej sekcji żądania parametry obejmują informacji dotyczących mapy niezależnego fragmentu hello i bazy danych hello hosting mapy niezależnego fragmentu. W szczególności należy tooprovide hello nazwę serwera bazy danych SQL Azure hello i obsługi hello shardmap bazy danych, poświadczenia tooconnect toohello niezależnych zamapować bazy danych, a koniec hello nazwa hello niezależnego fragmentu mapowania. Obecnie operację hello akceptuje tylko jednego zestawu poświadczeń. Wymagane są poświadczenia wystarczające uprawnienia toohave tooperform zmienia toohello niezależnego fragmentu mapy, a także toohello dane użytkowników na powitania fragmentów.
* Zakres źródła (dzielenie i scalanie): operacja dzielenie i scalanie przetwarza zakresu, używając swojego klucza niski i wysoki. toospecify operację, podając niepowiązanego wysoka wartość klucza, sprawdź pole wyboru "max jest wysoka wartość klucza" hello i hello wysokiej klucza pole powinno pozostać puste. Hello zakres wartości kluczy, które można określić czy nie potrzeba tooprecisely dopasowania mapowania i jego granice na mapie niezależnego fragmentu. Jeśli nie określono żadnych granic zakresu na wszystkich usługi hello wywnioskuje hello najbliższego zakresu można automatycznie. Można użyć hello GetMappings.ps1 PowerShell skryptu tooretrieve hello bieżące mapowania na mapie danego niezależnego fragmentu.
* Zachowanie źródła podziału (podział): dla operacji podziału, zdefiniuj hello toosplit punktu hello źródłowy zakres. Aby to zrobić, podając hello dzielenia na fragmenty klucza, którym chcesz hello podzielić toooccur. Przycisk radiowy hello Określ, czy hello dolnej części hello toomove zakresu (z wyjątkiem podziału klucza hello), czy czy ma toomove górnej części hello (w tym hello klucza podziału).
* Źródło Shardlet (przenoszenia): Przenieś operacji różnią się od podziału lub scalić operacji, ponieważ nie wymagają źródłem hello toodescribe zakresu. Źródło przenoszenia jest po prostu identyfikowany przez wartość klucza dzielenia na fragmenty hello zaplanowanie toomove.
* Docelowy identyfikator niezależnego fragmentu (podział): po hello informacji podano w źródle hello operacji podziału, należy toodefine, w którym mają zostać skopiowane hello danych toobe tooby udostępnienie hello bazy danych SQL Azure serwera i nazwę bazy danych dla obiektu docelowego hello.
* Zakres docelowy (scalanie): operacji scalania przenieść shardlets tooan istniejący identyfikator niezależnego fragmentu. Zapewniając granice zakresu hello hello istniejącego zakresu, który ma toomerge z należy zidentyfikować hello istniejących niezależnego fragmentu.
* Rozmiar partii: formanty rozmiaru partii hello hello liczba shardlets, które przechodzą w tryb offline w czasie przenoszenia danych hello. Jest to wartość całkowita gdzie użyciem mniejszej wartości są poufne toolong okresy przestojów w przypadku shardlets. Większe wartości spowoduje zwiększenie hello czas danego shardlet w trybie offline, ale może zwiększyć wydajność.
* Identyfikator operacji (anulować): Jeśli masz wykonywana operacja, która nie jest już potrzebne, można anulować operację hello podając jego identyfikator operacji w tym polu. Identyfikator operacji hello można pobrać z tabeli stan żądania hello (zobacz sekcja 8.1) lub z danych wyjściowych hello w przeglądarce sieci web hello której przesłano Żądanie hello.

## <a name="requirements-and-limitations"></a>Wymagania i ograniczenia
Bieżąca implementacja usługi scalania podziału hello Hello jest toohello podmiotu następujące wymagania i ograniczenia: 

* odłamków Hello muszą tooexist i zarejestrowany w mapie niezależnego fragmentu hello, zanim będzie można wykonać operacji scalania podziału na tych fragmentów. 
* Usługa Hello nie tworzy tabele lub inne obiekty bazy danych, które automatycznie w ramach operacji. Oznacza to, hello schematu dla wszystkich podzielonej tabel, które odwołują się do tabel muszą tooexist hello docelowy niezależnego fragmentu tooany uprzedniego podziału/merge/przeniesienia operacji. Podzielonej tabele są w szczególności toobe wymagane w zakresie hello skutkującej toobe dodane przez operację podziału/merge/przeniesienia shardlets nowy pusty. W przeciwnym razie hello operacja zakończy się niepowodzeniem sprawdzania spójności początkowej hello na powitania docelowy identyfikator niezależnego fragmentu. Należy pamiętać, że danych referencyjnych jest kopiowana tylko, jeśli tabela referencyjna hello jest pusta i czy nie występują żadne spójności gwarantuje również z uwzględnieniem tooother równoczesnych zapisu na powitania tabele odwołań. Jest to zalecane: podczas uruchamiania operacji podziału/merge, żadne inne operacje zapisu zmiany toohello tabele odwołań.
* Usługa Hello opiera się na tożsamości wiersza unikatowy indeks lub klucz, który obejmuje hello dzielenia na fragmenty klucza tooimprove wydajności i niezawodności dla dużych shardlets. Dzięki temu dane toomove usługi hello w jeszcze bardziej szczegółowy od właśnie hello dzielenia na fragmenty wartości klucza. Dzięki temu tooreduce hello maksymalną ilość miejsca w dzienniku i blokad, które są wymagane podczas operacji hello. Należy rozważyć utworzenie unikatowego indeksu lub klucza podstawowego, w tym hello dzielenia na fragmenty klucza w danej tabeli, jeśli chcesz, aby toouse tę tabelę z żądaniami podziału/merge/przeniesienia. Ze względu na wydajność hello dzielenia na fragmenty klucz powinien być hello wiodące kolumny hello klucz lub indeks hello.
* Trakcie hello przetwarzania żądania niektóre dane shardlet mogą występować zarówno na źródłowym hello i hello docelowy identyfikator niezależnego fragmentu. Jest to niezbędne tooprotect przed awariami podczas przemieszczania shardlet hello. Hello integracji podziału scalanie z mapą niezależnego fragmentu hello gwarantuje, że połączeń za pośrednictwem hello danych zależnych routingu interfejsów API przy użyciu hello **OpenConnectionForKey** metody na mapie niezależnego fragmentu hello nie ma żadnych niespójne pośrednich stanów. Jednak jeśli łączącego źródło toohello lub hello rozpoczęta odłamków bez użycia hello **OpenConnectionForKey** metody niespójne pośrednich stanów mogą być widoczne, gdy będą żądań move podziału/merge. Połączenia te mogą być wyświetlane wyniki częściowe lub zduplikowane w zależności od czasu hello lub podstawowego połączenia hello hello niezależnego fragmentu. To ograniczenie zawiera obecnie połączeń hello przez elastycznego skalowania kilku-Shard-zapytania.
* Witaj bazy danych metadanych dla usługi scalania podziału hello nie może być udostępniany między różne role. Na przykład rola hello scalania podziału usługa działająca w tymczasowej bazy danych metadanych tooa toopoint potrzeb niż hello produkcji roli.

## <a name="billing"></a>Rozliczenia
Usługa scalania podziału Hello działa jako usługa w chmurze w ramach subskrypcji Microsoft Azure. W związku z tym dla usługi w chmurze opłaty za wystąpienia tooyour hello usługi. Jeśli często wykonać operacji przenoszenia podziału/merge, zaleca się usunąć usługi w chmurze podziału scalania. Zapisuje kosztów uruchomiona albo wdrożyć wystąpienia usługi chmury. Można ponownie wdrożyć i rozpocząć konfigurację łatwo do uruchomienia przy każdym tooperform dzielenie i scalanie operacji. 

## <a name="monitoring"></a>Monitorowanie
### <a name="status-tables"></a>Stan tabel
Hello scalania podziału usługa zapewnia hello **stan żądania** tabeli w bazie danych magazynu metadanych hello monitorowania została zakończona i bieżących żądań. Witaj tabela zawiera wiersz dla każdego żądania podziału scalania, który został przesłany toothis wystąpienie usługi scalania podziału hello. Udostępnia następujące informacje dla każdego żądania hello:

* **Sygnatura czasowa**: hello godzinę i datę rozpoczęcia hello żądania.
* **OperationId**: A identyfikator GUID, który unikatowo identyfikuje hello żądania. To żądanie może być również używane toocancel hello operacji jest nadal uruchomione.
* **Stan**: hello bieżący stan żądania hello. Bieżące żądania również wyświetlane hello Bieżąca faza, w których hello jest żądanie.
* **CancelRequest**: flagę wskazującą, czy hello żądanie zostało anulowane.
* **Postęp**: oszacowanie przez procent wykonania operacji hello. Wartość 50 wskazuje, że operacja hello jest wykonano około 50%.
* **Szczegóły**: wartości XML, która zapewnia bardziej szczegółowy raport postępu. Raport dotyczący postępu Hello jest okresowo aktualizowany jako zestawy wierszy są kopiowane z tootarget źródła. W przypadku awarii lub wyjątki ta kolumna zawiera bardziej szczegółowe informacje dotyczące niepowodzenia hello.

### <a name="azure-diagnostics"></a>Diagnostyka Azure
Usługa scalania podziału Hello używa diagnostyki Azure oparte na 2.5 zestawu SDK platformy Azure, monitorowania i diagnostyki. Konfiguracją hello diagnostyki opisane tutaj: [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](../cloud-services/cloud-services-dotnet-diagnostics.md). Witaj pakiet do pobrania zawiera dwie konfiguracje diagnostyki — jeden dla roli sieci web hello i jeden dla roli proces roboczy hello. Te konfiguracje diagnostyki dla usługi hello postępuj zgodnie ze wskazówkami hello [podstawy usługi w chmurze w systemie Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Zawiera toolog definicje hello liczniki wydajności, dzienniki programu IIS, dzienniki zdarzeń systemu Windows i dzienniki zdarzeń aplikacji podziału scalania. 

## <a name="deploy-diagnostics"></a>Wdrażanie diagnostyki
tooenable monitorowania i diagnostyki dla role sieci web i proces roboczy hello udostępniane przez pakiet NuGet hello, uruchom następujące polecenia przy użyciu programu Azure PowerShell hello za pomocą Konfiguracja diagnostyczna hello: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Można znaleźć więcej informacji na temat tooconfigure i wdrażanie ustawień diagnostycznych tutaj: [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Pobrać diagnostyki
Łatwo dostępne diagnostycznej hello Eksploratora serwera w usłudze Visual Studio w hello Azure części drzewa Eksploratora serwera hello. Otwórz wystąpienie programu Visual Studio, a na pasku menu powitania kliknij widok i Eksploratora serwera. Kliknij przycisk hello Azure ikona tooconnect tooyour subskrypcji platformy Azure. Następnie przejdź tooAzure -> magazynu -> <your storage account> -> WADLogsTable -> tabel. Aby uzyskać więcej informacji, zobacz [przeglądanie zasobami magazynu za pomocą Eksploratora serwera](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Witaj WADLogsTable wyróżniane na powyższej ilustracji hello zawiera hello szczegółowe zdarzenia z dziennika aplikacji hello scalania podziału usługi. Należy zwrócić uwagę tej domyślnej konfiguracji hello hello pobrany pakiet jest przeznaczone dla wdrożenia produkcyjnego. W związku z tym interwał powitania jaką dzienniki i liczniki są pobierane z wystąpień usługi hello jest duża (5 minut). Badań i rozwoju niższe interwał powitania dostosowując hello ustawienia diagnostyki sieci web hello lub tooyour roli procesu roboczego hello musi. Kliknij prawym przyciskiem myszy na powitania roli w hello Eksploratora serwera w usłudze Visual Studio (zobacz powyżej), a następnie Dostosuj hello Transfer okres, w oknie dialogowym hello ustawień konfiguracji diagnostyki hello: 

![Konfiguracja][3]

## <a name="performance"></a>Wydajność
Ogólnie rzecz biorąc lepszą wydajność jest toobe z hello nowszą, oczekiwane więcej wydajności warstw usług w bazie danych SQL Azure. Wyższy we/wy, Procesor i pamięć przydziały hello wyższych warstw usług korzystają z kopiowaniem masowym hello i Usuń operacje, które hello używa usługi podziału scalania. Z tego powodu należy zwiększyć warstwy usług hello tylko dla tych baz danych zdefiniowana, ograniczony okres czasu.

Usługa Hello również wykonuje zapytania weryfikacji w ramach normalnych operacji. Te zapytania weryfikacji sprawdzić nieoczekiwany obecności danych w zakresie docelowego hello i upewnij się, że wszelkie operacje podziału/merge/przeniesienia zaczyna się w spójnym stanie. Te wszystkie zapytania pracy klucza zakresach dzielenia na fragmenty określonych przez zakres hello hello działania i rozmiar partii hello w ramach hello definicję żądania. Te zapytania wykonywane najlepiej, gdy indeks jest obecny, zawierającej klucz dzielenia na fragmenty hello hello wiodących kolumn. 

Ponadto właściwość unikatowości kluczem dzielenia na fragmenty hello jako kolumnę początku hello umożliwi toouse usługi hello zoptymalizowane metody, która ogranicza zużycie zasobów w zakresie miejsca w dzienniku i pamięci. Ta właściwość unikatowości jest wymagana toomove rozmiary dużej ilości danych (zazwyczaj ponad 1GB). 

## <a name="how-tooupgrade"></a>Jak tooupgrade
1. Wykonaj kroki hello w [wdrożyć usługę scalania podziału](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Zmienianie pliku konfiguracji usługi chmury dla wdrożenia scalania podziału tooreflect hello nowej konfiguracji parametry. Nowy parametr wymagany jest hello informacji na temat hello certyfikat używany do szyfrowania. Toodo łatwo jest toocompare hello nowego szablonu pliku konfiguracji z pobierania hello względem istniejącej konfiguracji. Upewnij się, że możesz dodać ustawienia hello "DataEncryptionPrimaryCertificateThumbprint" i "DataEncryptionPrimary" hello sieci web i roli proces roboczy hello.
3. Przed wdrożeniem hello tooAzure aktualizacji, upewnij się, że wszystkie operacje aktualnie uruchomione podziału scalanie zostało ukończone. Można to łatwo zrobić badając hello stan żądania i PendingWorkflows tabele w bazie danych metadanych scalania podziału hello bieżących żądań.
4. Aktualizowanie istniejącego wdrożenia usługi podziału scalanie w Twojej subskrypcji platformy Azure przy użyciu nowego pakietu hello i zaktualizowany plik konfiguracji chmury.

Nie trzeba tooprovision nowej bazy danych metadanych dla tooupgrade podziału scalania. Witaj nowej wersji automatycznie zaktualizuje istniejących metadanych bazy danych toohello nowej wersji. 

## <a name="best-practices--troubleshooting"></a>Najlepsze rozwiązania i rozwiązywanie problemów
* Zdefiniuj dzierżawcą testowym i wykonuje operacje podziału/merge/przeniesienia najważniejszych z dzierżawcą testowym hello między kilka fragmentów. Upewnij się, wszystkie metadane w którym jest zdefiniowany poprawnie mapy niezależnego fragmentu i że operacje hello narusza ograniczenia lub klucze obce.
* Rozmiar danych dzierżawy testu hello Keep powyżej hello maksymalnego rozmiaru danych dzierżawy największy tooensure pojawiły się nie rozmiar danych związane problemy. Dzięki temu można ocenić górna granica na powitania czas toomove pojedynczej dzierżawy wokół. 
* Upewnij się, że schemat zezwala na usuwanie. usługi scalania podziału Hello wymaga hello możliwości tooremove danych z niezależnych źródła hello po hello dane zostały pomyślnie skopiowane toohello docelowej. Na przykład **Usuwanie wyzwalaczy** może uniemożliwić usunięcie hello danych w źródle hello hello usługi i może spowodować toofail operacji.
* klucz dzielenia na fragmenty Hello powinien być hello wiodących kolumn w kluczu podstawowym lub definicji unikatowego indeksu. Dzięki temu hello najlepszą wydajność dla hello dzielenie i scalanie zapytania sprawdzania poprawności i hello rzeczywiste dane przenoszenie i usuwanie operacji zawsze działających na zakresami kluczy dzielenia na fragmenty.
* W ten sposób rozmieszczać usługi podziału scalania w centrum danych i region hello gdzie znajdują się bazy danych. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

