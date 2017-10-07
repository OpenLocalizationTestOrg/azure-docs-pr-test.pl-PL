---
title: "wskazówki przechwytywania centra zdarzeń aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykład, który używa hello Azure Python SDK toodemonstrate za pomocą funkcji przechwytywania centra zdarzeń hello."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="13d49-103">Wskazówki przechwytywania centra zdarzeń: Python</span><span class="sxs-lookup"><span data-stu-id="13d49-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="13d49-104">Przechwytywanie centra zdarzeń to funkcja usługi Event hubs umożliwia tooautomatically należy dostarczyć hello strumieniowego przesyłania danych w sieci tooan Centrum zdarzeń konta magazynu obiektów Blob Azure o wybranym.</span><span class="sxs-lookup"><span data-stu-id="13d49-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="13d49-105">Ta funkcja umożliwia łatwe tooperform przetwarzanie partii na dane przesyłane strumieniowo w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="13d49-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="13d49-106">W tym artykule opisano sposób toouse usługi Event Hubs przechwytywania języka Python.</span><span class="sxs-lookup"><span data-stu-id="13d49-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="13d49-107">Aby uzyskać więcej informacji na temat przechwytywania centra zdarzeń, zobacz hello [artykuł z omówieniem](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13d49-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="13d49-108">W przykładzie użyto hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) funkcja przechwytywania hello toodemonstrate.</span><span class="sxs-lookup"><span data-stu-id="13d49-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="13d49-109">Hello sender.py program wysyła symulowane telemetrii środowiska koncentratory tooEvent w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="13d49-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="13d49-110">Witaj Centrum zdarzeń jest skonfigurowany hello toouse przechwytywania funkcji toowrite tego magazynu tooblob danych w partiach.</span><span class="sxs-lookup"><span data-stu-id="13d49-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="13d49-111">aplikacji capturereader.py Hello następnie odczytuje te obiekty BLOB i tworzy plik append na urządzenie, a następnie zapisuje dane hello do plików CSV.</span><span class="sxs-lookup"><span data-stu-id="13d49-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="13d49-112">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="13d49-112">What will be accomplished</span></span>

1. <span data-ttu-id="13d49-113">Tworzenie konta magazynu obiektów Blob Azure i kontener obiektów blob, to przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13d49-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="13d49-114">Tworzenie Centrum zdarzeń przestrzeni nazw przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13d49-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="13d49-115">Tworzenie Centrum zdarzeń z funkcją przechwytywania hello włączone, za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13d49-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="13d49-116">Wysyłanie danych Centrum zdarzeń toohello przy użyciu skryptu języka Python.</span><span class="sxs-lookup"><span data-stu-id="13d49-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="13d49-117">Odczytywać pliki hello hello przechwytywania i przetwarzanie ich z innego skryptu języka Python.</span><span class="sxs-lookup"><span data-stu-id="13d49-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13d49-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13d49-118">Prerequisites</span></span>

