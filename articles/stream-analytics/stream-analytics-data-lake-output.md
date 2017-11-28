---
title: "Dane wyjściowe usługi Stream Analytics Data Lake Store | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="66e1d-103">Dane wyjściowe Stream Analytics Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="66e1d-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="66e1d-104">Zadania usługi analiza strumienia obsługuje kilka metod danych wyjściowych, co jest [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="66e1d-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="66e1d-105">Azure Data Lake Store to repozytorium w hiperskali obsługujące całe przedsiębiorstwo na potrzeby obciążeń analizy dużych ilości danych (big data).</span><span class="sxs-lookup"><span data-stu-id="66e1d-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="66e1d-106">Data Lake Store można przechowywać dane dowolnego rozmiar, typ i wprowadzanie szybkość analiz operacyjnych i poznawczych.</span><span class="sxs-lookup"><span data-stu-id="66e1d-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="66e1d-107">Autoryzuj konto usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="66e1d-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="66e1d-108">Po wybraniu jako dane wyjściowe w portalu Azure Data Lake Store pojawi się monit dopuszczają użycie usługi istniejących Data Lake Store lub zażądać dostępu do usługi Data Lake Store w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="66e1d-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="66e1d-109">Jeśli masz już dostępu do usługi Data Lake Store, kliknij przycisk "Autoryzuj" i krótki czas strony będzie wyskakujące wskazujący "Przekierowanie do autoryzacji".</span><span class="sxs-lookup"><span data-stu-id="66e1d-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="66e1d-110">Strona zostanie automatycznie zamknięte i zostanie wyświetlone na stronie, która pozwala na skonfigurowanie danych wyjściowych usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="66e1d-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="66e1d-111">Jeśli użytkownik nie jest zarejestrowany w usłudze Data Lake Store, można wykonać "Uaktywnij teraz" łącze do zainicjowania żądania lub wykonaj [uzyskać uruchomiono instrukcje](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="66e1d-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="66e1d-112">Skonfiguruj właściwości danych wyjściowych usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="66e1d-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="66e1d-113">Po utworzeniu konta usługi Data Lake Store uwierzytelnionego, można skonfigurować właściwości dla danych wyjściowych usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="66e1d-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="66e1d-114">W poniższej tabeli jest listą nazw właściwości i ich opis, aby skonfigurować dane wyjściowe usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="66e1d-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="66e1d-115"><B>NAZWA WŁAŚCIWOŚCI</B></span><span class="sxs-lookup"><span data-stu-id="66e1d-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="66e1d-116"><B>OPIS ELEMENTU</B></span><span class="sxs-lookup"><span data-stu-id="66e1d-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-117">Alias wyjściowy</span><span class="sxs-lookup"><span data-stu-id="66e1d-117">Output Alias</span></span></td>
<td><span data-ttu-id="66e1d-118">Jest to przyjazna nazwa używana w zapytaniach do kierowania wyników zapytania do tej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="66e1d-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-119">Konto usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="66e1d-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="66e1d-120">Nazwa konta magazynu, w którym wysyłania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="66e1d-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="66e1d-121">Zostanie wyświetlona lista kont usługi Data Lake Store, do których zalogowany użytkownik ma dostęp do.</span><span class="sxs-lookup"><span data-stu-id="66e1d-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-122">Wzorzec prefiksu ścieżki [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="66e1d-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="66e1d-123">Ścieżka do pliku używany do zapisywania plików w ramach określonego konta magazynu usługi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="66e1d-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="66e1d-124">{date} {time}</span><span class="sxs-lookup"><span data-stu-id="66e1d-124">{date}, {time}</span></span><BR><span data-ttu-id="66e1d-125">Przykład 1: folder1/dzienniki / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="66e1d-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="66e1d-126">Przykład 2: folder1/dzienniki / {date}</span><span class="sxs-lookup"><span data-stu-id="66e1d-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-127">Data w formacie [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="66e1d-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="66e1d-128">Jeśli token daty jest używany w ścieżce prefiks, można wybrać format daty, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="66e1d-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="66e1d-129">Przykład: RRRR/MM/dd.</span><span class="sxs-lookup"><span data-stu-id="66e1d-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-130">Format czasu [<I>opcjonalne</I>]</span><span class="sxs-lookup"><span data-stu-id="66e1d-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="66e1d-131">Jeśli czas nie jest używany w ścieżce prefiks, określ format czasu, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="66e1d-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="66e1d-132">Obecnie jedyna obsługiwana wartość to HH.</span><span class="sxs-lookup"><span data-stu-id="66e1d-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-133">Format serializacji zdarzeń</span><span class="sxs-lookup"><span data-stu-id="66e1d-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="66e1d-134">Format serializacji w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="66e1d-134">Serialization format for output data.</span></span> <span data-ttu-id="66e1d-135">JSON, CSV i Avro są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="66e1d-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="66e1d-136">Encoding</span></span></td>
<td><span data-ttu-id="66e1d-137">Jeśli formatu CSV lub JSON, należy określić kodowania.</span><span class="sxs-lookup"><span data-stu-id="66e1d-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="66e1d-138">UTF-8 to jedyny obsługiwany obecnie format kodowania.</span><span class="sxs-lookup"><span data-stu-id="66e1d-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-139">Ogranicznik</span><span class="sxs-lookup"><span data-stu-id="66e1d-139">Delimiter</span></span></td>
<td><span data-ttu-id="66e1d-140">Dotyczy tylko serializacji woluminów CSV.</span><span class="sxs-lookup"><span data-stu-id="66e1d-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="66e1d-141">Analiza strumienia obsługuje różne ograniczniki dla serializacji danych CSV.</span><span class="sxs-lookup"><span data-stu-id="66e1d-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="66e1d-142">Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek.</span><span class="sxs-lookup"><span data-stu-id="66e1d-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="66e1d-143">Format</span><span class="sxs-lookup"><span data-stu-id="66e1d-143">Format</span></span></td>
<td><span data-ttu-id="66e1d-144">Dotyczy tylko serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="66e1d-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="66e1d-145">Rozdzielone Określa, czy dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="66e1d-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="66e1d-146">Tablica Określa, czy dane wyjściowe będą formatowane jako tablica obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="66e1d-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="66e1d-147">Odnów autoryzacji usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="66e1d-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="66e1d-148">Obecnie jest to ograniczenie gdzie token uwierzytelniania musi być ręcznie odświeżyć co 90 dni, dla wszystkich zadań usługi Data Lake Store w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="66e1d-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="66e1d-149">Należy również ponownego uwierzytelnienia konta usługi Data Lake Store, jeśli hasło zostało zmienione od czasu utworzenia lub ostatniej uwierzytelniony zadania.</span><span class="sxs-lookup"><span data-stu-id="66e1d-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="66e1d-150">Objawem tego problemu jest Brak danych wyjściowych zadania i wystąpił błąd w dziennikach operacji wskazujący potrzebę ponownej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="66e1d-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="66e1d-151">Aby rozwiązać ten problem, Zatrzymaj uruchomione zadania i przejdź do usługi Data Lake Store dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="66e1d-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="66e1d-152">Kliknij łącze "Odnowić autoryzacji", a przez krótki czas strony będzie wyskakujące wskazujący "Przekierowanie do autoryzacji...".</span><span class="sxs-lookup"><span data-stu-id="66e1d-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="66e1d-153">Strona zostanie automatycznie zamknięte i w razie powodzenia wskaże "Autoryzacji został pomyślnie odnowiony".</span><span class="sxs-lookup"><span data-stu-id="66e1d-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="66e1d-154">Można następnie trzeba w dolnej części strony, kliknij przycisk "Zapisz" i przejść przez ponowne uruchomienie zadania od ostatniego czasu zatrzymana w celu uniknięcia utraty danych.</span><span class="sxs-lookup"><span data-stu-id="66e1d-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

