---
title: "twins urządzenia Azure IoT Hub aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera - Użyj urządzenia twins toosynchronize stan i dane konfiguracyjne między centrum IoT i urządzeniami"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>W zrozumieniu i użytkowaniu twins urządzenie w Centrum IoT
## <a name="overview"></a>Omówienie
*Urządzenie twins* są dokumentów JSON, w których są przechowywane informacje o stanie urządzenia (metadanych, konfiguracji i warunki). Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia połączyć z tooIoT koncentratora. W tym artykule opisano:

* Witaj struktury Witaj dwie urządzenia: *tagi*, *żądany* i *zgłosił właściwości*, i
* Witaj operacje aplikacji dla urządzeń i zaplecza na twins urządzenia.

> [!NOTE]
> Obecnie dostępny tylko w przypadku urządzeń łączących tooIoT Centrum są twins urządzenia przy użyciu protokołu MQTT hello. Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Gdy toouse
Użyj twins urządzenia do:

* Przechowywania metadanych specyficznych dla urządzeń w chmurze hello. Na przykład hello lokalizacja wdrożenia automaty maszyny.
* Bieżący stan informacji w raporcie, takie jak dostępne możliwości i warunków z aplikacją urządzenia. Na przykład urządzenie jest połączone tooyour Centrum IoT over komórkowej lub Wi-Fi.
* Synchronizuj stan hello przepływów pracy, długotrwałą między aplikacją urządzenia i aplikacji zaplecza. Na przykład podczas kopii rozwiązania hello zakończenia określa hello nowe tooinstall wersji oprogramowania układowego i raporty dotyczące aplikacji urządzeń hello hello różne etapy procesu aktualizacji hello.
* Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.

Odwołuje się zbyt[wskazówki komunikację urządzenia do chmury] [ lnk-d2c-guidance] wskazówki dotyczące przy użyciu właściwości zgłoszone, wiadomości urządzenia do chmury lub przekazywania pliku.
Odwołuje się zbyt[wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] wskazówki na temat używania żądanej właściwości, metody bezpośredniego lub komunikaty chmury do urządzenia.

## <a name="device-twins"></a>Twins urządzenia
Urządzenia twins przechowywać informacje dotyczące urządzeń który:

* Urządzenia i z powrotem kończy się za pomocą warunków urządzenia toosynchronize i konfiguracji.
* za pomocą tooquery zaplecza rozwiązania Hello i docelowa długotrwałej operacji.

cykl życia Witaj dwie urządzenie jest połączone odpowiadającego toohello [tożsamości urządzenia][lnk-identity]. Urządzenie twins niejawnie są tworzone i usuwane po utworzeniu lub usunięciu w Centrum IoT nowej tożsamości urządzenia.

Dwie urządzenia jest dokumentem JSON, który zawiera:

* **Tagi**. Sekcja hello dokumentu JSON, który hello zaplecza rozwiązania można z do odczytu i zapisu. Tagi nie są widoczne toodevice aplikacji.
* **Żądany właściwości**. Używać razem z konfiguracji urządzenia zgłoszonego właściwości toosynchronize lub warunków. Żądane właściwości można ustawić tylko przez rozwiązania hello zakończenia i może zostać odczytany przez hello aplikacji urządzenia. w czasie rzeczywistym zmian właściwości hello potrzeby też być powiadamiani Hello aplikacji urządzenia.
* **Zgłoszone właściwości**. Używać razem z konfiguracji urządzenia toosynchronize odpowiednie właściwości lub warunków. Zgłoszony właściwości można ustawić tylko przez aplikację urządzenia hello i można odczytać i żądanych przez zaplecza rozwiązania hello.

Ponadto hello głównego dokumentu JSON dwie urządzenia hello zawiera właściwości tylko do odczytu z hello odpowiedniego tożsamości urządzenia przechowywany w hello hello [rejestru tożsamości][lnk-identity].

![][img-twin]

Witaj poniższy przykład przedstawia dwie urządzenia dokumentu JSON:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

W obiekcie głównym hello, są hello właściwości systemu i kontener obiektów na `tags` i oba `reported` i `desired` właściwości. Witaj `properties` kontener zawiera niektóre elementy tylko do odczytu (`$metadata`, `$etag`, i `$version`) opisano w hello [metadane dwie urządzenia] [ lnk-twin-metadata] i [ Optymistycznej współbieżności] [ lnk-concurrency] sekcje.

### <a name="reported-property-example"></a>Przykład zgłoszony właściwości
W poprzednim przykładzie hello zawiera dwie urządzenia hello `batteryLevel` właściwości zgłaszane przez hello aplikacji urządzenia. Ta właściwość powoduje tooquery możliwe i działanie na urządzeniach, na podstawie ostatniego poziomu zgłoszone baterii hello. Przykładami innych hello urządzenia aplikacji raportowania możliwości urządzenia lub opcji łączności.

