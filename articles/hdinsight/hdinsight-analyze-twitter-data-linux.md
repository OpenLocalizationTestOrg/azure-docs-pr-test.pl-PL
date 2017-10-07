---
title: "aaaAnalyze Twitter danych za pomocą Apache Hive - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse korzystać z Hive i Hadoop w HDInsight tootransform nieprzetworzone dane w serwisie TWitter w tabeli programu Hive można wyszukiwać."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="aedd7-103">Analizowanie danych Twitter przy użyciu Hive i Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="aedd7-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="aedd7-104">Dowiedz się, jak toouse Apache Hive tooprocess danych Twitter.</span><span class="sxs-lookup"><span data-stu-id="aedd7-104">Learn how toouse Apache Hive tooprocess Twitter data.</span></span> <span data-ttu-id="aedd7-105">wynik Hello znajduje się lista Twitter użytkowników, którzy wysyłane hello większość tweetów, które zawierają określony wyraz.</span><span class="sxs-lookup"><span data-stu-id="aedd7-105">hello result is a list of Twitter users who sent hello most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aedd7-106">kroki Hello w tym dokumencie zostały przetestowane na 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aedd7-106">hello steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="aedd7-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="aedd7-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aedd7-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="aedd7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-hello-data"></a><span data-ttu-id="aedd7-109">Pobierz dane hello</span><span class="sxs-lookup"><span data-stu-id="aedd7-109">Get hello data</span></span>