- <span data-ttu-id="13d49-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="13d49-119">Python 2.7.x</span></span>
- <span data-ttu-id="13d49-120">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13d49-120">An Azure subscription</span></span>
- <span data-ttu-id="13d49-121">Aktywny [centra zdarzeń w przestrzeni nazw i zdarzenia koncentratora.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="13d49-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="13d49-122">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="13d49-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="13d49-123">Zaloguj się na toohello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="13d49-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="13d49-124">W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **magazynu**, a następnie kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="13d49-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="13d49-125">Wypełnij pola hello w bloku konto magazynu hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="13d49-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="13d49-126">Po hello **wdrożeń zakończyło się pomyślnie** komunikatów, kliknij nazwę hello hello nowe konto magazynu, w hello **Essentials** bloku, kliknij przycisk **obiekty BLOB**.</span><span class="sxs-lookup"><span data-stu-id="13d49-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="13d49-127">Gdy hello **usługa Blob** zostanie otwarty blok, kliknij przycisk **+ kontener** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="13d49-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="13d49-128">Nazwa kontenera hello **przechwytywania**, następnie zamknij hello **usługa Blob** bloku.</span><span class="sxs-lookup"><span data-stu-id="13d49-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="13d49-129">Kliknij przycisk **klucze dostępu** w powitania po lewej stronie bloku i skopiuj hello nazwy konta magazynu hello i wartość hello **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="13d49-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="13d49-130">Zapisz te wartości tooNotepad lub tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="13d49-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="13d49-131">Tworzenie Centrum zdarzeń tooyour zdarzenia toosend Python skryptu</span><span class="sxs-lookup"><span data-stu-id="13d49-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="13d49-132">Otwórz ulubionego edytora języka Python, takie jak [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="13d49-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="13d49-133">Utwórz skrypt o nazwie **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="13d49-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="13d49-134">Ten skrypt wysyła 200 Centrum zdarzeń tooyour zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="13d49-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="13d49-135">Są to proste odczyty środowiska wysyłane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="13d49-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="13d49-136">Wklej powitania po kodu do sender.py:</span><span class="sxs-lookup"><span data-stu-id="13d49-136">Paste hello following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="13d49-137">Zaktualizuj hello poprzedzających toouse kodu swoją nazwę przestrzeni nazw, wartość klucza i nazwy Centrum zdarzeń, które zostały uzyskane podczas tworzenia hello centra zdarzeń w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="13d49-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="13d49-138">Tworzenie plików przechwytywania tooread skryptu języka Python</span><span class="sxs-lookup"><span data-stu-id="13d49-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="13d49-139">Wypełnianie hello bloku, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="13d49-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="13d49-140">Utwórz skrypt o nazwie **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="13d49-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="13d49-141">Ten skrypt odczytuje hello zebrane pliki i tworzy plik na urządzeniu toowrite hello danych tylko dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="13d49-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="13d49-142">Wklej powitania po kodu do capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="13d49-142">Paste hello following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="13d49-143">Można się toopaste hello odpowiednie wartości dla nazwy konta magazynu, a klucz w hello wywołanie za`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="13d49-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="13d49-144">Uruchom skrypty hello</span><span class="sxs-lookup"><span data-stu-id="13d49-144">Run hello scripts</span></span>
1. <span data-ttu-id="13d49-145">Otwórz wiersz polecenia z języka Python w jego ścieżki, a następnie uruchom te polecenia tooinstall Python wstępnie wymagane pakiety:</span><span class="sxs-lookup"><span data-stu-id="13d49-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="13d49-146">Jeśli istnieje wcześniejszej wersji magazynu azure lub usługi azure może być konieczne toouse hello **— uaktualnienie** opcji</span><span class="sxs-lookup"><span data-stu-id="13d49-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="13d49-147">Należy również następujące hello toorun (niekonieczne w większości systemów):</span><span class="sxs-lookup"><span data-stu-id="13d49-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="13d49-148">Zmień toowherever Twojego katalogu, zapisane sender.py i capturereader.py, a następnie uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="13d49-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="13d49-149">To polecenie uruchamia nowy nadawca hello toorun proces języka Python.</span><span class="sxs-lookup"><span data-stu-id="13d49-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="13d49-150">Teraz Poczekaj kilka minut, aż toorun przechwytywania hello.</span><span class="sxs-lookup"><span data-stu-id="13d49-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="13d49-151">Następnie wpisz hello następującego polecenia do oryginalnego okna polecenia:</span><span class="sxs-lookup"><span data-stu-id="13d49-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="13d49-152">Ten procesor przechwytywania używa toodownload katalogu lokalnego hello wszystkie hello obiekty BLOB z kontenera konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="13d49-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="13d49-153">Procesy, które nie są puste i zapisuje wyniki hello jako pliki CSV do katalogu lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="13d49-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13d49-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13d49-154">Next steps</span></span>

<span data-ttu-id="13d49-155">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="13d49-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="13d49-156">[Omówienie usługi Event hubs przechwytywania][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="13d49-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="13d49-157">Kompletna [przykładowa aplikacja korzystająca z usługi Event Hubs][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="13d49-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="13d49-158">Witaj [skalowania przetwarzania zdarzeń za pomocą usługi Event Hubs] [ Scale out Event Processing with Event Hubs] próbki.</span><span class="sxs-lookup"><span data-stu-id="13d49-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="13d49-159">[Przegląd usługi Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="13d49-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