> [!NOTE]
> Właściwości zgłoszone uprościć scenariuszy, w którym zaplecza rozwiązania hello jest zainteresowana hello Ostatnia znana wartość właściwości. Użyj [wiadomości urządzenia do chmury] [ lnk-d2c] czy zaplecza rozwiązania hello wymaga tooprocess telemetrii urządzenia w formie hello sekwencji zdarzeń oznaczony znacznikiem czasowym, takich jak szeregów czasowych.

### <a name="desired-property-example"></a>Przykład żądanej właściwości
W poprzednim przykładzie hello hello `telemetryConfig` potrzebne dwie urządzeń i właściwości zgłoszone są używane przez zaplecza rozwiązania hello i hello urządzenia aplikacji toosynchronize hello telemetrii konfiguracji dla tego urządzenia. Na przykład:

1. zaplecza rozwiązania Hello ustawia hello wymaganą właściwość z wartością konfiguracji hello potrzebne. Poniżej przedstawiono część hello hello dokument z hello żądany zestaw właściwości:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. aplikacji urządzenia Hello jest powiadamiany o zmiany hello natychmiast, jeśli połączenie lub na powitania najpierw Połącz ponownie. Witaj aplikacji urządzenia następnie raporty hello aktualizacji konfiguracji (lub warunek błędu przy użyciu hello `status` właściwości). Oto hello część hello zgłoszonych właściwości:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. zaplecza rozwiązania Hello można śledzić hello wyniki operacji konfiguracji hello na wielu urządzeniach przez [badania] [ lnk-query] twins urządzenia.

> [!NOTE]
> Hello poprzedniego fragmenty kodu są przykłady, zoptymalizowana pod kątem czytelności jednokierunkowej tooencode Konfiguracja urządzenia i jego stan. Witaj dwie urządzenia żądanego i podać właściwości w twins urządzenia hello Centrum IoT nie nakłada określonego schematu.
> 
> 

Możesz użyć twins toosynchronize długotrwałe operacje, takie jak aktualizacje oprogramowania układowego. Aby uzyskać więcej informacji na temat sposobu toosynchronize właściwości toouse i Śledź operacją wymagającą dużo czasu na urządzeniach, zobacz [Użyj potrzeby urządzeń tooconfigure właściwości][lnk-twin-properties].

## <a name="back-end-operations"></a>Operacje zaplecza
zaplecza rozwiązania Hello działa na powitania dwie urządzenia przy użyciu powitania po operacjach niepodzielnych za pośrednictwem protokołu HTTP:

1. **Pobrać dwie urządzenia za pomocą identyfikatora**. Ta operacja zwraca hello urządzenia dwie dokumentu, łącznie z tagami i potrzeby zgłoszone i właściwości systemu.
2. **Częściowego zaktualizowania dwie urządzenia**. Ta operacja umożliwia hello rozwiązania zaplecza toopartially aktualizacji hello znaczników lub odpowiednie właściwości w dwie urządzenia. Witaj częściowej aktualizacji jest wyrażona jako dokument JSON, który dodaje lub aktualizuje dowolną właściwość. Właściwości ustawione zbyt`null` zostaną usunięte. Witaj poniższy przykład tworzy nową właściwość żądaną wartością `{"newProperty": "newValue"}`, zastępuje istniejącą wartość hello z `existingProperty` z `"otherNewValue"`i usuwa `otherOldProperty`. Nie zmian właściwości tooexisting potrzeby lub tagi:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Zastąp odpowiednie właściwości**. Toocompletely umożliwia zaplecza rozwiązania hello tej operacji zastąpić wszystkie istniejące właściwości żądanego i Zastąp nowy dokument JSON dla `properties/desired`.
4. **Zastąp znaczniki**. Toocompletely umożliwia zaplecza rozwiązania hello tej operacji zastąpić wszystkie istniejące znaczniki i Zastąp nowy dokument JSON dla `tags`.
5. **Odbieranie powiadomień dwie**. Ta operacja pozwala toobe zaplecza rozwiązania hello powiadomienie, gdy dwie hello jest modyfikowany. toodo tak, rozwiązania IoT musi toocreate trasy i równości źródła danych hello tooset zbyt*twinChangeEvents*. Domyślnie są wysyłane żadne powiadomienia dwie, oznacza to, że istnieje wstępnie ma takie tras. Jeśli hello szybkość zmian jest zbyt duża lub z innych powodów, takich jak wewnętrzne błędy hello Centrum IoT może wysłać tylko jedno powiadomienie, który zawiera wszystkie zmiany. Tak Jeśli aplikacja wymaga niezawodnej inspekcji i rejestrowania wszystkich stanów pośredniego, następnie nadal zalecane jest używanie D2C wiadomości. Witaj dwie powiadomienie zawiera właściwości, oraz i treść.

    - Właściwości

    | Nazwa | Wartość |
    | --- | --- |
    $content — typ | application/json |
    $iothub-enqueuedtime |  Czas wysłania powiadomienia hello |
    $iothub-komunikat-źródła | twinChangeEvents |
    $content-kodowania | UTF-8 |
    deviceId | Identyfikator urządzenia hello |
    hubName | Nazwa centrum IoT |
    operationTimestamp | [ISO8601] sygnatury czasowej operacji |
    Centrum iothub komunikat schemacie | deviceLifecycleNotification |
    opType | "replaceTwin" lub "updateTwin" |

    Właściwości systemu wiadomości są poprzedzane prefiksem hello `'$'` symbolu.

    - Treść
        
    Ta sekcja zawiera wszystkie Witaj dwie zmiany w formacie JSON. Używa takiego samego formatu hello poprawek, z różnicą hello którą może zawierać wszystkie dwie sekcje: tagi, properties.reported properties.desired i czy zawiera on elementy hello "$metadata". Na przykład:
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

