---
title: "aaaSerialize danych na platformie Azure Hadoop - Microsoft Avro Library – | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooserialize i deserializować danych na platformie Hadoop w usłudze HDInsight przy użyciu hello Microsoft Avro Library toopersist toomemory, bazy danych lub pliku."
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Serializować danych w Hadoop za pomocą hello Microsoft Avro Library

>[!NOTE]
>Witaj Avro SDK nie jest już obsługiwana przez firmę Microsoft. Biblioteka Hello jest obsługiwana społeczności typu open source. źródeł Hello hello biblioteki znajdują się w [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

W tym temacie przedstawiono sposób toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize obiektów i innych danych struktury do strumieni toopersist ich toomemory, bazy danych lub pliku. Zawiera także sposób toodeserialize ich toorecover hello oryginalnych obiektów.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Witaj <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementuje hello system serializacji danych Apache Avro hello środowiska Microsoft.NET. Format wymiany danych binarnych Apache Avro zapewnia serializacji. Używa <a href="http://www.json.org" target="_blank">JSON</a> toodefine języka-schematu z niesprecyzowanym współdziałanie języków. Dane serializowane w jednym języku mogą być odczytywane w innym. C, C++, C#, Java, PHP, Python i Ruby są obecnie obsługiwane. Szczegółowe informacje o formacie hello znajdują się w hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>. 

>[!NOTE]
>Hello Microsoft Avro Library nie obsługuje części wywołania procedury zdalnej hello tej specyfikacji.
>

Reprezentacja Hello serializacji obiektu w hello Avro systemu składa się z dwóch części: schemat i wartością rzeczywistą. schemacie Avro Hello opisano model danych niezależny od języka hello hello serializacji danych z formatu JSON. Są one przedstawiane równolegle to binarna reprezentacja danych. O schematu hello niezależnie od hello binarna reprezentacja zezwala na każdym toobe obiektu napisane na platformie nie kosztów ogólnych na wartość, co serializacji szybkiego i hello reprezentacja małych.

## <a name="hello-hadoop-scenario"></a>Scenariusz Hadoop Hello
format serializacji Apache Avro Hello jest powszechnie używany w innych środowiskach Apache Hadoop i usłudze Azure HDInsight. Avro zapewnia toorepresent wygodny sposób złożone struktury danych w ramach zadania MapReduce z Hadoop. Hello format plików Avro (pliku kontenera obiektu Avro) zostało zaprojektowane toosupport model programowania MapReduce hello rozproszonych. Hello funkcji klucza, który umożliwia dystrybucję hello jest, że pliki hello są "podzielne" w hello sensie, że jeden wyszukiwać dowolne miejsce w pliku i rozpocząć odczytywanie od określonego bloku.

## <a name="serialization-in-avro-library"></a>Serializacja w bibliotece Avro
Witaj Biblioteka .NET dla Avro obsługuje serializowania obiektów na dwa sposoby:

* **odbicie** -hello schematu JSON dla typów hello automatycznie składa się z danych hello atrybuty kontraktu toobe typów .NET hello serializacji.
* **ogólny rekordu** -schematu A JSON jawnie określonej w rekordzie reprezentowany przez hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) klasy podczas żadnych typów .NET są obecne toodescribe hello schematu dla hello toobe danych serializacji.

Gdy schemat danych hello jest znany tooboth hello zapisywania i odczytywania strumienia hello, hello danych mogą być wysyłane bez jego schematu. W przypadku stosowania pliku kontenera obiektu Avro schemat hello jest przechowywany w pliku hello. Można określić innych parametrów, takich jak hello koder-dekoder, używany w przypadku kompresji danych. Te scenariusze są opisane bardziej szczegółowo i przedstawia hello następujące przykłady kodu:

## <a name="install-avro-library"></a>Zainstaluj biblioteki Avro
Przed zainstalowaniem hello biblioteki, wymagane są następujące Hello:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 lub nowszy)

Należy zauważyć, że ten hello Newtonsoft.Json.dll zależności jest pobierany automatycznie z instalacją hello hello Microsoft Avro Library. procedury Hello znajduje się w hello następujących sekcji:

