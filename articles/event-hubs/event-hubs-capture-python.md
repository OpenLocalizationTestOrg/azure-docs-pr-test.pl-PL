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
# <a name="event-hubs-capture-walkthrough-python"></a>Wskazówki przechwytywania centra zdarzeń: Python

Przechwytywanie centra zdarzeń to funkcja usługi Event hubs umożliwia tooautomatically należy dostarczyć hello strumieniowego przesyłania danych w sieci tooan Centrum zdarzeń konta magazynu obiektów Blob Azure o wybranym. Ta funkcja umożliwia łatwe tooperform przetwarzanie partii na dane przesyłane strumieniowo w czasie rzeczywistym. W tym artykule opisano sposób toouse usługi Event Hubs przechwytywania języka Python. Aby uzyskać więcej informacji na temat przechwytywania centra zdarzeń, zobacz hello [artykuł z omówieniem](event-hubs-archive-overview.md).

W przykładzie użyto hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) funkcja przechwytywania hello toodemonstrate. Hello sender.py program wysyła symulowane telemetrii środowiska koncentratory tooEvent w formacie JSON. Witaj Centrum zdarzeń jest skonfigurowany hello toouse przechwytywania funkcji toowrite tego magazynu tooblob danych w partiach. aplikacji capturereader.py Hello następnie odczytuje te obiekty BLOB i tworzy plik append na urządzenie, a następnie zapisuje dane hello do plików CSV.

## <a name="what-will-be-accomplished"></a>Co zostanie osiągnięte?

1. Tworzenie konta magazynu obiektów Blob Azure i kontener obiektów blob, to przy użyciu hello portalu Azure.
2. Tworzenie Centrum zdarzeń przestrzeni nazw przy użyciu hello portalu Azure.
3. Tworzenie Centrum zdarzeń z funkcją przechwytywania hello włączone, za pomocą hello portalu Azure.
4. Wysyłanie danych Centrum zdarzeń toohello przy użyciu skryptu języka Python.
5. Odczytywać pliki hello hello przechwytywania i przetwarzanie ich z innego skryptu języka Python.

## <a name="prerequisites"></a>Wymagania wstępne

- Python 2.7.x
- Subskrypcja platformy Azure
- Aktywny [centra zdarzeń w przestrzeni nazw i zdarzenia koncentratora.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage
1. Zaloguj się na toohello [portalu Azure][Azure portal].
2. W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **magazynu**, a następnie kliknij przycisk **konta magazynu**.
3. Wypełnij pola hello w bloku konto magazynu hello, a następnie kliknij przycisk **Utwórz**.
   
   ![][1]
4. Po hello **wdrożeń zakończyło się pomyślnie** komunikatów, kliknij nazwę hello hello nowe konto magazynu, w hello **Essentials** bloku, kliknij przycisk **obiekty BLOB**. Gdy hello **usługa Blob** zostanie otwarty blok, kliknij przycisk **+ kontener** u góry hello. Nazwa kontenera hello **przechwytywania**, następnie zamknij hello **usługa Blob** bloku.
5. Kliknij przycisk **klucze dostępu** w powitania po lewej stronie bloku i skopiuj hello nazwy konta magazynu hello i wartość hello **klucz1**. Zapisz te wartości tooNotepad lub tymczasowej lokalizacji.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Tworzenie Centrum zdarzeń tooyour zdarzenia toosend Python skryptu
1. Otwórz ulubionego edytora języka Python, takie jak [Visual Studio Code][Visual Studio Code].
2. Utwórz skrypt o nazwie **sender.py**. Ten skrypt wysyła 200 Centrum zdarzeń tooyour zdarzenia. Są to proste odczyty środowiska wysyłane w formacie JSON.
3. Wklej powitania po kodu do sender.py:
   
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
4. Zaktualizuj hello poprzedzających toouse kodu swoją nazwę przestrzeni nazw, wartość klucza i nazwy Centrum zdarzeń, które zostały uzyskane podczas tworzenia hello centra zdarzeń w przestrzeni nazw.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Tworzenie plików przechwytywania tooread skryptu języka Python

1. Wypełnianie hello bloku, a następnie kliknij przycisk **Utwórz**.
2. Utwórz skrypt o nazwie **capturereader.py**. Ten skrypt odczytuje hello zebrane pliki i tworzy plik na urządzeniu toowrite hello danych tylko dla tego urządzenia.
3. Wklej powitania po kodu do capturereader.py:
   
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
4. Można się toopaste hello odpowiednie wartości dla nazwy konta magazynu, a klucz w hello wywołanie za`startProcessing`.

## <a name="run-hello-scripts"></a>Uruchom skrypty hello
1. Otwórz wiersz polecenia z języka Python w jego ścieżki, a następnie uruchom te polecenia tooinstall Python wstępnie wymagane pakiety:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Jeśli istnieje wcześniejszej wersji magazynu azure lub usługi azure może być konieczne toouse hello **— uaktualnienie** opcji
   
  Należy również następujące hello toorun (niekonieczne w większości systemów):
   
  ```
  pip install cryptography
  ```
2. Zmień toowherever Twojego katalogu, zapisane sender.py i capturereader.py, a następnie uruchom to polecenie:
   
  ```
  start python sender.py
  ```
   
  To polecenie uruchamia nowy nadawca hello toorun proces języka Python.
3. Teraz Poczekaj kilka minut, aż toorun przechwytywania hello. Następnie wpisz hello następującego polecenia do oryginalnego okna polecenia:
   
   ```
   python capturereader.py
   ```

   Ten procesor przechwytywania używa toodownload katalogu lokalnego hello wszystkie hello obiekty BLOB z kontenera konta magazynu hello. Procesy, które nie są puste i zapisuje wyniki hello jako pliki CSV do katalogu lokalnego hello.

## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event hubs przechwytywania][Overview of Event Hubs Capture]
* Kompletna [przykładowa aplikacja korzystająca z usługi Event Hubs][sample application that uses Event Hubs].
* Witaj [skalowania przetwarzania zdarzeń za pomocą usługi Event Hubs] [ Scale out Event Processing with Event Hubs] próbki.
* [Przegląd usługi Event Hubs][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
