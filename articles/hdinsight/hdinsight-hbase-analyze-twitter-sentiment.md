---
title: "aaaAnalyze w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodo wskaźniki nastrojów klientów w czasie rzeczywistym analizy danych big data z Twitter, za pomocą bazy danych HBase w klastrze HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jgao
ms.openlocfilehash: 87e5c0c0a90d222a3f0bc3c3f3fce1e938320480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a>Analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight
Dowiedz się, jak w czasie rzeczywistym toodo [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) z danych big data w serwisie Twitter przy użyciu klastra HBase w usłudze HDInsight.

Społecznościowych witryn sieci Web są jednym z głównych wymusza pobudzenie hello przyjmowania danych big data. Publiczny interfejsów API dostarczonych przez witryn, takie jak Twitter są użyteczne źródło danych do analizowania i zrozumienie trendów popularnych. W tym samouczku opracowywania konsoli przesyłania strumieniowego aplikacji usługi i następujących hello tooperform aplikacji ASP.NET w sieci web:

![HDInsight HBase analizowanie Twitter wskaźniki nastrojów klientów][img-app-arch]

* przesyłanie strumieniowe aplikacji Hello

  * Pobierz oznakowane geograficznie tweetów w czasie rzeczywistym za pomocą usługi Twitter hello przesyłania strumieniowego interfejsu API
  * Ocena hello wskaźniki nastrojów klientów tych tweetów
  * przechowywanie hello wskaźniki nastrojów klientów informacji w bazie danych HBase przy użyciu hello Microsoft HBase SDK
* Witaj aplikacji witryny sieci Web Azure

  * Wykres hello w czasie rzeczywistym statystyczne na map Bing przy użyciu aplikacji sieci web ASP.NET. Wizualizacja tweetów hello jest podobne toohello po zrzut ekranu:

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    Jesteś tooquery stanie tweety z niektórych tooget słów kluczowych w pewnym sensie jeżeli opinia hello wyrażone w tweetów hello jest dodatnią, ujemną lub neutralnym.