Microsoft Avro Library Hello jest rozpowszechniany jako pakietu NuGet, który może zostać zainstalowany z programu Visual Studio za pośrednictwem hello następujące procedury:

1. Wybierz hello **projektu** -> kartę **Zarządzaj pakietami NuGet...**
2. Wyszukaj "Microsoft.Hadoop.Avro" w hello **wyszukiwania Online** pole.
3. Kliknij przycisk hello **zainstalować** obok przycisku zbyt**Biblioteka programu Microsoft Azure HDInsight Avro**.

Należy pamiętać, że hello Newtonsoft.Json.dll (> = 6.0.4) zależności jest również pobierane automatycznie z hello Microsoft Avro Library.

Witaj Microsoft Avro Library kod źródłowy jest dostępny na [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Kompilacja za pomocą biblioteki Avro schematów
Witaj Microsoft Avro Library zawiera generowania kodu, narzędzie umożliwiające tworzenie typów C# automatycznie w oparciu o hello wcześniej zdefiniowany schematu JSON. Narzędzie generowania kodu Hello nie jest rozpowszechniany jako binarnym pliku wykonywalnym, ale mogą być łatwo wbudowane za pośrednictwem hello następujące procedury:

1. Pobierz plik zip hello hello najnowszej wersji zestawu SDK HDInsight kodu źródłowego z <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK dla platformy Hadoop</a>. (Kliknij hello **Pobierz** ikonę, nie hello **pobiera** kartę.)
2. Wyodrębnij hello katalogu tooa zestawu SDK HDInsight hello maszyny z programem .NET Framework 4 zainstalowane i połączone toohello Internetu do pobrania niezbędnych zależności pakietów NuGet. Poniżej przyjęto założenie, że kod źródłowy hello jest tooC:\SDK wyodrębnione.
3. Przejdź do folderu toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools i uruchom build.bat. (hello wywołania pliku MSBuild z 32-bitowych dystrybucji hello hello .NET Framework. Jeśli chcesz toouse hello 64-bitowej wersji Edycja build.bat po komentarze hello wewnątrz pliku hello). Upewnij się, że hello kompilacja zakończy się pomyślnie. (W niektórych systemach MSBuild może powodować ostrzeżenia. Ostrzeżenia te nie wpływają na powitania narzędzie tak długo, jak nie ma żadnych błędów kompilacji.)
4. Narzędzie Hello skompilowany znajduje się w C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget zapoznać się z hello składni wiersza polecenia, wykonaj następujące polecenie z folderu hello, w którym znajduje się narzędzie generowania kodu hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

Narzędzie hello tootest, można wygenerować klas C# z hello próbki JSON schematu pliku podana z kodem źródłowym hello. Wykonaj hello następujące polecenie:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

To powinien tooproduce dwóch C# plików w bieżącym katalogu hello: SensorData.cs i Location.cs.

toounderstand hello logikę, która używa narzędzie generowania kodu hello podczas konwertowania typów tooC # hello JSON schematu, zobacz plik hello GenerationVerification.feature znajduje się w C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Przestrzenie nazw są wyodrębniane z hello schematu JSON, przy użyciu logiki hello opisany w pliku hello wspomnianego powyżej hello. Przestrzenie nazw wyodrębnione ze schematu hello pierwszeństwo niezależnie od jest dostarczana z parametru /n hello w wierszu polecenia narzędzia hello. Jeśli chcesz zawartych w schemacie hello hello toooverride w przestrzeni nazw, należy użyć parametru /nf hello. Na przykład toochange wszystkie przestrzenie nazw z hello SampleJSONSchema.avsc toomy.own.nspace, wykonać hello następujące polecenie:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Przykłady hello — informacje
Sześciu przykłady podane w tym temacie przedstawiono różne scenariusze obsługiwane przez hello Microsoft Avro Library. Microsoft Avro Library Hello jest zaprojektowana toowork z jakimkolwiek strumieniu. W tych przykładach danych steruje się za pośrednictwem strumieni pamięci zamiast strumieni plików lub baz danych, aby był prosty i spójności. podejście Hello w środowisku produkcyjnym zależy od wymagań scenariusza dokładne hello, źródła danych i wolumin ograniczeń wydajności i innych czynników.

jak Hello pierwszy dwóch przykładach tooserialize i deserializuje dane na buforów strumienia pamięci przy użyciu odbicia i rodzajowy rekordów. Witaj schematu w tych dwóch przypadkach zakłada, że toobe współużytkowane hello czytelników i zapisywania poza pasmem.

Hello trzeci i czwarty przykładach pokazano sposób tooserialize i deserializować danych przy użyciu hello Avro obiektu kontenera plików. Gdy dane są przechowywane w pliku kontenera Avro, schematem jest zawsze przechowywane z nim ponieważ hello schematu musi być udostępniony do deserializacji.

Witaj zawierające przykładowy hello pierwsze cztery przykłady można pobrać z hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">przykłady kodu Azure</a> lokacji.

Witaj piątej przykładzie pokazano sposób toouse koder-dekoder kompresji niestandardowych dla Avro obiektów kontenera plików. Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">przykłady kodu Azure</a> lokacji.

Witaj szóstego pokazano sposób toouse Avro serializacji tooupload danych tooAzure magazynu obiektów Blob, a następnie analizować je przy użyciu usługi Hive z klastrem usługi HDInsight (Hadoop). Można go pobrać z hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">przykłady kodu Azure</a> lokacji.

Oto łącza sześć próbek toohello opisem w temacie hello:

* <a href="#Scenario1">**Serializacja za pomocą odbicia** </a> -hello schematu JSON dla typów toobe serializacji automatycznie składa się z danych hello atrybuty kontraktu.
* <a href="#Scenario2">**Serializacja z rekordem ogólnego** </a> -schematu JSON hello jest jawnie określony w rekordzie, jeśli żaden typ .NET jest dostępny w celu odbicia.
* <a href="#Scenario3">**Serializacji przy użyciu plików kontenera obiektów za pomocą odbicia** </a> -schematu JSON hello jest automatycznie utworzony i udostępnione oraz hello serializowane dane za pomocą pliku kontenera obiektu Avro.
* <a href="#Scenario4">**Serializacji przy użyciu plików kontenera obiektów z rekordem ogólnego** </a> -schematu JSON hello jest jawnie określone przed hello serializacji i udostępnione wraz z hello danych za pomocą pliku kontenera obiektu Avro.
* <a href="#Scenario5">**Serializacji przy użyciu plików kontenera obiektów z koder-dekoder kompresji niestandardowych** </a> -hello przykładzie pokazano, jak toocreate Avro obiektów kontenera pliku z dostosowanych implementacją .NET hello Deflate danych kompresji kodera-dekodera.
* <a href="#Scenario6">**Przy użyciu danych tooupload Avro hello usługi Microsoft Azure HDInsight** </a> — przykład Witaj przedstawiono, jak serializacji Avro współdziała z hello usługi HDInsight. Aktywne Azure subskrypcji i dostęp tooan Azure HDInsight klastra są wymagane toorun w tym przykładzie.

## <a name="Scenario1"></a>Przykład 1: Serializacja za pomocą odbicia
Hello schematu JSON dla typów hello można atrybuty kontraktu hello C# obiektów toobe serializacji automatycznie utworzony przez hello Microsoft Avro Library za pośrednictwem odbicia z hello danych. Witaj Microsoft Avro Library tworzy [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) toobe pól hello tooidentify serializacji.

W tym przykładzie obiekty ( **SensorData** klasy z elementem członkowskim **lokalizacji** struktury) są tooa serializowanego strumienia pamięci i z kolei jest deserializacji tego strumienia. Witaj wynik jest następnie porównywany toohello początkowej wystąpienia tooconfirm tego hello **SensorData** obiekt odzyskane jest identyczne toohello oryginalnego.

Schemat Hello w tym przykładzie przyjęto, że toobe udostępniane między czytników hello i zapisywania, więc hello Avro obiektu kontenera format nie jest wymagana. Na przykład jak tooserialize i deserializować danych do buforów pamięci przy użyciu odbicia w formacie kontenera obiektu hello, gdy schemat hello można udostępniać dane hello, zobacz <a href="#Scenario3">serializacji przy użyciu plików kontenera obiektów za pomocą odbicia</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Przykład 2: Serializacji z rekordem ogólny
Schematu JSON można jawnie określić w rekordzie ogólnym po odbicia nie można użyć, ponieważ nie może być reprezentowany hello danych za pośrednictwem klasy .NET z kontraktem danych. Ta metoda działa wolniej niż przy użyciu odbicia. W takich przypadkach hello schematu dla danych hello mogą być również dynamiczny, oznacza to, że nie jest znany w czasie kompilacji. Dane reprezentowane jako wartości rozdzielanych przecinkami (CSV) plików, których schematu jest nieznany, dopóki nie jest on przekształcany format Avro toohello w czasie wykonywania jest przykład tego rodzaju scenariusza dynamicznej.

W tym przykładzie pokazano sposób toocreate i użyj [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly Określ schematu JSON, jak toopopulate go przy użyciu hello danych, a następnie jak tooserialize i do deserializacji. wynik Hello jest następnie porównywany toohello tooconfirm wystąpieniem początkowej, która hello rekordu odzyskane jest identyczne toohello oryginalnego.

Schemat Hello w tym przykładzie przyjęto, że toobe udostępniane między czytników hello i zapisywania, więc hello Avro obiektu kontenera format nie jest wymagana. Na przykład jak tooserialize i deserializować danych do buforów pamięci przy użyciu rekordu ogólny format kontenera obiektu hello gdy schemat hello musi być uwzględniona w danych serializacji hello, zobacz hello <a href="#Scenario4">serializacji przy użyciu kontenera obiektów pliki z rekordem ogólnego</a> przykład.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Przykład 3: Serializacji przy użyciu plików kontenera obiektów i serializacji za pomocą odbicia
W tym przykładzie jest podobny scenariusz toohello w hello <a href="#Scenario1"> pierwszym przykładzie</a>, gdzie schemat hello jest niejawnie określony za pomocą odbicia. Hello różnicą jest to, że w tym miejscu hello schematu nie zakłada, że toobe znane toohello reader, który deserializuje go. Witaj **SensorData** toobe obiekty serializacji i ich niejawnie określony schemat są przechowywane w pliku Avro kontenera obiektu reprezentowanego przez hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) Klasa.

dane Hello jest serializowany w tym przykładzie z [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) i zdeserializowany z [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). wynik Hello jest następnie porównywany toohello początkowej wystąpień tooensure tożsamości.

Witaj w hello obiekt danych kompresowania pliku kontenera za pomocą domyślnego hello [ **Deflate** ] [ deflate-100] koder-dekoder kompresji z programu .NET Framework 4. Zobacz hello <a href="#Scenario5"> przykład piąty</a> w toolearn w tym temacie sposób toouse nowszej i wyższego poziomu wersji hello [ **Deflate** ] [ deflate-110] kompresji Koder-dekoder dostępnych w programie .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Przykład 4: Serializacji przy użyciu plików kontenera obiektów i serializacji z rekordem ogólny
W tym przykładzie jest podobny scenariusz toohello w hello <a href="#Scenario2"> drugi przykład</a>, gdzie schemat hello jest jawnie określony z formatu JSON. Hello różnicą jest to, że w tym miejscu hello schematu nie zakłada, że toobe znane toohello reader, który deserializuje go.

Witaj testowego zestawu danych zbieranych na listę wartości [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) obiektów za pomocą jawnie zdefiniowanych schematu JSON, a następnie zapisywana w pliku kontenera obiektu reprezentowanego przez hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) klasy. Ten plik kontenera tworzy zapisywania danych hello używane tooserialize, nieskompresowane tooa strumienia pamięci, który następnie jest zapisywana w pliku tooa. Witaj [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parametru użytego do utworzenia czytnika danych hello Określa, że te dane nie jest skompresowany.

dane Hello jest następnie odczytu z pliku hello i deserializacji do kolekcji obiektów. Ta kolekcja jest porównywany toohello początkowej listy Avro tooconfirm rejestruje, czy są one identyczne.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Przykład 5: Serializacji przy użyciu plików kontenera obiektów z koder-dekoder kompresji niestandardowych
Witaj piątej przykładzie pokazano sposób toouse koder-dekoder kompresji niestandardowych dla Avro obiektów kontenera plików. Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello [przykłady kodu Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) lokacji.

Hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) umożliwia użycie koder-dekoder kompresji opcjonalne (oprócz zbyt**Null** i **Deflate** ustawień domyślnych). W tym przykładzie nie implementuje nowy koder-dekoder takich jak Snappy (wymieniony jako obsługiwany opcjonalne kodera-dekodera w hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)). Pokazuje, jak toouse hello wdrożenia programu .NET Framework 4.5 hello [ **Deflate** ] [ deflate-110] koder-dekoder, który zapewnia lepszą algorytmu kompresji oparte na powitania [zlib](http://zlib.net/) biblioteki kompresji niż hello domyślnej wersji .NET Framework 4.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Przykład 6: Przy użyciu danych tooupload Avro hello usługi Microsoft Azure HDInsight
przykład szóstego Witaj przedstawiono niektóre programowania techniki pokrewne toointeracting przy użyciu usługi Azure HDInsight hello. Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello [przykłady kodu Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) lokacji.

przykład Witaj Witaj następujących zadań:

* Łączy tooan istniejącego klastra usługi HDInsight.
* Serializuje kilka plików CSV i przekazuje hello wynik tooAzure obiektu Blob magazynu. (plików CSV hello są dystrybuowane wraz z przykładowych hello i reprezentują wyodrębniania z załączniku historyczne dane dystrybuowana [Infochimps](http://www.infochimps.com/) okres hello 1970 2010. przykład Witaj odczytuje dane z pliku CSV, konwertuje hello tooinstances rekordy z hello **giełdowych** klasy, a następnie serializuje je przy użyciu odbicia. Definicja typu podstawowego jest tworzona na podstawie schematu JSON za pośrednictwem hello narzędzie generowania kodu Microsoft Avro Library.
* Tworzy nową tabelę zewnętrznych o nazwie **zasobów** w gałęzi i łączy go danych toohello przekazać hello poprzedniego kroku.
* Wykonuje zapytanie przy użyciu Hive za pośrednictwem hello **zasobów** tabeli.

Ponadto próbki hello przeprowadza procedurę czyszczenia przed i po wykonaniu operacji głównych. Podczas hello oczyszczania wszystkie hello powiązanych danych obiektów Blob platformy Azure i foldery zostały usunięte, a tabela Hive hello jest usuwana. Można także wywoływać procedury czyszczenia hello z hello przykładowy wiersz polecenia.

przykład Witaj ma hello następujące wymagania wstępne:

* Aktywną subskrypcją Microsoft Azure i jego identyfikatora subskrypcji.
* Certyfikat zarządzania dla subskrypcji hello przy hello odpowiedniego klucza prywatnego. Witaj certyfikatu powinien być zainstalowany w hello bieżącego użytkownika prywatnego magazynu na powitania maszyna używana toorun hello próbki.
* Aktywnego klastra usługi HDInsight.
* Konto usługi Azure Storage połączone toohello klastra usługi HDInsight z hello poprzedniej wymagań wstępnych, wraz z hello odpowiedni klucz podstawowy lub pomocniczy dostęp.

Wszystkie informacje hello z wymagań wstępnych hello należy wprowadzić toohello przykładowy plik konfiguracyjny przed uruchomieniem próbki hello. Istnieją dwa możliwe sposoby toodo go:

* Edytowanie pliku app.config hello w katalogu głównym próbki hello i późniejszego kompilowania hello próbki
* Najpierw utworzyć przykładowy hello, a następnie edytuj AvroHDISample.exe.config w katalog kompilacji hello

W obu przypadkach należy wykonywać wszystkie zmiany w hello  **<appSettings>**  w sekcji Ustawienia. Wykonaj hello komentarze w pliku hello.
Witaj próbki jest Uruchom z wiersza polecenia hello, wykonując następujące polecenie (gdzie hello pliku .zip próbki hello założono tooC:\AvroHDISample toobe wyodrębnione; Jeśli hello odpowiednie w przeciwnym razie użyj ścieżki pliku) hello:

    AvroHDISample run C:\AvroHDISample\Data

tooclean zapasowej hello klastra, uruchom następujące polecenie hello:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
