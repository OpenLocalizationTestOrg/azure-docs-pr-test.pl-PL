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
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="e1aac-104">Serializować danych w Hadoop za pomocą hello Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="e1aac-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="e1aac-105">Witaj Avro SDK nie jest już obsługiwana przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e1aac-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="e1aac-106">Biblioteka Hello jest obsługiwana społeczności typu open source.</span><span class="sxs-lookup"><span data-stu-id="e1aac-106">hello library is open source community supported.</span></span> <span data-ttu-id="e1aac-107">źródeł Hello hello biblioteki znajdują się w [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="e1aac-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="e1aac-108">W tym temacie przedstawiono sposób toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize obiektów i innych danych struktury do strumieni toopersist ich toomemory, bazy danych lub pliku.</span><span class="sxs-lookup"><span data-stu-id="e1aac-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="e1aac-109">Zawiera także sposób toodeserialize ich toorecover hello oryginalnych obiektów.</span><span class="sxs-lookup"><span data-stu-id="e1aac-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="e1aac-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="e1aac-110">Apache Avro</span></span>
<span data-ttu-id="e1aac-111">Witaj <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementuje hello system serializacji danych Apache Avro hello środowiska Microsoft.NET.</span><span class="sxs-lookup"><span data-stu-id="e1aac-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="e1aac-112">Format wymiany danych binarnych Apache Avro zapewnia serializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="e1aac-113">Używa <a href="http://www.json.org" target="_blank">JSON</a> toodefine języka-schematu z niesprecyzowanym współdziałanie języków.</span><span class="sxs-lookup"><span data-stu-id="e1aac-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="e1aac-114">Dane serializowane w jednym języku mogą być odczytywane w innym.</span><span class="sxs-lookup"><span data-stu-id="e1aac-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="e1aac-115">C, C++, C#, Java, PHP, Python i Ruby są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e1aac-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="e1aac-116">Szczegółowe informacje o formacie hello znajdują się w hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span><span class="sxs-lookup"><span data-stu-id="e1aac-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="e1aac-117">Hello Microsoft Avro Library nie obsługuje części wywołania procedury zdalnej hello tej specyfikacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="e1aac-118">Reprezentacja Hello serializacji obiektu w hello Avro systemu składa się z dwóch części: schemat i wartością rzeczywistą.</span><span class="sxs-lookup"><span data-stu-id="e1aac-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="e1aac-119">schemacie Avro Hello opisano model danych niezależny od języka hello hello serializacji danych z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="e1aac-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="e1aac-120">Są one przedstawiane równolegle to binarna reprezentacja danych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="e1aac-121">O schematu hello niezależnie od hello binarna reprezentacja zezwala na każdym toobe obiektu napisane na platformie nie kosztów ogólnych na wartość, co serializacji szybkiego i hello reprezentacja małych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="e1aac-122">Scenariusz Hadoop Hello</span><span class="sxs-lookup"><span data-stu-id="e1aac-122">hello Hadoop scenario</span></span>
<span data-ttu-id="e1aac-123">format serializacji Apache Avro Hello jest powszechnie używany w innych środowiskach Apache Hadoop i usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1aac-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="e1aac-124">Avro zapewnia toorepresent wygodny sposób złożone struktury danych w ramach zadania MapReduce z Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e1aac-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="e1aac-125">Hello format plików Avro (pliku kontenera obiektu Avro) zostało zaprojektowane toosupport model programowania MapReduce hello rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="e1aac-126">Hello funkcji klucza, który umożliwia dystrybucję hello jest, że pliki hello są "podzielne" w hello sensie, że jeden wyszukiwać dowolne miejsce w pliku i rozpocząć odczytywanie od określonego bloku.</span><span class="sxs-lookup"><span data-stu-id="e1aac-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="e1aac-127">Serializacja w bibliotece Avro</span><span class="sxs-lookup"><span data-stu-id="e1aac-127">Serialization in Avro Library</span></span>
<span data-ttu-id="e1aac-128">Witaj Biblioteka .NET dla Avro obsługuje serializowania obiektów na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="e1aac-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="e1aac-129">**odbicie** -hello schematu JSON dla typów hello automatycznie składa się z danych hello atrybuty kontraktu toobe typów .NET hello serializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="e1aac-130">**ogólny rekordu** -schematu A JSON jawnie określonej w rekordzie reprezentowany przez hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) klasy podczas żadnych typów .NET są obecne toodescribe hello schematu dla hello toobe danych serializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="e1aac-131">Gdy schemat danych hello jest znany tooboth hello zapisywania i odczytywania strumienia hello, hello danych mogą być wysyłane bez jego schematu.</span><span class="sxs-lookup"><span data-stu-id="e1aac-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="e1aac-132">W przypadku stosowania pliku kontenera obiektu Avro schemat hello jest przechowywany w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="e1aac-133">Można określić innych parametrów, takich jak hello koder-dekoder, używany w przypadku kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="e1aac-134">Te scenariusze są opisane bardziej szczegółowo i przedstawia hello następujące przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="e1aac-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="e1aac-135">Zainstaluj biblioteki Avro</span><span class="sxs-lookup"><span data-stu-id="e1aac-135">Install Avro Library</span></span>
<span data-ttu-id="e1aac-136">Przed zainstalowaniem hello biblioteki, wymagane są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="e1aac-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="e1aac-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="e1aac-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="e1aac-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="e1aac-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="e1aac-139">Należy zauważyć, że ten hello Newtonsoft.Json.dll zależności jest pobierany automatycznie z instalacją hello hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="e1aac-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="e1aac-140">procedury Hello znajduje się w hello następujących sekcji:</span><span class="sxs-lookup"><span data-stu-id="e1aac-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="e1aac-141">Microsoft Avro Library Hello jest rozpowszechniany jako pakietu NuGet, który może zostać zainstalowany z programu Visual Studio za pośrednictwem hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="e1aac-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="e1aac-142">Wybierz hello **projektu** -> kartę **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="e1aac-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="e1aac-143">Wyszukaj "Microsoft.Hadoop.Avro" w hello **wyszukiwania Online** pole.</span><span class="sxs-lookup"><span data-stu-id="e1aac-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="e1aac-144">Kliknij przycisk hello **zainstalować** obok przycisku zbyt**Biblioteka programu Microsoft Azure HDInsight Avro**.</span><span class="sxs-lookup"><span data-stu-id="e1aac-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="e1aac-145">Należy pamiętać, że hello Newtonsoft.Json.dll (> = 6.0.4) zależności jest również pobierane automatycznie z hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="e1aac-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="e1aac-146">Witaj Microsoft Avro Library kod źródłowy jest dostępny na [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="e1aac-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="e1aac-147">Kompilacja za pomocą biblioteki Avro schematów</span><span class="sxs-lookup"><span data-stu-id="e1aac-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="e1aac-148">Witaj Microsoft Avro Library zawiera generowania kodu, narzędzie umożliwiające tworzenie typów C# automatycznie w oparciu o hello wcześniej zdefiniowany schematu JSON.</span><span class="sxs-lookup"><span data-stu-id="e1aac-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="e1aac-149">Narzędzie generowania kodu Hello nie jest rozpowszechniany jako binarnym pliku wykonywalnym, ale mogą być łatwo wbudowane za pośrednictwem hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="e1aac-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="e1aac-150">Pobierz plik zip hello hello najnowszej wersji zestawu SDK HDInsight kodu źródłowego z <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK dla platformy Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="e1aac-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="e1aac-151">(Kliknij hello **Pobierz** ikonę, nie hello **pobiera** kartę.)</span><span class="sxs-lookup"><span data-stu-id="e1aac-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="e1aac-152">Wyodrębnij hello katalogu tooa zestawu SDK HDInsight hello maszyny z programem .NET Framework 4 zainstalowane i połączone toohello Internetu do pobrania niezbędnych zależności pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e1aac-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="e1aac-153">Poniżej przyjęto założenie, że kod źródłowy hello jest tooC:\SDK wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="e1aac-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="e1aac-154">Przejdź do folderu toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools i uruchom build.bat.</span><span class="sxs-lookup"><span data-stu-id="e1aac-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="e1aac-155">(hello wywołania pliku MSBuild z 32-bitowych dystrybucji hello hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e1aac-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="e1aac-156">Jeśli chcesz toouse hello 64-bitowej wersji Edycja build.bat po komentarze hello wewnątrz pliku hello). Upewnij się, że hello kompilacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e1aac-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="e1aac-157">(W niektórych systemach MSBuild może powodować ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="e1aac-158">Ostrzeżenia te nie wpływają na powitania narzędzie tak długo, jak nie ma żadnych błędów kompilacji.)</span><span class="sxs-lookup"><span data-stu-id="e1aac-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="e1aac-159">Narzędzie Hello skompilowany znajduje się w C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="e1aac-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="e1aac-160">tooget zapoznać się z hello składni wiersza polecenia, wykonaj następujące polecenie z folderu hello, w którym znajduje się narzędzie generowania kodu hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="e1aac-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="e1aac-161">Narzędzie hello tootest, można wygenerować klas C# z hello próbki JSON schematu pliku podana z kodem źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="e1aac-162">Wykonaj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e1aac-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="e1aac-163">To powinien tooproduce dwóch C# plików w bieżącym katalogu hello: SensorData.cs i Location.cs.</span><span class="sxs-lookup"><span data-stu-id="e1aac-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="e1aac-164">toounderstand hello logikę, która używa narzędzie generowania kodu hello podczas konwertowania typów tooC # hello JSON schematu, zobacz plik hello GenerationVerification.feature znajduje się w C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="e1aac-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="e1aac-165">Przestrzenie nazw są wyodrębniane z hello schematu JSON, przy użyciu logiki hello opisany w pliku hello wspomnianego powyżej hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="e1aac-166">Przestrzenie nazw wyodrębnione ze schematu hello pierwszeństwo niezależnie od jest dostarczana z parametru /n hello w wierszu polecenia narzędzia hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="e1aac-167">Jeśli chcesz zawartych w schemacie hello hello toooverride w przestrzeni nazw, należy użyć parametru /nf hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="e1aac-168">Na przykład toochange wszystkie przestrzenie nazw z hello SampleJSONSchema.avsc toomy.own.nspace, wykonać hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e1aac-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="e1aac-169">Przykłady hello — informacje</span><span class="sxs-lookup"><span data-stu-id="e1aac-169">About hello samples</span></span>
<span data-ttu-id="e1aac-170">Sześciu przykłady podane w tym temacie przedstawiono różne scenariusze obsługiwane przez hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="e1aac-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="e1aac-171">Microsoft Avro Library Hello jest zaprojektowana toowork z jakimkolwiek strumieniu.</span><span class="sxs-lookup"><span data-stu-id="e1aac-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="e1aac-172">W tych przykładach danych steruje się za pośrednictwem strumieni pamięci zamiast strumieni plików lub baz danych, aby był prosty i spójności.</span><span class="sxs-lookup"><span data-stu-id="e1aac-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="e1aac-173">podejście Hello w środowisku produkcyjnym zależy od wymagań scenariusza dokładne hello, źródła danych i wolumin ograniczeń wydajności i innych czynników.</span><span class="sxs-lookup"><span data-stu-id="e1aac-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="e1aac-174">jak Hello pierwszy dwóch przykładach tooserialize i deserializuje dane na buforów strumienia pamięci przy użyciu odbicia i rodzajowy rekordów.</span><span class="sxs-lookup"><span data-stu-id="e1aac-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="e1aac-175">Witaj schematu w tych dwóch przypadkach zakłada, że toobe współużytkowane hello czytelników i zapisywania poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="e1aac-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="e1aac-176">Hello trzeci i czwarty przykładach pokazano sposób tooserialize i deserializować danych przy użyciu hello Avro obiektu kontenera plików.</span><span class="sxs-lookup"><span data-stu-id="e1aac-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="e1aac-177">Gdy dane są przechowywane w pliku kontenera Avro, schematem jest zawsze przechowywane z nim ponieważ hello schematu musi być udostępniony do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="e1aac-178">Witaj zawierające przykładowy hello pierwsze cztery przykłady można pobrać z hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">przykłady kodu Azure</a> lokacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="e1aac-179">Witaj piątej przykładzie pokazano sposób toouse koder-dekoder kompresji niestandardowych dla Avro obiektów kontenera plików.</span><span class="sxs-lookup"><span data-stu-id="e1aac-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="e1aac-180">Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">przykłady kodu Azure</a> lokacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="e1aac-181">Witaj szóstego pokazano sposób toouse Avro serializacji tooupload danych tooAzure magazynu obiektów Blob, a następnie analizować je przy użyciu usługi Hive z klastrem usługi HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="e1aac-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="e1aac-182">Można go pobrać z hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">przykłady kodu Azure</a> lokacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="e1aac-183">Oto łącza sześć próbek toohello opisem w temacie hello:</span><span class="sxs-lookup"><span data-stu-id="e1aac-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="e1aac-184"><a href="#Scenario1">**Serializacja za pomocą odbicia** </a> -hello schematu JSON dla typów toobe serializacji automatycznie składa się z danych hello atrybuty kontraktu.</span><span class="sxs-lookup"><span data-stu-id="e1aac-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="e1aac-185"><a href="#Scenario2">**Serializacja z rekordem ogólnego** </a> -schematu JSON hello jest jawnie określony w rekordzie, jeśli żaden typ .NET jest dostępny w celu odbicia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="e1aac-186"><a href="#Scenario3">**Serializacji przy użyciu plików kontenera obiektów za pomocą odbicia** </a> -schematu JSON hello jest automatycznie utworzony i udostępnione oraz hello serializowane dane za pomocą pliku kontenera obiektu Avro.</span><span class="sxs-lookup"><span data-stu-id="e1aac-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="e1aac-187"><a href="#Scenario4">**Serializacji przy użyciu plików kontenera obiektów z rekordem ogólnego** </a> -schematu JSON hello jest jawnie określone przed hello serializacji i udostępnione wraz z hello danych za pomocą pliku kontenera obiektu Avro.</span><span class="sxs-lookup"><span data-stu-id="e1aac-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="e1aac-188"><a href="#Scenario5">**Serializacji przy użyciu plików kontenera obiektów z koder-dekoder kompresji niestandardowych** </a> -hello przykładzie pokazano, jak toocreate Avro obiektów kontenera pliku z dostosowanych implementacją .NET hello Deflate danych kompresji kodera-dekodera.</span><span class="sxs-lookup"><span data-stu-id="e1aac-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="e1aac-189"><a href="#Scenario6">**Przy użyciu danych tooupload Avro hello usługi Microsoft Azure HDInsight** </a> — przykład Witaj przedstawiono, jak serializacji Avro współdziała z hello usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1aac-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="e1aac-190">Aktywne Azure subskrypcji i dostęp tooan Azure HDInsight klastra są wymagane toorun w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e1aac-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="e1aac-191"><a name="Scenario1"></a>Przykład 1: Serializacja za pomocą odbicia</span><span class="sxs-lookup"><span data-stu-id="e1aac-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="e1aac-192">Hello schematu JSON dla typów hello można atrybuty kontraktu hello C# obiektów toobe serializacji automatycznie utworzony przez hello Microsoft Avro Library za pośrednictwem odbicia z hello danych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="e1aac-193">Witaj Microsoft Avro Library tworzy [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) toobe pól hello tooidentify serializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="e1aac-194">W tym przykładzie obiekty ( **SensorData** klasy z elementem członkowskim **lokalizacji** struktury) są tooa serializowanego strumienia pamięci i z kolei jest deserializacji tego strumienia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="e1aac-195">Witaj wynik jest następnie porównywany toohello początkowej wystąpienia tooconfirm tego hello **SensorData** obiekt odzyskane jest identyczne toohello oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="e1aac-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="e1aac-196">Schemat Hello w tym przykładzie przyjęto, że toobe udostępniane między czytników hello i zapisywania, więc hello Avro obiektu kontenera format nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="e1aac-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="e1aac-197">Na przykład jak tooserialize i deserializować danych do buforów pamięci przy użyciu odbicia w formacie kontenera obiektu hello, gdy schemat hello można udostępniać dane hello, zobacz <a href="#Scenario3">serializacji przy użyciu plików kontenera obiektów za pomocą odbicia</a>.</span><span class="sxs-lookup"><span data-stu-id="e1aac-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="e1aac-198">Przykład 2: Serializacji z rekordem ogólny</span><span class="sxs-lookup"><span data-stu-id="e1aac-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="e1aac-199">Schematu JSON można jawnie określić w rekordzie ogólnym po odbicia nie można użyć, ponieważ nie może być reprezentowany hello danych za pośrednictwem klasy .NET z kontraktem danych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="e1aac-200">Ta metoda działa wolniej niż przy użyciu odbicia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-200">This method is slower than using reflection.</span></span> <span data-ttu-id="e1aac-201">W takich przypadkach hello schematu dla danych hello mogą być również dynamiczny, oznacza to, że nie jest znany w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="e1aac-202">Dane reprezentowane jako wartości rozdzielanych przecinkami (CSV) plików, których schematu jest nieznany, dopóki nie jest on przekształcany format Avro toohello w czasie wykonywania jest przykład tego rodzaju scenariusza dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="e1aac-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="e1aac-203">W tym przykładzie pokazano sposób toocreate i użyj [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly Określ schematu JSON, jak toopopulate go przy użyciu hello danych, a następnie jak tooserialize i do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="e1aac-204">wynik Hello jest następnie porównywany toohello tooconfirm wystąpieniem początkowej, która hello rekordu odzyskane jest identyczne toohello oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="e1aac-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="e1aac-205">Schemat Hello w tym przykładzie przyjęto, że toobe udostępniane między czytników hello i zapisywania, więc hello Avro obiektu kontenera format nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="e1aac-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="e1aac-206">Na przykład jak tooserialize i deserializować danych do buforów pamięci przy użyciu rekordu ogólny format kontenera obiektu hello gdy schemat hello musi być uwzględniona w danych serializacji hello, zobacz hello <a href="#Scenario4">serializacji przy użyciu kontenera obiektów pliki z rekordem ogólnego</a> przykład.</span><span class="sxs-lookup"><span data-stu-id="e1aac-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="e1aac-207">Przykład 3: Serializacji przy użyciu plików kontenera obiektów i serializacji za pomocą odbicia</span><span class="sxs-lookup"><span data-stu-id="e1aac-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="e1aac-208">W tym przykładzie jest podobny scenariusz toohello w hello <a href="#Scenario1"> pierwszym przykładzie</a>, gdzie schemat hello jest niejawnie określony za pomocą odbicia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="e1aac-209">Hello różnicą jest to, że w tym miejscu hello schematu nie zakłada, że toobe znane toohello reader, który deserializuje go.</span><span class="sxs-lookup"><span data-stu-id="e1aac-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="e1aac-210">Witaj **SensorData** toobe obiekty serializacji i ich niejawnie określony schemat są przechowywane w pliku Avro kontenera obiektu reprezentowanego przez hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) Klasa.</span><span class="sxs-lookup"><span data-stu-id="e1aac-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="e1aac-211">dane Hello jest serializowany w tym przykładzie z [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) i zdeserializowany z [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1aac-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="e1aac-212">wynik Hello jest następnie porównywany toohello początkowej wystąpień tooensure tożsamości.</span><span class="sxs-lookup"><span data-stu-id="e1aac-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="e1aac-213">Witaj w hello obiekt danych kompresowania pliku kontenera za pomocą domyślnego hello [ **Deflate** ] [ deflate-100] koder-dekoder kompresji z programu .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="e1aac-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="e1aac-214">Zobacz hello <a href="#Scenario5"> przykład piąty</a> w toolearn w tym temacie sposób toouse nowszej i wyższego poziomu wersji hello [ **Deflate** ] [ deflate-110] kompresji Koder-dekoder dostępnych w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e1aac-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="e1aac-215">Przykład 4: Serializacji przy użyciu plików kontenera obiektów i serializacji z rekordem ogólny</span><span class="sxs-lookup"><span data-stu-id="e1aac-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="e1aac-216">W tym przykładzie jest podobny scenariusz toohello w hello <a href="#Scenario2"> drugi przykład</a>, gdzie schemat hello jest jawnie określony z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="e1aac-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="e1aac-217">Hello różnicą jest to, że w tym miejscu hello schematu nie zakłada, że toobe znane toohello reader, który deserializuje go.</span><span class="sxs-lookup"><span data-stu-id="e1aac-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="e1aac-218">Witaj testowego zestawu danych zbieranych na listę wartości [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) obiektów za pomocą jawnie zdefiniowanych schematu JSON, a następnie zapisywana w pliku kontenera obiektu reprezentowanego przez hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="e1aac-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="e1aac-219">Ten plik kontenera tworzy zapisywania danych hello używane tooserialize, nieskompresowane tooa strumienia pamięci, który następnie jest zapisywana w pliku tooa.</span><span class="sxs-lookup"><span data-stu-id="e1aac-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="e1aac-220">Witaj [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parametru użytego do utworzenia czytnika danych hello Określa, że te dane nie jest skompresowany.</span><span class="sxs-lookup"><span data-stu-id="e1aac-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="e1aac-221">dane Hello jest następnie odczytu z pliku hello i deserializacji do kolekcji obiektów.</span><span class="sxs-lookup"><span data-stu-id="e1aac-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="e1aac-222">Ta kolekcja jest porównywany toohello początkowej listy Avro tooconfirm rejestruje, czy są one identyczne.</span><span class="sxs-lookup"><span data-stu-id="e1aac-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

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




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="e1aac-223">Przykład 5: Serializacji przy użyciu plików kontenera obiektów z koder-dekoder kompresji niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e1aac-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="e1aac-224">Witaj piątej przykładzie pokazano sposób toouse koder-dekoder kompresji niestandardowych dla Avro obiektów kontenera plików.</span><span class="sxs-lookup"><span data-stu-id="e1aac-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="e1aac-225">Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello [przykłady kodu Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) lokacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="e1aac-226">Hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) umożliwia użycie koder-dekoder kompresji opcjonalne (oprócz zbyt**Null** i **Deflate** ustawień domyślnych).</span><span class="sxs-lookup"><span data-stu-id="e1aac-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="e1aac-227">W tym przykładzie nie implementuje nowy koder-dekoder takich jak Snappy (wymieniony jako obsługiwany opcjonalne kodera-dekodera w hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="e1aac-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="e1aac-228">Pokazuje, jak toouse hello wdrożenia programu .NET Framework 4.5 hello [ **Deflate** ] [ deflate-110] koder-dekoder, który zapewnia lepszą algorytmu kompresji oparte na powitania [zlib](http://zlib.net/) biblioteki kompresji niż hello domyślnej wersji .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="e1aac-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

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

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="e1aac-229">Przykład 6: Przy użyciu danych tooupload Avro hello usługi Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1aac-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="e1aac-230">przykład szóstego Witaj przedstawiono niektóre programowania techniki pokrewne toointeracting przy użyciu usługi Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="e1aac-231">Przykład zawierający kod hello, w tym przykładzie mogą być pobierane ze hello [przykłady kodu Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) lokacji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="e1aac-232">przykład Witaj Witaj następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="e1aac-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="e1aac-233">Łączy tooan istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1aac-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="e1aac-234">Serializuje kilka plików CSV i przekazuje hello wynik tooAzure obiektu Blob magazynu.</span><span class="sxs-lookup"><span data-stu-id="e1aac-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="e1aac-235">(plików CSV hello są dystrybuowane wraz z przykładowych hello i reprezentują wyodrębniania z załączniku historyczne dane dystrybuowana [Infochimps](http://www.infochimps.com/) okres hello 1970 2010.</span><span class="sxs-lookup"><span data-stu-id="e1aac-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="e1aac-236">przykład Witaj odczytuje dane z pliku CSV, konwertuje hello tooinstances rekordy z hello **giełdowych** klasy, a następnie serializuje je przy użyciu odbicia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="e1aac-237">Definicja typu podstawowego jest tworzona na podstawie schematu JSON za pośrednictwem hello narzędzie generowania kodu Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="e1aac-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="e1aac-238">Tworzy nową tabelę zewnętrznych o nazwie **zasobów** w gałęzi i łączy go danych toohello przekazać hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="e1aac-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="e1aac-239">Wykonuje zapytanie przy użyciu Hive za pośrednictwem hello **zasobów** tabeli.</span><span class="sxs-lookup"><span data-stu-id="e1aac-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="e1aac-240">Ponadto próbki hello przeprowadza procedurę czyszczenia przed i po wykonaniu operacji głównych.</span><span class="sxs-lookup"><span data-stu-id="e1aac-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="e1aac-241">Podczas hello oczyszczania wszystkie hello powiązanych danych obiektów Blob platformy Azure i foldery zostały usunięte, a tabela Hive hello jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="e1aac-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="e1aac-242">Można także wywoływać procedury czyszczenia hello z hello przykładowy wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="e1aac-243">przykład Witaj ma hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="e1aac-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="e1aac-244">Aktywną subskrypcją Microsoft Azure i jego identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e1aac-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="e1aac-245">Certyfikat zarządzania dla subskrypcji hello przy hello odpowiedniego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="e1aac-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="e1aac-246">Witaj certyfikatu powinien być zainstalowany w hello bieżącego użytkownika prywatnego magazynu na powitania maszyna używana toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="e1aac-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="e1aac-247">Aktywnego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1aac-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="e1aac-248">Konto usługi Azure Storage połączone toohello klastra usługi HDInsight z hello poprzedniej wymagań wstępnych, wraz z hello odpowiedni klucz podstawowy lub pomocniczy dostęp.</span><span class="sxs-lookup"><span data-stu-id="e1aac-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="e1aac-249">Wszystkie informacje hello z wymagań wstępnych hello należy wprowadzić toohello przykładowy plik konfiguracyjny przed uruchomieniem próbki hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="e1aac-250">Istnieją dwa możliwe sposoby toodo go:</span><span class="sxs-lookup"><span data-stu-id="e1aac-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="e1aac-251">Edytowanie pliku app.config hello w katalogu głównym próbki hello i późniejszego kompilowania hello próbki</span><span class="sxs-lookup"><span data-stu-id="e1aac-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="e1aac-252">Najpierw utworzyć przykładowy hello, a następnie edytuj AvroHDISample.exe.config w katalog kompilacji hello</span><span class="sxs-lookup"><span data-stu-id="e1aac-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="e1aac-253">W obu przypadkach należy wykonywać wszystkie zmiany w hello  **<appSettings>**  w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e1aac-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="e1aac-254">Wykonaj hello komentarze w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="e1aac-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="e1aac-255">Witaj próbki jest Uruchom z wiersza polecenia hello, wykonując następujące polecenie (gdzie hello pliku .zip próbki hello założono tooC:\AvroHDISample toobe wyodrębnione; Jeśli hello odpowiednie w przeciwnym razie użyj ścieżki pliku) hello:</span><span class="sxs-lookup"><span data-stu-id="e1aac-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="e1aac-256">tooclean zapasowej hello klastra, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e1aac-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