<span data-ttu-id="aedd7-110">Twitter umożliwia tooretrieve hello [dane dla każdego tweet](https://dev.twitter.com/docs/platform-objects/tweets) jako dokument JavaScript Object Notation (JSON) za pośrednictwem interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="aedd7-110">Twitter allows you tooretrieve hello [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="aedd7-111">[OAuth](http://oauth.net) jest wymagany dla uwierzytelniania toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="aedd7-111">[OAuth](http://oauth.net) is required for authentication toohello API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="aedd7-112">Utwórz aplikację usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="aedd7-112">Create a Twitter application</span></span>

1. <span data-ttu-id="aedd7-113">W przeglądarce sieci web, zaloguj się za[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="aedd7-113">From a web browser, sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="aedd7-114">Kliknij przycisk hello **rejestracji teraz** łącza, jeśli nie masz konta w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="aedd7-114">Click hello **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="aedd7-115">Kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="aedd7-116">Wprowadź **nazwa**, **opis**, **witryny sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="aedd7-117">Można uzupełnić adres URL hello **witryny sieci Web** pola.</span><span class="sxs-lookup"><span data-stu-id="aedd7-117">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="aedd7-118">Witaj w poniższej tabeli przedstawiono niektóre przykładowe wartości toouse:</span><span class="sxs-lookup"><span data-stu-id="aedd7-118">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="aedd7-119">Pole</span><span class="sxs-lookup"><span data-stu-id="aedd7-119">Field</span></span> | <span data-ttu-id="aedd7-120">Wartość</span><span class="sxs-lookup"><span data-stu-id="aedd7-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="aedd7-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="aedd7-121">Name</span></span> |<span data-ttu-id="aedd7-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="aedd7-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="aedd7-123">Opis</span><span class="sxs-lookup"><span data-stu-id="aedd7-123">Description</span></span> |<span data-ttu-id="aedd7-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="aedd7-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="aedd7-125">Witryna sieci Web</span><span class="sxs-lookup"><span data-stu-id="aedd7-125">Website</span></span> |<span data-ttu-id="aedd7-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="aedd7-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="aedd7-127">Sprawdź **tak, zgadzam się**, a następnie kliknij przycisk **tworzenie aplikacji Twitter**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="aedd7-128">Kliknij przycisk hello **uprawnienia** kartę hello domyślne uprawnienia **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-128">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span>

6. <span data-ttu-id="aedd7-129">Kliknij przycisk hello **kluczy i tokenów dostępu** kartę.</span><span class="sxs-lookup"><span data-stu-id="aedd7-129">Click hello **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="aedd7-130">Kliknij przycisk **Utwórz moje tokenu dostępu**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="aedd7-131">Kliknij przycisk **OAuth testu** w hello prawym górnym rogu strony hello.</span><span class="sxs-lookup"><span data-stu-id="aedd7-131">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>

9. <span data-ttu-id="aedd7-132">Zapisz **konsumenta**, **klucz tajny klienta**, **token dostępu**, i **klucz tajny tokenu dostępu**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="aedd7-133">Pobierz tweetów</span><span class="sxs-lookup"><span data-stu-id="aedd7-133">Download tweets</span></span>

<span data-ttu-id="aedd7-134">Witaj następującego kodu Python pobiera tweetów 10 000 z serwisem Twitter, a następnie zapisz je tooa plik o nazwie **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="aedd7-134">hello following Python code downloads 10,000 tweets from Twitter and save them tooa file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="aedd7-135">Hello następujące kroki są wykonywane w klastrze usługi HDInsight hello, ponieważ Python jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="aedd7-135">hello following steps are performed on hello HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="aedd7-136">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="aedd7-136">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="aedd7-137">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aedd7-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="aedd7-138">Użyj następujących hello polecenia tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)i inne wymagane pakiety:</span><span class="sxs-lookup"><span data-stu-id="aedd7-138">Use hello following commands tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="aedd7-139">Użyj hello następujące polecenie toocreate plik o nazwie **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="aedd7-139">Use hello following command toocreate a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="aedd7-140">Witaj Użyj następującego tekstu jako zawartość hello hello **gettweets.py** pliku:</span><span class="sxs-lookup"><span data-stu-id="aedd7-140">Use hello following text as hello contents of hello **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="aedd7-141">Zastąp tekst zastępczy hello hello poniższych elementach hello informacji z aplikacji twitter:</span><span class="sxs-lookup"><span data-stu-id="aedd7-141">Replace hello placeholder text for hello following items with hello information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="aedd7-142">Użyj **Ctrl + X**, następnie **Y** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="aedd7-142">Use **Ctrl + X**, then **Y** toosave hello file.</span></span>

7. <span data-ttu-id="aedd7-143">Pobierz tweetów i używać hello poniższe polecenie toorun hello plik:</span><span class="sxs-lookup"><span data-stu-id="aedd7-143">Use hello following command toorun hello file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="aedd7-144">Wyświetlany jest wskaźnik postępu.</span><span class="sxs-lookup"><span data-stu-id="aedd7-144">A progress indicator appears.</span></span> <span data-ttu-id="aedd7-145">Liczy % too100 jako powitalne tweetów zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="aedd7-145">It counts up too100% as hello tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aedd7-146">Jeśli trwa zbyt długo tooadvance pasek postępu hello, należy zmienić hello filtru tootrack trendów tematów.</span><span class="sxs-lookup"><span data-stu-id="aedd7-146">If it is taking a long time for hello progress bar tooadvance, you should change hello filter tootrack trending topics.</span></span> <span data-ttu-id="aedd7-147">W przypadku wielu tweetów temat hello w filtrze, możesz szybko uzyskać hello 10000 tweetów potrzebne.</span><span class="sxs-lookup"><span data-stu-id="aedd7-147">When there are many tweets about hello topic in your filter, you can quickly get hello 10000 tweets needed.</span></span>

### <a name="upload-hello-data"></a><span data-ttu-id="aedd7-148">Przekazywanie danych hello</span><span class="sxs-lookup"><span data-stu-id="aedd7-148">Upload hello data</span></span>

<span data-ttu-id="aedd7-149">tooupload hello tooHDInsight pamięci masowej, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="aedd7-149">tooupload hello data tooHDInsight storage, use hello following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="aedd7-150">Te polecenia przechowywanie danych hello w miejscu dostępnym dla wszystkich węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="aedd7-150">These commands store hello data in a location that all nodes in hello cluster can access.</span></span>

## <a name="run-hello-hiveql-job"></a><span data-ttu-id="aedd7-151">Uruchom zadanie HiveQL hello</span><span class="sxs-lookup"><span data-stu-id="aedd7-151">Run hello HiveQL job</span></span>

1. <span data-ttu-id="aedd7-152">Użyj następującego polecenia toocreate plik zawierający instrukcje HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="aedd7-152">Use hello following command toocreate a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="aedd7-153">Użyj następującego tekstu jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="aedd7-153">Use hello following text as hello contents of hello file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="aedd7-154">Naciśnij klawisz **Ctrl + X**, naciśnij klawisz **Y** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="aedd7-154">Press **Ctrl + X**, then press **Y** toosave hello file.</span></span>
3. <span data-ttu-id="aedd7-155">Użyj następującego polecenia toorun powitalne HiveQL zawarte w pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="aedd7-155">Use hello following command toorun hello HiveQL contained in hello file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="aedd7-156">To polecenie uruchamia hello hello **twitter.hql** pliku.</span><span class="sxs-lookup"><span data-stu-id="aedd7-156">This command runs hello hello **twitter.hql** file.</span></span> <span data-ttu-id="aedd7-157">Po wykonaniu kwerendy hello, zostanie wyświetlony `jdbc:hive2//localhost:10001/>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="aedd7-157">Once hello query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="aedd7-158">W wierszu beeline hello Użyj powitania po tooverify zapytania, że dane zostały zaimportowane:</span><span class="sxs-lookup"><span data-stu-id="aedd7-158">From hello beeline prompt, use hello following query tooverify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="aedd7-159">Ta kwerenda zwraca maksymalnie 10 tweetów, zawierające słowo hello **Azure** w tekście wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="aedd7-159">This query returns a maximum of 10 tweets that contain hello word **Azure** in hello message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aedd7-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aedd7-160">Next steps</span></span>

<span data-ttu-id="aedd7-161">Wiesz już, jak tootransform bez struktury zestawu danych JSON w strukturze tabeli programu Hive.</span><span class="sxs-lookup"><span data-stu-id="aedd7-161">You have learned how tootransform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="aedd7-162">toolearn więcej informacji na temat Hive w usłudze HDInsight, zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="aedd7-162">toolearn more about Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="aedd7-163">Rozpoczynanie pracy z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="aedd7-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="aedd7-164">Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="aedd7-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