Kompletne przykładowe rozwiązanie Visual Studio można znaleźć w witrynie GitHub: [czasu rzeczywistego społecznościowych wskaźniki nastrojów klientów analizy aplikacji](https://github.com/maxluk/tweet-sentiment).

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Klaster HBase w usłudze HDInsight**. Aby uzyskać instrukcje tworzenia klastrów, zobacz [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight HBase][hbase-get-started]. 

* **Stacja robocza** z programu Visual Studio 2013/2015/2017 zainstalowane. Aby uzyskać instrukcje, zobacz [Instalowanie programu Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).

## <a name="create-a-twitter-application-id-and-secrets"></a>Utwórz identyfikator aplikacji usługi Twitter i kluczy tajnych
Witaj Twitter interfejsów API przesyłania strumieniowego [OAuth](http://oauth.net/) tooauthorize żądań. Hello pierwszy krok toouse OAuth jest toocreate nowej aplikacji na powitania witryny dla deweloperów usługi Twitter.

**Identyfikator aplikacji usługi Twitter toocreate i kluczy tajnych**

1. Zaloguj się za[aplikacji w usłudze Twitter](https://apps.twitter.com/). Kliknij przycisk hello **Zamów teraz** łącza, jeśli nie masz konta w usłudze Twitter.
2. Kliknij przycisk **Utwórz nową aplikację**.
3. Wprowadź **nazwa**, **opis**, i **witryny sieci Web**. Nazwa aplikacji Hello Twitter musi być unikatowa. pola Website Hello naprawdę nie jest używany. Toobe nie ma prawidłowego adresu URL.
4. Sprawdź **tak, zgadzam się**, a następnie kliknij przycisk **tworzenie aplikacji Twitter**.
5. Kliknij przycisk hello **uprawnienia** , a następnie kliknij pozycję **tylko do odczytu**. uprawnienia tylko do odczytu Hello jest wystarczająca dla tego samouczka.
6. Kliknij przycisk hello **kluczy i tokenów dostępu** kartę.
7. Kliknij przycisk **Utwórz moje tokenu dostępu** na powitania u dołu strony hello.
9. Kopiuj hello **konsumenta (klucz interfejsu API)**, **klucz tajny klienta (klucz tajny interfejsu API)**, **token dostępu**, i **klucz tajny tokenu dostępu** wartości. Te wartości muszą się później w samouczku hello.

    > ! Przycisk Test OAuth hello [Uwaga] nie działa.

## <a name="create-twitter-streaming-service"></a>Utwórz przesyłania strumieniowego usługi Twitter
Należy toocreate tweetów tooget aplikacji obliczania wyniku wskaźniki nastrojów klientów tweet i wysyłać tooHBase słowa tweet hello przetworzone.

**przesyłanie strumieniowe aplikacji hello toocreate**

1. Otwórz **programu Visual Studio**i Utwórz aplikację konsoli języka Visual C# o nazwie **TweetSentimentStreaming**.
2. Z **Konsola Menedżera pakietów**Uruchom hello następujących poleceń:

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    Te polecenia zainstalować hello [zestawu .NET SDK HBase](https://www.nuget.org/packages/Microsoft.HBase.Client/) pakiet, który jest klaster HBase hello tooaccess powitania klienta biblioteki i hello [Tweetinvi interfejsu API](https://www.nuget.org/packages/TweetinviAPI/) pakietu, który jest używany tooaccess hello interfejs API usługi Twitter.

   > [!NOTE]
   > Przykładowe Hello używane w tym artykule przetestowano przy użyciu wersji hello wymienione powyżej.  Możesz usunąć hello — wersja przełącznika tooinstall hello najnowszej wersji.
   >
   >
3. Z **Eksploratora rozwiązań**, Dodaj **System.Configuration** toohello odwołania.
4. Dodaj projekt toohello nowego pliku klasy o nazwie **HBaseWriter.cs**i Zastąp kod hello hello następujący:

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //hello default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter hello Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and hello punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting tooHBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects tooHBase, loads hello sentiment dictionary, and starts hello thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create hello HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting tooHBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("hello remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue hello Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object toobe written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split hello Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on hello words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in hello Tweet add a row toohello HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns toohello row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) tooHBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write hello Tweet by words cell set toohello HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. Ustaw stałe hello w poprzednim kodzie hello, w tym **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**i DICTIONARYFILENAME. Witaj DICTIONARYFILENAME jest hello nazwę pliku i lokalizację hello hello direction.tsv.  można pobrać z pliku Hello **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**. Jeśli nazwa tabeli bazy danych HBase hello toochange, należy odpowiednio zmienić nazwę tabeli hello w aplikacji sieci web hello.
6. Otwórz **Program.cs**i Zastąp kod hello hello następujące czynności:

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(90, -180), new Coordinates(-90,180));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets tooHBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. Ustaw hello stałe, włączając **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** i **TWITTERAPPAPISECRET**.

Witaj toorun przesyłania strumieniowego usługi, naciśnij klawisz **F5**. Zrzut ekranu aplikacji konsoli hello jest następujący Hello:

![hdinsight.hbase.twitter.sentiment.Streaming.Service][img-streaming-service]

Zachowaj hello przesyłania strumieniowego aplikacji konsolowej działającej podczas opracowywania aplikacji sieci web hello, więc więcej toouse danych. wstawione do tabeli hello danych hello tooexamine, można użyć powłoki HBase. Zobacz [Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).

## <a name="visualize-real-time-sentiment"></a>Wizualizuj wskaźniki nastrojów klientów w czasie rzeczywistym
W tej sekcji Aby utworzyć dane ASP.NET MVC sieci web aplikacji tooread hello wskaźniki nastrojów klientów w czasie rzeczywistym z bazy danych HBase i kreślenia danych hello na mapy Bing.

**toocreate aplikacji sieci Web programu ASP.NET MVC**

1. Otwórz program Visual Studio.
2. Kliknij przycisk **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
3. Wprowadź hello następujących informacji:

   * Szablon kategorii: **Visual C# / sieci Web**
   * Szablon: **aplikacji sieci Web ASP.NET**
   * Nazwa: **TweetSentimentWeb**
   * Lokalizacja: **C:\Tutorials**
4. Kliknij przycisk **OK**.
5. W **wybierz szablon**, kliknij przycisk **MVC**.
6. W **Microsoft Azure**, kliknij przycisk **Zarządzaj subskrypcjami**.
7. Z **Zarządzanie subskrypcji platformy Microsoft Azure**, kliknij przycisk **Zaloguj**.
8. Wprowadź swoje poświadczenia usługi Azure. Informacje o subskrypcji platformy Azure jest wyświetlany na powitania **kont** kartę.
9. Kliknij przycisk **Zamknij** tooclose hello **Zarządzanie subskrypcji platformy Microsoft Azure** okna.
10. Z **nowy projekt ASP.NET - TweetSentimentWeb**, kliknij przycisk **OK**.
11. Z **Konfiguruj ustawienia witryny Microsoft Azure**, wybierz pozycję hello **Region** czyli najbliższej tooyou. Nie trzeba toospecify serwera bazy danych.
12. Kliknij przycisk **OK**.

**pakiety NuGet tooinstall**

1. Z hello **narzędzia** menu, kliknij przycisk **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**. panel konsoli Hello jest otwarty u dołu hello hello strony.
2. Użyj hello następujące polecenie tooinstall hello [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) pakiet, który jest powitania klienta biblioteki tooaccess klastra HBase:

        Install-Package Microsoft.HBase.Client

**tooadd HBaseReader — klasa**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentiment**.
2. Kliknij prawym przyciskiem myszy **modele**, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.
3. W hello **nazwa** wpisz **HBaseReader.cs**, a następnie kliknij przycisk **Dodaj**.
4. Zastąp kod hello hello następujące czynności:

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // hello constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from hello HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering hello data from hello past 6 hours hello row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find hello cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. Witaj wewnątrz **HBaseReader** klasy, zmień wartości stałych hello w następujący sposób:

   * **CLUSTERNAME**: hello HBase nazwę klastra, na przykład *https://<HBaseClusterName>.azurehdinsight.net/*.
   * **HADOOPUSERNAME**: nazwa użytkownika użytkownika hello HBase klastra usługi Hadoop. Nazwa domyślnej Hello jest *admin*.
   * **HADOOPUSERPASSWORD**: hasło użytkownika hello HBase klastra usługi Hadoop.
   * **HBASETABLENAME** = "tweets_by_words";

     Nazwa tabeli bazy danych HBase Hello jest **"tweets_by_words";**. Witaj wartości muszą być zgodne wartości hello wysłanych w hello przesyłania strumieniowego usługi, dzięki czemu hello aplikacji sieci web odczytuje dane hello z hello tej samej tabeli HBase.

**Kontroler TweetsController tooadd**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**.
2. Kliknij prawym przyciskiem myszy **kontrolerów**, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.
3. Kliknij przycisk **kontrolera 2 interfejsu API sieci Web — pusty**, a następnie kliknij przycisk **Dodaj**.
4. W hello **nazwy kontrolera** wpisz **TweetsController**, a następnie kliknij przycisk **Dodaj**.
5. Z **Eksploratora rozwiązań**, kliknij dwukrotnie plik hello tooopen TweetsController.cs.
6. Modyfikowanie pliku hello tak wygląda jak poniżej hello:

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

**tooadd heatmap.js**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**.
2. Kliknij prawym przyciskiem myszy **skryptów**, kliknij przycisk **Dodaj**, kliknij przycisk **plik JavaScript**.
3. W hello **nazwa elementu** wpisz **heatmap.js**.
4. Wklej powitania po kod do pliku hello. Kod Hello zapisał Alastair Aitchison. Aby uzyskać więcej informacji, zobacz [AJAX mapy Bing w wersji 7 HeatMap biblioteki](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used tooadd a heatmap
        * overlay on a Bing Maps v7 control. hello intensity and temperature palette
        * of hello heatmap are designed toobe easily customisable.
        *
        * Requirements:
        * hello heatmap layer itself is created dynamically on hello client-side using
        * hello HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love toohear from you!
        *
        * Usage:
        * hello HeatMapLayer constructor requires:
        * - A reference tooa map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters toocustomise hello appearance of hello layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of hello map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function toobe fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create hello canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in hello constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from hello suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up hello event handler tooredraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets hello heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient toohello intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get hello alpha of this pixel
                    if (a != 0) { // If there is any data tooplot
                        pix[p] = _temperaturemap[a]; // set hello red value of hello gradient that corresponds toothis alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set hello green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set hello blue value based on alpha
                    }
                    p += 4; // Move on toohello next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets hello heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method toodraw hello heatmap
            function _createHeatMap() {
                // Ensure hello canvas matches hello current dimensions of hello map
                // This also has hello effect of resetting hello canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate hello pixel radius of each heatpoint at hello current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long toopixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create hello Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw hello heatpoint onto hello canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply hello specified colour gradient toohello intensity map
                _colouriseHeatMap();

                // Call hello callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which hello heatmap is created
            this.SetPoints = function (locations) {
                // Reset hello existing heatmap layer
                _clearHeatMap();
                // Pass in hello new set of locations
                _setPoints(locations);
                // Recreate hello layer
                _createHeatMap();
            }

            // Removes hello heatmap layer from hello DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call hello initialisation routine
            _init();
        };

        // Call hello Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

**tooadd twitterStream.js**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**.
2. Kliknij prawym przyciskiem myszy **skryptów**, kliknij przycisk **Dodaj**, kliknij przycisk **plik JavaScript**.
3. W hello **nazwa elementu** wpisz**twitterStream.js**.
4. Skopiuj i Wklej powitania po kod do pliku hello:

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize hello map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load hello Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet toohello heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

**toomodify hello layout.cshtml**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**, rozwiń węzeł **widoków**, rozwiń węzeł **Shared**, a następnie kliknij dwukrotnie _**Layout.cshtml**.
2. Zastąp zawartość hello hello następujące czynności:

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

**Witaj toomodify Index.cshtml**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**, rozwiń węzeł **widoków**, rozwiń węzeł **Home**, a następnie kliknij dwukrotnie  **Index.cshtml**.
2. Zastąp zawartość hello hello następujące czynności:

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

**pliku site.css hello toomodify**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**, rozwiń węzeł **zawartości**, a następnie kliknij dwukrotnie **Site.css**.
2. Dołącz hello następującego pliku toohello kodu:

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

**Plik global.asax hello toomodify**

1. Z **Eksploratora rozwiązań**, rozwiń węzeł **TweetSentimentWeb**, a następnie kliknij dwukrotnie **Global.asax**.
2. Dodaj następujące hello **przy użyciu** instrukcji:

        using System.Web.Http;
3. Dodaj następujące wiersze wewnątrz hello hello **Application_Start()** funkcji:

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    Zmodyfikuj rejestracji hello hello interfejsu API tras toomake hello interfejsu API sieci Web kontrolera pracy w aplikacji MVC hello.

**Aplikacja sieci web hello toorun**

1. Sprawdź, czy pozwala zobaczyć zmiany w czasie rzeczywistym hello tego hello przesyłania strumieniowego aplikacji konsoli usługi jest nadal uruchomiona.
2. Naciśnij klawisz **F5** aplikacji sieci web hello toorun:

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. W polu tekstowym hello, wprowadź słowo kluczowe, a następnie kliknij przycisk **Przejdź**.  W zależności od hello zbieranych danych w tabeli HBase hello nie można znaleźć niektórych słów kluczowych. Spróbuj niektóre typowe słowa kluczowe, takie jak "lubisz", "xbox" i "playstation."
4. Przełącz między **dodatnią**, **Neutral**, i **ujemna** toocompare wskaźniki nastrojów klientów na temat hello.
5. Let hello usługi przesyłania strumieniowego, uruchom na inną godzinę, a następnie wyszukiwania hello same słowa kluczowe i porównywania wyników hello.

Opcjonalnie można wdrożyć tooAzure aplikacji hello witryn sieci Web. Aby uzyskać instrukcje, zobacz [Rozpoczynanie pracy z witryn sieci Web platformy Azure i ASP.NET][website-get-started].

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób tooget tweetów, analizuje hello wskaźniki nastrojów klientów tweetów Zapisz hello wskaźniki nastrojów klientów danych tooHBase oraz obecne hello w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów tooBing mapowania danych. toolearn więcej, zobacz:

* [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md)
* [Analizowanie danych z serwisu Twitter na platformie Hadoop w usłudze HDInsight][hdinsight-analyze-twitter-data]
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-delay-data]
* [Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: ./media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: ./media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
