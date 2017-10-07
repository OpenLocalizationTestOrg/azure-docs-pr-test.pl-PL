---
title: aaaScale limit bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: Jak toouse hello ShardMapManager, biblioteki klienta elastycznej bazy danych
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Skalowanie w poziomie baz danych, menedżera map niezależnego fragmentu hello
tooeasily skalowania bazy danych SQL Azure, użyj Menedżera map niezależnego fragmentu. Menedżera map niezależnego fragmentu Hello jest specjalne bazy danych, która przechowuje Mapowanie globalne informacje o wszystkich odłamków (bazy danych) w zestawie niezależnego fragmentu. Witaj metadanych umożliwia aplikacji tooconnect toohello prawidłową bazę danych na podstawie wartości hello z hello **klucza dzielenia na fragmenty**. Ponadto każdy identyfikator niezależnego fragmentu w zestawie hello zawiera map, które śledzą dane dotyczące niezależnych lokalne powitania (nazywane **shardlets**). 

![Identyfikator niezależnego fragmentu mapy zarządzania](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Zrozumienie, jak te mapowania są zbudowane jest istotne tooshard mapy zarządzania. Odbywa się przy użyciu hello [klasy ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), liczba znalezionych w hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md) toomanage niezależnego fragmentu mapowania.  

## <a name="shard-maps-and-shard-mappings"></a>Mapy niezależnego fragmentu i niezależnego fragmentu mapowania
Dla każdego niezależnych musisz wybrać typ hello toocreate mapy niezależnego fragmentu. Wybór Hello zależy od hello Architektura bazy danych: 

1. Pojedynczej dzierżawy na bazę danych  
2. Wiele dzierżaw dla jednej bazy danych (dwa typy):
   1. Mapowanie list
   2. Mapowanie zakresu

Model pojedynczego dzierżawcy można utworzyć **mapowania listy** mapy niezależnego fragmentu. model pojedynczej dzierżawy Hello przypisuje jednej bazy danych dla każdego dzierżawcy. Jest to efektywne modelu dla deweloperów SaaS, ponieważ takie rozwiązanie upraszcza zarządzanie.

![Mapowanie list][1]

modelu wielodostępnym Hello przypisuje kilka dzierżaw tooa pojedynczej bazy danych (i grup dzierżawcy mogą rozpowszechniają wielu baz danych). Użyj tego modelu, gdy oczekuje się, że każdy dzierżawca toohave niewielkie zbiory danych musi. W tym modelu możemy Przypisz zakres przy użyciu bazy danych tooa dzierżawców **mapowanie zakresu**. 

![Mapowanie zakresu][2]

Lub możesz wdrożyć model bazy danych wielu dzierżawców przy użyciu *mapowania listy* tooassign wiele dzierżaw tooa pojedynczej bazy danych. Na przykład DB1 jest używane toostore informacji na temat identyfikatora dzierżawy 1 do 5 i bazy danych DB2 przechowuje dane dla dzierżawy 7 i dzierżawcy 10. 

![Wielu dzierżawców dla jednej bazy danych][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Obsługiwane typy .net dla kluczy dzielenia na fragmenty
Elastyczne hello obsługi skalowania po .net Framework typy jako klucze dzielenia na fragmenty:

* Liczba całkowita
* długa
* Identyfikator GUID
* Byte]  
* Data i godzina
* Zakres czasu
* Datetimeoffset

### <a name="list-and-range-shard-maps"></a>Mapuje niezależnych listy i zakresu
Mapy niezależnych można skonstruować przy użyciu **list dzielenia na fragmenty poszczególne wartości klucza**, lub może być skonstruowany, za pomocą **wartości klucza zakresy dzielenia na fragmenty**. 

### <a name="list-shard-maps"></a>Lista niezależnych mapy
**Odłamków** zawierają **shardlets** i mapowanie shardlets tooshards hello jest obsługiwana przez mapy niezależnego fragmentu. A **mapy niezależnego fragmentu listy** jest skojarzenie między hello poszczególnych wartości klucza identyfikujące hello shardlets i baz danych hello, które służą jako niezależne.  **Lista mapowań** są jawne i różnych wartości klucza może być zmapowane toohello tej samej bazy danych. Na przykład klucz 1 mapuje tooDatabase A i wartości kluczy, 3 i 6 odwołania B. bazy danych

