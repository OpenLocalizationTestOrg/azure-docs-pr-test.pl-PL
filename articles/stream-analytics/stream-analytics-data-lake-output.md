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
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="e093e-103">Dane wyjściowe Stream Analytics Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e093e-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="e093e-104">Zadania usługi analiza strumienia obsługuje kilka metod danych wyjściowych, co jest [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="e093e-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="e093e-105">Azure Data Lake Store to repozytorium w hiperskali obsługujące całe przedsiębiorstwo na potrzeby obciążeń analizy dużych ilości danych (big data).</span><span class="sxs-lookup"><span data-stu-id="e093e-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="e093e-106">Data Lake Store umożliwia toostore danych dowolnego rozmiar, typ i wprowadzanie szybkość analiz operacyjnych i poznawczych.</span><span class="sxs-lookup"><span data-stu-id="e093e-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="e093e-107">Autoryzuj konto usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e093e-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="e093e-108">Po wybraniu jako dane wyjściowe w hello portalu Azure Data Lake Store pojawi się monit tooauthorize Użyj istniejącej usługi Data Lake Store lub toorequest dostępu toohello Data Lake Store za pomocą hello klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="e093e-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="e093e-109">Jeśli masz już dostępu tooData Lake Store, kliknij przycisk "Autoryzuj" i krótki czas strony będzie wyskakujące wskazujący "Tooauthorization przekierowanie".</span><span class="sxs-lookup"><span data-stu-id="e093e-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="e093e-110">Strona Hello zostanie automatycznie zamknięte i zostanie wyświetlona z hello strony, która umożliwiałaby tooconfigure hello usługi Data Lake Store w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e093e-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="e093e-111">Jeśli użytkownik nie jest zarejestrowany w usłudze Data Lake Store, można wykonać hello "Uaktywnij teraz" łącze tooinitiate hello żądania lub wykonaj hello [uzyskać uruchomiono instrukcje](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e093e-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="e093e-112">Skonfiguruj właściwości danych wyjściowych usługi Data Lake Store hello</span><span class="sxs-lookup"><span data-stu-id="e093e-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="e093e-113">Po utworzeniu konta usługi Data Lake Store hello uwierzytelnionego, można skonfigurować właściwości powitania dla danych wyjściowych usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e093e-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="e093e-114">w poniższej tabeli Hello jest hello listę nazw właściwości i ich tooconfigure opis, który output usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e093e-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="e093e-115"><B>NAZWA WŁAŚCIWOŚCI</B></span><span class="sxs-lookup"><span data-stu-id="e093e-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="e093e-116"><B>OPIS ELEMENTU</B></span><span class="sxs-lookup"><span data-stu-id="e093e-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-117">Alias wyjściowy</span><span class="sxs-lookup"><span data-stu-id="e093e-117">Output Alias</span></span></td>
<td><span data-ttu-id="e093e-118">Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e093e-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-119">Konto usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e093e-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="e093e-120">Nazwa Hello hello konta magazynu, gdzie wysyłania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e093e-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="e093e-121">Zostanie wyświetlona lista kont usługi Data Lake Store, do których hello zalogowany użytkownik ma dostęp do.</span><span class="sxs-lookup"><span data-stu-id="e093e-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-122">Wzorzec prefiksu ścieżki [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="e093e-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="e093e-123">Witaj toowrite użyta ścieżka pliku pliki w obrębie hello określić konta usługi Data Lake magazynu.</span><span class="sxs-lookup"><span data-stu-id="e093e-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="e093e-124">{date} {time}</span><span class="sxs-lookup"><span data-stu-id="e093e-124">{date}, {time}</span></span><BR><span data-ttu-id="e093e-125">Przykład 1: folder1/dzienniki / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="e093e-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="e093e-126">Przykład 2: folder1/dzienniki / {date}</span><span class="sxs-lookup"><span data-stu-id="e093e-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-127">Data w formacie [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="e093e-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="e093e-128">Jeśli token daty hello jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="e093e-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="e093e-129">Przykład: RRRR/MM/dd.</span><span class="sxs-lookup"><span data-stu-id="e093e-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-130">Format czasu [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="e093e-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="e093e-131">Jeśli token czasu hello jest używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="e093e-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="e093e-132">Wartość hello tylko obsługiwane jest obecnie HH.</span><span class="sxs-lookup"><span data-stu-id="e093e-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-133">Format serializacji zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e093e-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="e093e-134">Format serializacji w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e093e-134">Serialization format for output data.</span></span> <span data-ttu-id="e093e-135">JSON, CSV i Avro są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e093e-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="e093e-136">Encoding</span></span></td>
<td><span data-ttu-id="e093e-137">Jeśli formatu CSV lub JSON, należy określić kodowania.</span><span class="sxs-lookup"><span data-stu-id="e093e-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="e093e-138">Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.</span><span class="sxs-lookup"><span data-stu-id="e093e-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-139">Ogranicznik</span><span class="sxs-lookup"><span data-stu-id="e093e-139">Delimiter</span></span></td>
<td><span data-ttu-id="e093e-140">Dotyczy tylko serializacji woluminów CSV.</span><span class="sxs-lookup"><span data-stu-id="e093e-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="e093e-141">Analiza strumienia obsługuje różne ograniczniki dla serializacji danych CSV.</span><span class="sxs-lookup"><span data-stu-id="e093e-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="e093e-142">Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek.</span><span class="sxs-lookup"><span data-stu-id="e093e-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e093e-143">Format</span><span class="sxs-lookup"><span data-stu-id="e093e-143">Format</span></span></td>
<td><span data-ttu-id="e093e-144">Dotyczy tylko serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="e093e-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="e093e-145">Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e093e-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="e093e-146">Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="e093e-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="e093e-147">Odnów autoryzacji usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e093e-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="e093e-148">Obecnie jest to ograniczenie gdy token uwierzytelniania hello musi toobe ręcznie odświeżane co 90 dni, dla wszystkich zadań usługi Data Lake Store w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e093e-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="e093e-149">Należy również toore-uwierzytelniania konta usługi Data Lake Store, jeśli hasło zostało zmienione od czasu utworzenia lub ostatniej uwierzytelniony zadania.</span><span class="sxs-lookup"><span data-stu-id="e093e-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="e093e-150">Objawem tego problemu jest Brak danych wyjściowych zadania i wystąpił błąd w dziennikach operacji hello wskazujący potrzebę ponownej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="e093e-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="e093e-151">tooresolve ten problem, Zatrzymaj uruchomione zadania i przejdź output tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e093e-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="e093e-152">Kliknij łącze "Odnawiania autoryzacji" hello, a przez krótki czas strony będzie wyskakujące wskazujący "Tooauthorization przekierowanie...".</span><span class="sxs-lookup"><span data-stu-id="e093e-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="e093e-153">Strona Hello zostanie automatycznie zamknięte i w razie powodzenia wskaże "Autoryzacji został pomyślnie odnowiony".</span><span class="sxs-lookup"><span data-stu-id="e093e-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="e093e-154">Następnie należy tooclick przycisk Zapisz, u dołu strony hello hello, a przejść przez ponowne uruchomienie zadania z hello utraty danych tooavoid czas ostatniego zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="e093e-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

