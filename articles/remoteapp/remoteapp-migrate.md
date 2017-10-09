---
title: "aaaMigrate danych użytkownika z usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate danych użytkownika i usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="f23cf-103">Jak toomigrate danych do i z usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f23cf-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f23cf-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f23cf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f23cf-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f23cf-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f23cf-106">Można używać wielu różnych narzędzi i metod tootransfer [dane użytkownika](remoteapp-upd.md) do i z usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f23cf-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="f23cf-107">Oto kilka metod:</span><span class="sxs-lookup"><span data-stu-id="f23cf-107">Here are a few methods:</span></span>

* <span data-ttu-id="f23cf-108">Skopiuj i Wklej korzystania z funkcji udostępniania schowka</span><span class="sxs-lookup"><span data-stu-id="f23cf-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="f23cf-109">Skopiuj pliki i dane serwera plików tooa</span><span class="sxs-lookup"><span data-stu-id="f23cf-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="f23cf-110">Skopiuj pliki tooOneDrive dla firm przy użyciu przeglądarki</span><span class="sxs-lookup"><span data-stu-id="f23cf-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="f23cf-111">Skopiować pliki przy użyciu przekierowania</span><span class="sxs-lookup"><span data-stu-id="f23cf-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="f23cf-112">Nie można włączyć hello usługi OneDrive dla firm i konsumentów agentów synchronizacji — one [nie są obsługiwane](remoteapp-onedrive.md) w usłudze Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f23cf-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="f23cf-113">Użyj kopiowania i wklejania w Eksploratorze plików</span><span class="sxs-lookup"><span data-stu-id="f23cf-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="f23cf-114">Kopiowanie i wklejanie przy użyciu Schowka hello jest włączone w przypadku wdrożeń usługi RemoteApp [domyślnie](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="f23cf-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="f23cf-115">Umożliwia to użytkownikom kopiowania plików między ich lokalnego komputera i programów RemoteApp aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f23cf-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="f23cf-116">Często za pośrednictwem hello trakcie normalnego przebiegu za pomocą aplikacji w usłudze RemoteApp, użytkownicy mają zapisane pliki UPD tootheir — przenoszenie, że dane z usługi RemoteApp jest prosty:</span><span class="sxs-lookup"><span data-stu-id="f23cf-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="f23cf-117">[Publikowanie Eksploratora plików jako aplikacja](remoteapp-publish.md) w kolekcji usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f23cf-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="f23cf-118">(Należy pamiętać, że jest to zadanie administracyjne).</span><span class="sxs-lookup"><span data-stu-id="f23cf-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="f23cf-119">Bezpośrednie użytkowników toolaunch hello Eksploratora plików aplikacji, która została opublikowana i toouse tego toocopy i Wklej pliki zarówno do ich UPD i od niego.</span><span class="sxs-lookup"><span data-stu-id="f23cf-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="f23cf-120">Przekazywanie plików i serwer plików tooa danych za pomocą kopiowania plików na standardowe sieci</span><span class="sxs-lookup"><span data-stu-id="f23cf-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="f23cf-121">Organizacje często używają danych toostore ogólnych serwerów plików.</span><span class="sxs-lookup"><span data-stu-id="f23cf-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="f23cf-122">Jeśli znasz nazwę serwera hello lub lokalizacji, użytkowników można Przeglądaj hello sieci lokalne powitania serwera, a następnie skopiuj pliki, znacznie, tak jak powyżej.</span><span class="sxs-lookup"><span data-stu-id="f23cf-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="f23cf-123">Będzie ponownie mają toopublish tooRemoteApp Eksplorator plików i udostępnij go użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="f23cf-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="f23cf-124">powitania serwera plików musi być hello routingu sieci, która programów RemoteApp został wdrożony do.</span><span class="sxs-lookup"><span data-stu-id="f23cf-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="f23cf-125">Skopiuj pliki tooOneDrive dla firm</span><span class="sxs-lookup"><span data-stu-id="f23cf-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="f23cf-126">Mimo że nie można włączyć hello usługi OneDrive dla firm agenta synchronizacji w usłudze RemoteApp, możesz nadal skopiować pliki z tooOneDrive Twojego UPD dla firm za pośrednictwem przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f23cf-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="f23cf-127">Publikowanie tooRemoteApp Eksploratora plików, a następnie się, że użytkownicy tooaccess hello plików za pomocą tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f23cf-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="f23cf-128">Jest najprostszym pliki tootransfer ich kompresji, użytkowników, należy utworzyć plik zip, który zawiera wszystkie tooOneDrive toomove pliki hello dla firm.</span><span class="sxs-lookup"><span data-stu-id="f23cf-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="f23cf-129">Poproś użytkowników portalu usługi Office 365 toohello toogo i przejdź tooOneDrive i przekaż plik zip hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="f23cf-130">Skopiuj pliki za pomocą przekierowania dysku</span><span class="sxs-lookup"><span data-stu-id="f23cf-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="f23cf-131">Jeśli włączono [przekierowanie dysku](remoteapp-redirection.md), mapowany dysk zostały już utworzone dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f23cf-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="f23cf-132">W takim przypadku można skompresować swoich plików na dysku hello przekierowanie i zapisywać je po tootheir komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f23cf-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="f23cf-133">Jak Administratorzy mogą eksportować dane</span><span class="sxs-lookup"><span data-stu-id="f23cf-133">How administrators can export data</span></span>

<span data-ttu-id="f23cf-134">Zarządza dla usługi Azure RemoteApp można wyeksportować wszystkie dyski profilu użytkownika (UPD) dla wszystkich kolekcji w subskrypcji tooAzure magazynu przy użyciu programu Azure PowerShell polecenia cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="f23cf-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="f23cf-135">Nie możliwości tooselect poszczególnych UPD firmy nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f23cf-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="f23cf-136">Po wykonaniu polecenia programu PowerShell hello każdego dysku użytkownika zostanie 50gb dysku o stałym rozmiarze rozmiar i być wyeksportowane tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="f23cf-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="f23cf-137">Koszty magazynu Azure będą naliczane natychmiast dla tego magazynu.</span><span class="sxs-lookup"><span data-stu-id="f23cf-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="f23cf-138">Jeżeli upewnij się, wykonanie tego polecenia nie ma żadnych sesji, które w przeciwnym razie eksportu hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f23cf-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="f23cf-139">UPD dla wdrożenia usługi Azure RemoteApp przyłączony do domeny mogą być używane tylko ponownie we wdrożeniu usług pulpitu zdalnego, nie można użyć wdrożenia przyłączone do domeny z systemem innym niż.</span><span class="sxs-lookup"><span data-stu-id="f23cf-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="f23cf-140">W przypadku użycia tych dysków we wdrożeniu usług pulpitu zdalnego, firma Microsoft zaleca toouse naszych [automatycznego skrypty](https://github.com/arcadiahlyy/aramigration) który będzie wyeksportować, konwertowanie oraz importowanie hello w UPD do wdrożenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f23cf-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