| Klucz | Identyfikator niezależnego fragmentu lokalizacji |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| Przyciski ... |Przyciski ... |

### <a name="range-shard-maps"></a>Mapuje niezależnych zakresu
W **mapy niezależnego fragmentu zakresu**, zakresem kluczy hello jest opisany przez parę **[wartość niska, wysoka wartość)** gdzie hello *niska wartość* jest hello klucz minimum zakresu hello i hello *Wysokiej wartości* jest hello pierwszej wartości wyższej niż hello zakres. 

Na przykład **[0, 100)** obejmuje wszystkie liczby całkowite większe niż lub równa 0 i mniejsza niż 100. Należy pamiętać, że wiele zakresów może punktu toohello sama baza danych i rozłączne zakresy są obsługiwane (np. [100,200) i [400,600) zarówno tooDatabase punktu C w poniższym przykładzie hello.)

| Klucz | Identyfikator niezależnego fragmentu lokalizacji |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| Przyciski ... |Przyciski ... |

Każdej z tabel hello pokazanym powyżej to przykład koncepcyjnej **ShardMap** obiektu. Każdy wiersz jest uproszczony przykład osoba **PointMapping** (dla mapy niezależnego fragmentu listy hello) lub **RangeMapping** (dla mapy niezależnego fragmentu zakresu hello) obiektu.

## <a name="shard-map-manager"></a>Menedżer mapy niezależnego fragmentu
W bibliotece klienta hello hello niezależnego fragmentu mapy Menedżer jest kolekcja map niezależnego fragmentu. Witaj danych zarządzanych przez **ShardMapManager** wystąpienia jest przechowywany w trzech miejscach: 

1. **Globalne mapy niezależnego fragmentu (GSM)**: Określ tooserve bazy danych jako repozytorium powitania dla wszystkich map niezależnego fragmentu i mapowania. Specjalne tabele i procedury składowane są tworzone automatycznie toomanage hello informacji. Zazwyczaj jest mała baza danych, a lekkim dostępne i nie powinna być używana na potrzeby innych aplikacji hello. Witaj tabele są w schemacie specjalne o nazwie **__ShardManagement**. 
2. **Lokalny identyfikator niezależnego fragmentu mapy (LSM) tak**: każdej bazy danych, który określisz toobe niezależnego fragmentu jest zmodyfikowany toocontain kilka tabel małe i specjalnych procedur składowanych, zawierające i zarządzanie niezależnych toothat określonych informacji mapy niezależnego fragmentu. Te informacje są nadmiarowe informacje hello w hello GSM, i udostępnia informacje o mapy niezależnego fragmentu toovalidate w pamięci podręcznej aplikacji hello bez wprowadzania żadnych obciążenia na powitania GSM; Aplikacja Hello używa hello LSM toodetermine mapowanie pamięci podręcznej jest nadal ważny. Hello tabele odpowiedniego toohello LSM na każdym niezależnego fragmentu są również w schemacie hello **__ShardManagement**.
3. **Pamięci podręcznej aplikacji**: każda aplikacja wystąpienia dostęp do **ShardMapManager** obiekt zachowuje lokalnej pamięci podręcznej w pamięci z jego mapowanie. Przechowuje informacje routingu, która została ostatnio pobrana. 

## <a name="constructing-a-shardmapmanager"></a>Konstruowanie ShardMapManager
A **ShardMapManager** obiekt jest tworzony przy użyciu [fabryki](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) wzorca. Witaj  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  metoda przyjmuje poświadczenia (w tym hello nazwy serwera i bazy danych zawierający hello GSM) w formie hello  **ConnectionString** i zwraca wystąpienie klasy **ShardMapManager**.  

