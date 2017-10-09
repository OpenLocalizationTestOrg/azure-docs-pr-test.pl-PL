---
title: "aaaStream Analytics Data Lake magazynu w danych wyjściowych | Dokumentacja firmy Microsoft"
description: "Konfiguracja uwierzytelniania i autoryzacji usługi Azure Data Lake Store w zadaniu Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Dane wyjściowe Stream Analytics Data Lake Store
Zadania usługi analiza strumienia obsługuje kilka metod danych wyjściowych, co jest [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Azure Data Lake Store to repozytorium w hiperskali obsługujące całe przedsiębiorstwo na potrzeby obciążeń analizy dużych ilości danych (big data). Data Lake Store umożliwia toostore danych dowolnego rozmiar, typ i wprowadzanie szybkość analiz operacyjnych i poznawczych.

## <a name="authorize-a-data-lake-store-account"></a>Autoryzuj konto usługi Data Lake Store
1. Po wybraniu jako dane wyjściowe w hello portalu Azure Data Lake Store pojawi się monit tooauthorize Użyj istniejącej usługi Data Lake Store lub toorequest dostępu toohello Data Lake Store za pomocą hello klasycznego portalu.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Jeśli masz już dostępu tooData Lake Store, kliknij przycisk "Autoryzuj" i krótki czas strony będzie wyskakujące wskazujący "Tooauthorization przekierowanie". Strona Hello zostanie automatycznie zamknięte i zostanie wyświetlona z hello strony, która umożliwiałaby tooconfigure hello usługi Data Lake Store w danych wyjściowych.

Jeśli użytkownik nie jest zarejestrowany w usłudze Data Lake Store, można wykonać hello "Uaktywnij teraz" łącze tooinitiate hello żądania lub wykonaj hello [uzyskać uruchomiono instrukcje](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Skonfiguruj właściwości danych wyjściowych usługi Data Lake Store hello
Po utworzeniu konta usługi Data Lake Store hello uwierzytelnionego, można skonfigurować właściwości powitania dla danych wyjściowych usługi Data Lake Store. w poniższej tabeli Hello jest hello listę nazw właściwości i ich tooconfigure opis, który output usługi Data Lake Store.

<table>
<tbody>
<tr>
<td><B>NAZWA WŁAŚCIWOŚCI</B></td>
<td><B>OPIS ELEMENTU</B></td>
</tr>
<tr>
<td>Alias wyjściowy</td>
<td>Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis usługi Data Lake Store.</td>
</tr>
<tr>
<td>Konto usługi Data Lake Store</td>
<td>Nazwa Hello hello konta magazynu, gdzie wysyłania danych wyjściowych. Zostanie wyświetlona lista kont usługi Data Lake Store, do których hello zalogowany użytkownik ma dostęp do.</td>
</tr>
<tr>
<td>Wzorzec prefiksu ścieżki [<I>opcjonalne</I>]</td>
<td>Witaj toowrite użyta ścieżka pliku pliki w obrębie hello określić konta usługi Data Lake magazynu. <BR>{date} {time}<BR>Przykład 1: folder1/dzienniki / {date} / {time}<BR>Przykład 2: folder1/dzienniki / {date}</td>
</tr>
<tr>
<td>Data w formacie [<I>opcjonalne</I>]</td>
<td>Jeśli token daty hello jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane. Przykład: RRRR/MM/dd.</td>
</tr>
<tr>
<td>Format czasu [<I>opcjonalne</I>]</td>
<td>Jeśli token czasu hello jest używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane. Wartość hello tylko obsługiwane jest obecnie HH.</td>
</tr>
<tr>
<td>Format serializacji zdarzeń</td>
<td>Format serializacji w danych wyjściowych. JSON, CSV i Avro są obsługiwane.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Jeśli formatu CSV lub JSON, należy określić kodowania. Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.</td>
</tr>
<tr>
<td>Ogranicznik</td>
<td>Dotyczy tylko serializacji woluminów CSV. Analiza strumienia obsługuje różne ograniczniki dla serializacji danych CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek.</td>
</tr>
<tr>
<td>Format</td>
<td>Dotyczy tylko serializacji JSON. Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza. Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Odnów autoryzacji usługi Data Lake Store
Obecnie jest to ograniczenie gdy token uwierzytelniania hello musi toobe ręcznie odświeżane co 90 dni, dla wszystkich zadań usługi Data Lake Store w danych wyjściowych. Należy również toore-uwierzytelniania konta usługi Data Lake Store, jeśli hasło zostało zmienione od czasu utworzenia lub ostatniej uwierzytelniony zadania. Objawem tego problemu jest Brak danych wyjściowych zadania i wystąpił błąd w dziennikach operacji hello wskazujący potrzebę ponownej autoryzacji.

tooresolve ten problem, Zatrzymaj uruchomione zadania i przejdź output tooyour Data Lake Store. Kliknij łącze "Odnawiania autoryzacji" hello, a przez krótki czas strony będzie wyskakujące wskazujący "Tooauthorization przekierowanie...". Strona Hello zostanie automatycznie zamknięte i w razie powodzenia wskaże "Autoryzacji został pomyślnie odnowiony". Następnie należy tooclick przycisk Zapisz, u dołu strony hello hello, a przejść przez ponowne uruchomienie zadania z hello utraty danych tooavoid czas ostatniego zatrzymania.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