Wszystkie hello poprzedniej operacji obsługi [optymistycznej współbieżności] [ lnk-concurrency] i wymagają hello **ServiceConnect** uprawnienia, zgodnie z definicją w hello [zabezpieczeń ] [ lnk-security] artykułu.

Ponadto operacji toothese, rozwiązanie hello kopii może zakończenia:

* Zapytanie hello twins urządzenia przy użyciu hello przypominającego SQL [język zapytań Centrum IoT][lnk-query].
* Wykonywanie operacji na dużych zestawów twins urządzenia przy użyciu [zadania][lnk-jobs].

## <a name="device-operations"></a>Operacje urządzenia
Witaj urządzenia aplikacji działa na Witaj dwie urządzenia przy użyciu powitania po operacjach niepodzielnych:

1. **Pobrać dwie urządzenia**. Ta operacja zwraca hello urządzenia dwie dokumentu (łącznie tagów i potrzeby, zgłoszone i właściwości systemu) dla hello aktualnie połączonych urządzeń.
2. **Częściowego zaktualizowania właściwości zgłoszone**. Ta operacja umożliwia hello częściowego zaktualizowania hello zgłosił właściwości hello podłączonego urządzenia. To hello używa operacji aktualizacji JSON tego samego formatu tego hello rozwiązania wstecz celu zastosowania częściowej aktualizacji odpowiednie właściwości.
3. **Sprawdź odpowiednie właściwości**. Witaj aktualnie podłączonego urządzenia można wybrać toobe powiadomienie właściwości toohello potrzeby aktualizacje, gdy wystąpią. Witaj urządzenie odbiera hello tego samego formularza aktualizacji (pełnych lub wymiana) wykonywane przez zaplecza rozwiązania hello.

Witaj wszystkich poprzednich operacji wymagają hello **DeviceConnect** uprawnienia, zgodnie z definicją w hello [zabezpieczeń] [ lnk-security] artykułu.

Witaj [urządzenia Azure IoT SDK] [ lnk-sdks] była hello łatwe toouse poprzedzających operacje z wielu języków i platform. Więcej informacji na temat hello szczegóły Centrum IoT w nim elementów podstawowych synchronizacji odpowiednie właściwości można znaleźć w [przepływu ponowne łączenie urządzenia][lnk-reconnection].

> [!NOTE]
> Obecnie dostępny tylko w przypadku urządzeń łączących tooIoT Centrum są twins urządzenia przy użyciu protokołu MQTT hello.
> 
> 

## <a name="reference-topics"></a>Tematy odwołań:
Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat kontrolowania dostępu tooyour IoT hub.

## <a name="tags-and-properties-format"></a>Format znaczników i właściwości
Tagi, żądane i podać właściwości są obiektów JSON z hello następujące ograniczenia:

* Wszystkie klucze w obiektów JSON jest rozróżniana wielkość liter 64 bajtów ciągów UNICODE UTF-8. Dozwolone znaki kontrolne UNICODE (segmenty C0 i C1), Wyklucz znaków i `'.'`, `' '`, i `'$'`.
* Wszystkie wartości w formacie JSON obiekty mogą być hello następujące typy JSON: wartość logiczna, liczba, ciąg, obiekt. Tablice nie są dozwolone.
* Wszystkie obiekty JSON w tagach, żądane i podać właściwości mogą mieć maksymalną głębokość 5. Na przykład po obiektu hello jest prawidłowy:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Wszystkie wartości ciągu może mieć maksymalnie 512 bajtów długości.