**Uwaga:** hello **ShardMapManager** były tworzone tylko raz dla domeny aplikacji w ramach hello kodu inicjowania aplikacji. Tworzenie wystąpień dodatkowe ShardMapManager w hello tego samego elementu appdomain, wynikiem będzie znacznie większą ilość pamięci i procesora aplikacji hello. A **ShardMapManager** może zawierać dowolną liczbę niezależnych mapy. Mapa jednego niezależnego fragmentu może być wystarczające dla wielu aplikacji, istnieją momenty, gdy różne zestawy baz danych są używane do innego schematu lub do celów unikatowe; w takich przypadkach może być preferowana wielu map niezależnego fragmentu. 

W tym kodzie aplikacja próbuje tooopen istniejące **ShardMapManager** z hello [metody TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Jeśli obiekty reprezentujące Global **ShardMapManager** (GSM) nie zostały jeszcze istnieje wewnątrz hello bazy danych, powitania klienta biblioteki tworzy je tam przy użyciu hello [metody CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

Alternatywnie można użyć programu Powershell toocreate nowego Menedżera mapy niezależnego fragmentu. Przykład jest dostępny [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Pobierz RangeShardMap lub ListShardMap
Po utworzeniu niezależnych menedżera map, możesz uzyskać hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) lub [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) przy użyciu hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), lub hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metody.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Poświadczenia administrowania niezależnego fragmentu mapy
Aplikacje, które administrowania i manipulowania mapy niezależnego fragmentu różnią się od tych, które korzystają z połączeń tooroute mapy niezależnego fragmentu hello. 

mapuje tooadminister niezależnego fragmentu (Dodawanie lub zmienianie odłamków, mapy niezależnego fragmentu, niezależnego fragmentu mapowania, itp.) musi utworzyć wystąpienia hello **ShardMapManager** przy użyciu **poświadczenia, które mają uprawnienia w bazie danych zarówno hello GSM i na każdym odczytu/zapisu bazy danych, która służy jako identyfikator niezależnego fragmentu**. poświadczenia Hello muszą zezwalać na dla operacji zapisu dla tabel hello w obu hello GSM i LSM niezależnego fragmentu mapy informacji jest wprowadzona lub zmienić również podobnie jak w przypadku tworzenia tabel LSM na nowych fragmentów.  

Zobacz [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Tylko metadane, których to dotyczy
Metody używane do zapełniania lub zmiany hello **ShardMapManager** danych nie należy zmieniać hello dane użytkownika przechowywane w odłamków hello, samodzielnie. Na przykład metod, takich jak **CreateShard**, **DeleteShard**, **UpdateMapping**, itd. wpływa na powitania niezależnego fragmentu mapy zawierają tylko metadane. Nie należy usuwać, Dodaj lub alter użytkownika dane zawarte w odłamków hello. Jednak te metody są zaprojektowane toobe używane w połączeniu z oddzielnych Przeprowadź toocreate lub usunąć rzeczywiste bazy danych lub ten ruch wiersze z tabeli toorebalance tooanother jednego niezależnego fragmentu podzielonej środowiska.  (hello **scalania podziału** narzędzia dołączonego do narzędzi elastycznej bazy danych korzysta z poniższych interfejsów API oraz organizowanie rzeczywiste przeniesienie danych między odłamków.) Zobacz [skalowania, za pomocą narzędzia hello scalanie podziału elastycznej bazy danych](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Wypełnianie przykład mapy niezależnego fragmentu
Poniżej przedstawiono przykład sekwencji operacji toopopulate mapy określonych niezależnego fragmentu. Kod Hello wykonuje następujące czynności: 

1. Nowej mapy niezależnego fragmentu jest tworzony w ramach menedżera map niezależnego fragmentu. 
2. Witaj metadanych dla dwóch różnych odłamków jest dodawany toohello niezależnego fragmentu mapy. 
3. Różnych mapowań klucza zakresu zostaną dodane, a hello ogólną mapy niezależnego fragmentu hello jest wyświetlana zawartość. 

Kod Hello jest zapisywany tak, aby metody hello można uruchomić ponownie, jeśli wystąpi błąd. Każde żądanie sprawdza, czy identyfikator niezależnego fragmentu lub mapowanie już istnieje, przed podjęciem próby wykonania toocreate go. Witaj kodu zakłada, że bazy danych o nazwie **sample_shard_0**, **sample_shard_1** i **sample_shard_2** zostały już utworzone na serwerze hello odwołuje się ciąg **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Jak można użyć programu PowerShell zamiast skryptów tooachieve hello spowodować takie same. Dostępne są niektóre przykłady z programu PowerShell próbki hello [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Po mapy niezależnego fragmentu są wypełnione, aplikacje dostępu do danych można utworzyć lub dostosowywane toowork przy użyciu map hello. Wypełnianie lub manipulowanie mapy hello muszą wystąpić ponownie dopiero **mapę układu** musi toochange.  

## <a name="data-dependent-routing"></a>Routing zależny od danych
Hello niezależnego fragmentu Mapa Menedżera będzie najbardziej używany w aplikacji, które wymagają bazy danych połączenia tooperform hello dane specyficzne dla aplikacji operacji. Te połączenia musi być skojarzony z hello poprawną bazą danych. Jest to nazywane **danych zależnych routingu**. W przypadku tych aplikacji wystąpienia obiekt menedżera niezależnego fragmentu mapy z fabryki hello przy użyciu poświadczeń, które mają dostęp tylko do odczytu w bazie danych GSM hello. Poszczególnych żądań w połączeniach nowszej Podaj poświadczenia niezbędne do łączenia toohello odpowiedni identyfikator niezależnego fragmentu w bazie danych.

Należy pamiętać, że te aplikacje (przy użyciu **ShardMapManager** otwarty przy użyciu poświadczeń tylko do odczytu) nie można wprowadzić zmiany mapy toohello lub mapowania. W przypadku tych potrzeb utworzyć administracyjne dotyczące aplikacji i skryptów programu PowerShell, zapewniających poświadczenia z niskimi uprawnieniami, zgodnie z wcześniejszym opisem. Zobacz [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md).

Aby uzyskać więcej informacji, zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modyfikowanie mapy niezależnego fragmentu
Mapa niezależnych można zmienić na różne sposoby. Modyfikowanie wszystkich hello następujące metody hello metadane opisujące odłamków hello i ich mapowania, ale ich nie należy fizycznie modyfikować danych w ramach odłamków hello ani ich tworzyć ani nie usuwaj hello rzeczywiste baz danych.  Niektóre operacje hello na mapie niezależnego fragmentu hello opisanych poniżej może być konieczne toobe skoordynować z działania administracyjne, które fizycznie przenieść dane lub dodać i usunąć bazy danych służy jako niezależne.

Te metody współpracują ze sobą jako bloków konstrukcyjnych hello dostępne modyfikowania hello ogólną rozkład danych w środowisku podzielonej bazy danych.  

* tooadd lub usuń odłamków: Użyj  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  i  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  z hello [Shardmap klasy](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Witaj serwera i reprezentujący hello docelowy identyfikator niezależnego fragmentu bazy danych musi już istnieć dla tooexecute te operacje. Te metody nie mają wpływu na powitania baz danych, tylko na metadanych w mapie niezależnego fragmentu hello.
* toocreate lub usuwanie punktów lub zakresy, które są mapowane odłamków toohello: Użyj  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  z hello [Klasy RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx), i  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  z hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Wiele różnych punktach lub zakresy mogą być mapowane toohello sam identyfikator niezależnego fragmentu. Te metody mają wpływ tylko na metadanych — nie wpływają na dane, które mogą już być obecne w fragmentów. Jeśli dane wymagają toobe usunięte z bazy danych hello w kolejności toobe zgodne z **DeleteMapping** operacje, konieczne będzie tooperform te operacje oddzielnie, ale w połączeniu z przy użyciu tych metod.  
* toosplit istniejących zakresów do dwóch lub scalania sąsiadujących zakresów w jednym: Użyj  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  i  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Należy pamiętać, że dzielenie i scalanie operacji **nie należy zmieniać klucza toowhich niezależnego fragmentu hello wartości są mapowane**. Podział dzieli istniejący zakres na dwie części, ale pozostawia zarówno jako toohello mapowane sam identyfikator niezależnego fragmentu. Scalanie działa na dwóch sąsiadujących zakresów, które są już mapowane toohello sam identyfikator niezależnego fragmentu, łączenie ich do jednego zakresu.  Witaj przepływu punkty lub zakresy się między odłamków musi toobe koordynowane przy użyciu **UpdateMapping** w połączeniu z rzeczywiste przeniesienie danych.  Można użyć hello **podziału/Merge** usługi, która jest częścią elastycznej bazy danych narzędzi toocoordinate niezależnego fragmentu mapy zmian z przepływu danych, gdy potrzebny jest przepływu. 
* Mapa toore (lub Przenieś) poszczególnych punktów lub zakresy toodifferent odłamków: Użyj  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Ponieważ danych może być konieczne toobe przeniesione z jednego niezależnego fragmentu tooanother w kolejności toobe zgodne z **UpdateMapping** operacji, konieczne będzie tooperform tego przepływu oddzielnie, ale w połączeniu z przy użyciu tych metod.
* mapowania tootake online i offline: Użyj  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  i  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello stan online mapowania. 
  
    Niektóre operacje na niezależnego fragmentu mapowania są dozwolone tylko podczas mapowania jest w stanie "offline", w tym **UpdateMapping** i **DeleteMapping**. Podczas mapowania jest w trybie offline, żądanie zależne od danych oparte na kluczu zawarte w tym mapowania spowoduje zwrócenie błędu. Ponadto gdy zakres jest najpierw przełączona w tryb offline, wszystkie niezależnych toohello dotyczy połączeń są automatycznie skasowane w kolejności wyniki niespójne lub niekompletne tooprevent zapytań skierowanej zakresy zmieniane. 

Mapowania są niezmienne obiekty w środowisku .net.  Wszystkie metody hello powyżej, które spowodują zmianę mapowania również unieważnienie toothem żadnych odwołań w kodzie. toomake it łatwiejsze tooperform sekwencji działań, które spowodują zmianę stanu mapowania, wszystkie metody hello, które spowodują zmianę mapowania zwrócić nowe mapowanie odwołania, co operacje można powiązać. Na przykład toodelete istniejące mapowanie w sm shardmap, który zawiera klucz hello 25, można wykonywać następujące hello: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Dodawanie niezależnego fragmentu
Aplikacje często wymagają toosimply dodać nowe dane toohandle odłamków oczekuje się od nowych kluczy lub kluczy zakresów, mapy niezależnego fragmentu, która już istnieje. Na przykład aplikację podzielonej na podstawie Identyfikatora dzierżawcy może być konieczne tooprovision nowy identyfikator niezależnego fragmentu dla nowej dzierżawy lub co miesiąc podzielonej danych może być konieczne nowy identyfikator niezależnego fragmentu udostępnione przed rozpoczęciem powitalne każdego nowego miesiąca. 

Jeśli hello nowy zakres wartości kluczy nie jest już częścią istniejące mapowanie i nie przenoszenia danych jest to konieczne, jest bardzo prosty tooadd hello nowy identyfikator niezależnego fragmentu i Skojarz nowy klucz hello lub fragmentacji toothat zakresu. Aby uzyskać więcej informacji na temat dodawania nowych fragmentów, zobacz [Dodawanie nowych niezależnego fragmentu](sql-database-elastic-scale-add-a-shard.md).

W scenariuszach, wymagających przenoszenia danych jednak narzędzie scalania podziału hello jest wymagane tooorchestrate przenoszenia danych hello między odłamków w połączeniu z hello niezbędne niezależnych mapy aktualizacji. Aby uzyskać szczegółowe informacje o wykorzystaniu hello yool scalania podziału, zobacz [omówienie scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
