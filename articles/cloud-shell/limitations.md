---
title: "aaaAzure ograniczenia chmury powłoki (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Omówienie ograniczenia powłoki chmury Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="200a2-103">Ograniczenia powłoki w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="200a2-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="200a2-104">Powłoka chmury Azure ma hello następujące znane ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="200a2-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="200a2-105">Stan systemu i trwałości</span><span class="sxs-lookup"><span data-stu-id="200a2-105">System state and persistence</span></span>
<span data-ttu-id="200a2-106">Witaj maszynę, która udostępnia sesję powłoki chmury jest tymczasowy i zostanie odtworzony po sesja jest nieaktywny przez 20 minut.</span><span class="sxs-lookup"><span data-stu-id="200a2-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="200a2-107">Chmura powłoki wymaga toobe udziału plików, zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="200a2-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="200a2-108">W związku z tym subskrypcji musi być tooset stanie się tooaccess zasobów magazynu powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="200a2-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="200a2-109">Inne zagadnienia dotyczące obejmują:</span><span class="sxs-lookup"><span data-stu-id="200a2-109">Other considerations include:</span></span>
* <span data-ttu-id="200a2-110">Z magazynem zainstalowanym, tylko zmiany w ramach Twojej `$Home` katalogu lub `clouddrive` katalogu są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="200a2-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="200a2-111">Udziały plików może być instalowany tylko z poziomu programu [przypisane region](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="200a2-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="200a2-112">Usługa pliki Azure obsługuje tylko lokalnie nadmiarowego magazynu i kont magazynu geograficznie nadmiarowego.</span><span class="sxs-lookup"><span data-stu-id="200a2-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="200a2-113">Uprawnienia użytkowników</span><span class="sxs-lookup"><span data-stu-id="200a2-113">User permissions</span></span>
<span data-ttu-id="200a2-114">Uprawnienia zostały ustawione jako normalnych użytkowników bez dostępu do operacji sudo.</span><span class="sxs-lookup"><span data-stu-id="200a2-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="200a2-115">Każda instalacja poza Twojej `$Home` nie zachowa katalogu.</span><span class="sxs-lookup"><span data-stu-id="200a2-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="200a2-116">Mimo że hello niektórych poleceń w `clouddrive` katalogu, takie jak `git clone`, nie ma odpowiednich uprawnień, Twoje `$Home` katalogu uprawnień.</span><span class="sxs-lookup"><span data-stu-id="200a2-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="200a2-117">Obsługa przeglądarek</span><span class="sxs-lookup"><span data-stu-id="200a2-117">Browser support</span></span>
<span data-ttu-id="200a2-118">Powłoka chmura obsługuje hello najnowsze wersje Microsoft Edge, programu Microsoft Internet Explorer, Google Chrome, Mozilla Firefox i Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="200a2-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="200a2-119">Przeglądarka Safari w trybie prywatnym nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="200a2-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="200a2-120">Kopiowanie i wklejanie</span><span class="sxs-lookup"><span data-stu-id="200a2-120">Copy and paste</span></span>
<span data-ttu-id="200a2-121">CTRL + C i Ctrl + V nie działają zgodnie z kopiowania/wklejania skróty w powłoce chmury na komputerach z systemem Windows, użyj klawiszy Ctrl + Insert i Shift + Insert toocopy i Wklej odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="200a2-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="200a2-122">Kliknij prawym przyciskiem myszy kopiowania i wklejania opcje są także dostępne, ale funkcja Kliknij prawym przyciskiem myszy jest dostęp do Schowka specyficzne dla toobrowser podmiotu.</span><span class="sxs-lookup"><span data-stu-id="200a2-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="200a2-123">Edytowanie .bashrc</span><span class="sxs-lookup"><span data-stu-id="200a2-123">Editing .bashrc</span></span>
<span data-ttu-id="200a2-124">Mają ostrożność w przypadku edycji .bashrc w ten sposób może spowodować nieoczekiwane błędy w chmurze powłoki.</span><span class="sxs-lookup"><span data-stu-id="200a2-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="200a2-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="200a2-125">.bash_history</span></span>
<span data-ttu-id="200a2-126">Historię poleceń bash może być niespójna z powodu przerw w działaniu sesję powłoki chmury lub równoczesnych sesji.</span><span class="sxs-lookup"><span data-stu-id="200a2-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="200a2-127">Limity użycia</span><span class="sxs-lookup"><span data-stu-id="200a2-127">Usage limits</span></span>
<span data-ttu-id="200a2-128">Powłoka chmury jest przeznaczony dla przypadków użycia interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="200a2-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="200a2-129">W związku z tym wszystkie długotrwałe nieinterakcyjnym sesje zostaną zakończone bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="200a2-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="200a2-130">Połączenie sieciowe</span><span class="sxs-lookup"><span data-stu-id="200a2-130">Network connectivity</span></span>
<span data-ttu-id="200a2-131">Wszelkie opóźnienia w powłoce chmury jest połączenie z Internetem toolocal podmiotu, powłoki chmury nadal toocarry tooattempt się żadnych instrukcji wysyłane.</span><span class="sxs-lookup"><span data-stu-id="200a2-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="200a2-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="200a2-132">Next steps</span></span>
[<span data-ttu-id="200a2-133">Szybki Start powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="200a2-133">Cloud Shell Quickstart</span></span>](quickstart.md)