## <a name="device-twin-size"></a>Rozmiar dwie urządzenia
Centrum IoT wymusza ograniczenie rozmiaru 8KB na wartościach hello `tags`, `properties/desired`, i `properties/reported`, z wyjątkiem elementów tylko do odczytu.
Hello rozmiar jest obliczany poprzez zliczanie sterowania wszystkie znaki oprócz UNICODE znaków (segmenty C0 i C1) i miejsca `' '` po wyświetleniu poza stałą typu string.
Centrum IoT z powodu błędu odrzuca wszystkie operacje, które spowoduje zwiększenie rozmiaru hello tych dokumentów przekracza hello limit.

## <a name="device-twin-metadata"></a>Metadane dwie urządzenia
Centrum IoT przechowuje hello sygnatura czasowa hello ostatniej aktualizacji dla każdego obiektu JSON w dwie urządzenia żądanego i podać właściwości. sygnatury czasowe Hello są w UTC i kodowany w hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Na przykład:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Ta informacja jest przechowywana w każdej poziomu aktualizacji toopreserve (nie tylko hello liśćmi hello strukturze JSON), które usunąć klucze obiektu.

## <a name="optimistic-concurrency"></a>Optymistycznej współbieżności
Tagi, potrzeby i podać właściwości wszystkich optymistycznej współbieżności pomocy technicznej.
Tagi przypada tag ETag jako [RFC7232], reprezentujący reprezentacja JSON hello tagu. Elementy etag można użyć w operacjach aktualizowania warunkowego z hello rozwiązania zaplecza tooensure spójności.

Dwie urządzenia żądanego i podać właściwości nie ma elementy etag, ale `$version` wartość, która jest gwarantowana toobe przyrostowe. Podobnie tooan ETag, wersja hello mogą być używane przez hello aktualizowanie spójności tooenforce strona aktualizacji. Na przykład aplikacji urządzenia dla zgłoszonego właściwości lub hello zaplecza rozwiązania dla żądanej właściwości.

Wersje są także przydatne, gdy observing agenta (np. aplikacji urządzenia hello obserwowania właściwości hello żądanego) należy uzgodnić szczepy między hello wynik operacji pobierania i powiadomienie o aktualizacji. Witaj sekcji [przepływu ponowne łączenie urządzenia] [ lnk-reconnection] zawiera więcej informacji.

## <a name="device-reconnection-flow"></a>Przepływ ponowne nawiązanie połączenia urządzenia
Centrum IoT nie zachowa powiadomienia o aktualizacji odpowiednie właściwości dla urządzeń bez połączenia. Wynika, że urządzenia, które nawiązuje połączenie musi pobrać hello pełne odpowiednie właściwości dokument w toosubscribing dodanie powiadomień aktualizacji. Biorąc pod uwagę możliwość hello szczepy między powiadomienia o aktualizacji i pobieranie pełnej, należy zapewnić hello następującego przepływu:

1. Aplikacji urządzenia łączy tooan Centrum IoT.
2. Subskrybuje aplikacji urządzenia dla żądanej właściwości powiadomienia o aktualizacji.
3. Aplikacji urządzenia pobiera hello pełnego dokumentu dla żądanej właściwości.

zignorować wszystkie powiadomienia z aplikacji urządzenia Hello `$version` mniejsza lub równa niż wersja hello hello pełnego dokumentu pobrane. Takie podejście jest możliwa, ponieważ gwarantuje Centrum IoT wersje zawsze zwiększyć.

> [!NOTE]
> Istotą takiej logiki jest już zaimplementowany w hello [urządzenia Azure IoT SDK][lnk-sdks]. Ten opis jest przydatny tylko wtedy, gdy hello aplikacji urządzenia nie można użyć dowolnego urządzenia Azure IoT zestawy SDK i musi program hello MQTT interfejsu bezpośrednio.
> 
> 

## <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały
Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* Witaj [punkty końcowe Centrum IoT] [ lnk-endpoints] hello opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* Witaj [ograniczenia przepustowości i przydziały] [ lnk-quotas] przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello artykule.
* Witaj [zestawów SDK urządzeń i usług Azure IoT] [ lnk-sdks] list artykułu hello różnych SDK języka można używać podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* Witaj [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ lnk-query] artykule hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT .
* Witaj [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] artykuł zawiera więcej informacji na temat Centrum IoT obsługę protokołu MQTT hello.

## <a name="next-steps"></a>Następne kroki
Teraz wiesz już, o twins urządzenia, mogą być zainteresowane hello następujące tematy przewodnik dewelopera Centrum IoT:

* [Wywoływanie metody bezpośrednio na urządzeniu][lnk-methods]
* [Planowanie zadań na wielu urządzeniach][lnk-jobs]

Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello następujące samouczki Centrum IoT:

* [Jak toouse Witaj dwie urządzenia][lnk-twin-tutorial]
* [Jak urządzenia toouse dwie właściwości][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
