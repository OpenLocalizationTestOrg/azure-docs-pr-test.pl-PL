---
title: "Omówienie powłoki chmury (wersja zapoznawcza) aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd hello powłoki chmury Azure."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="94e76-103">Omówienie powłoki chmury Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="94e76-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="94e76-104">Powłoki chmury Azure jest interaktywny, dostępny w przeglądarce powłoki zarządzania zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94e76-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="94e76-105">Funkcje</span><span class="sxs-lookup"><span data-stu-id="94e76-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="94e76-106">Środowisko powłoki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="94e76-106">Browser-based shell experience</span></span>
<span data-ttu-id="94e76-107">Chmury powłoki umożliwia dostęp tooa wiersza polecenia w przeglądarce skompilowanej za pomocą zadań zarządzania platformy Azure na uwadze.</span><span class="sxs-lookup"><span data-stu-id="94e76-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="94e76-108">Korzystaj z powłoki chmury toowork autonomiczne z komputera lokalnego w sposób, który można podać tylko hello chmury.</span><span class="sxs-lookup"><span data-stu-id="94e76-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="94e76-109">Wstępnie skonfigurowane Azure stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="94e76-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="94e76-110">Powłoki chmury jest wstępnie zainstalowane z popularnych narzędzi wiersza polecenia i język obsługuje, dzięki czemu można pracować szybciej.</span><span class="sxs-lookup"><span data-stu-id="94e76-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="94e76-111">Wyświetl hello narzędzi pełną listę dla powłoki chmury Azure tutaj.</span><span class="sxs-lookup"><span data-stu-id="94e76-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="94e76-112">Automatyczne uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="94e76-112">Automatic authentication</span></span>
<span data-ttu-id="94e76-113">W każdej sesji dla zasobów tooyour natychmiastowy dostęp za pośrednictwem hello Azure CLI 2.0 powłoki chmury bezpiecznie uwierzytelnia automatycznie.</span><span class="sxs-lookup"><span data-stu-id="94e76-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="94e76-114">Łączenie z magazynem plików Azure</span><span class="sxs-lookup"><span data-stu-id="94e76-114">Connect your Azure File storage</span></span>
<span data-ttu-id="94e76-115">Maszyny powłoki chmury są tymczasowe i w związku z tym wymagają toobe udziału plików na platformę Azure zainstalowany jako `clouddrive` toopersist $Home katalogu.</span><span class="sxs-lookup"><span data-stu-id="94e76-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="94e76-116">Przy pierwszym uruchomieniu chmury powłoka wyświetli monit toocreate, które grupy zasobów, konta magazynu i udziału plików w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="94e76-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="94e76-117">To jest jednorazowe kroku i być automatycznie dołączane do wszystkich sesji.</span><span class="sxs-lookup"><span data-stu-id="94e76-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="94e76-118">Tworzenie nowego magazynu</span><span class="sxs-lookup"><span data-stu-id="94e76-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="94e76-119">Konto magazyn lokalnie nadmiarowy (LRS) można utworzyć w Twoim imieniu z udziału plików na platformę Azure zawierającego domyślny obraz dysku 5 GB.</span><span class="sxs-lookup"><span data-stu-id="94e76-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="94e76-120">Instaluje Hello udziału plików jako `clouddrive` dla pliku udziału interakcji z obrazu dysku hello są używane toosync i utrwala $Home katalogu.</span><span class="sxs-lookup"><span data-stu-id="94e76-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="94e76-121">Koszty przechowywania regularne mają zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="94e76-121">Regular storage costs apply.</span></span>

<span data-ttu-id="94e76-122">Trzy zasoby zostaną utworzone w Twoim imieniu:</span><span class="sxs-lookup"><span data-stu-id="94e76-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="94e76-123">Grupa zasobów o nazwie:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="94e76-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="94e76-124">Konto magazynu o nazwie:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="94e76-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="94e76-125">Udział plików o nazwie:`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="94e76-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="94e76-126">Wszystkie pliki w katalogu $Home, takie jak klucze SSH są trwale przechowywane w udziale zainstalowanego pliku obrazu dysku użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94e76-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="94e76-127">Zastosowanie najlepszych rozwiązań podczas zapisywania plików w katalogu $Home i udziału zainstalowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="94e76-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="94e76-128">Korzystać z istniejących zasobów</span><span class="sxs-lookup"><span data-stu-id="94e76-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="94e76-129">Zaawansowana opcja dostępne są również zezwolenie na obecność możesz tooassociate istniejących zasobów tooCloud powłoki.</span><span class="sxs-lookup"><span data-stu-id="94e76-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="94e76-130">Po prezentowany hello magazynu Instalatora wiersza, kliknij przycisk "Pokaż zaawansowane ustawienia" tooselect dodatkowe opcje.</span><span class="sxs-lookup"><span data-stu-id="94e76-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="94e76-131">Listę rozwijaną są filtrowane przypisany region powłoki w chmurze i kont/globalnie — magazyn lokalnie nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="94e76-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="94e76-132">[Więcej informacji na temat magazynu powłoki chmury aktualizowanie udziałów plików i przekazywanie pobierania plików.] (utrwalanie shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="94e76-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="94e76-133">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="94e76-133">Concepts</span></span>
* <span data-ttu-id="94e76-134">Powłoka działa na tymczasowej maszyny na sesji, poszczególnych użytkowników w chmurze</span><span class="sxs-lookup"><span data-stu-id="94e76-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="94e76-135">Chmura powłoki upłynie limit czasu po upływie 20 minut bez interaktywnego działania</span><span class="sxs-lookup"><span data-stu-id="94e76-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="94e76-136">Powłoka chmury można uzyskać tylko z udziałem plików dołączone</span><span class="sxs-lookup"><span data-stu-id="94e76-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="94e76-137">Chmura powłoki przypisano na jednym komputerze na konto użytkownika</span><span class="sxs-lookup"><span data-stu-id="94e76-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="94e76-138">Uprawnienia zostały ustawione jako zwykłych użytkowników systemu Linux</span><span class="sxs-lookup"><span data-stu-id="94e76-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="94e76-139">Dowiedz się więcej o wszystkich funkcji powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="94e76-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="94e76-140">Przykłady</span><span class="sxs-lookup"><span data-stu-id="94e76-140">Examples</span></span>
* <span data-ttu-id="94e76-141">Utwórz lub Edytuj tooautomate skryptów zarządzania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="94e76-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="94e76-142">Jednoczesne zarządzanie zasobami za pośrednictwem portalu Azure i 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="94e76-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="94e76-143">Test-Drive Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94e76-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="94e76-144">Wypróbuj te przykłady na powitania powłoki chmury — Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="94e76-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="94e76-145">Cennik</span><span class="sxs-lookup"><span data-stu-id="94e76-145">Pricing</span></span>
<span data-ttu-id="94e76-146">Hello komputerem obsługującym powłoki chmury jest wolne, wymaga wstępnie posiadania zainstalowanego pliku Azure udział toopersist $Home katalogu.</span><span class="sxs-lookup"><span data-stu-id="94e76-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="94e76-147">Koszty przechowywania regularne mają zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="94e76-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="94e76-148">Obsługiwane przeglądarki</span><span class="sxs-lookup"><span data-stu-id="94e76-148">Supported browsers</span></span>
<span data-ttu-id="94e76-149">Powłoka w chmurze jest zalecane Chrome, Edge i przeglądarki Safari.</span><span class="sxs-lookup"><span data-stu-id="94e76-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="94e76-150">Powłoka chmury jest obsługiwana dla programu Chrome, Firefox Safari, IE i krawędzi, powłoki chmury jest ustawienia przeglądarki toospecific podmiotu.</span><span class="sxs-lookup"><span data-stu-id="94e76-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="94e76-151">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="94e76-151">Troubleshooting</span></span>
1. <span data-ttu-id="94e76-152">Podczas korzystania z subskrypcji usługi Azure Active Directory, nie można utworzyć magazynu z powodu tooError: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="94e76-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="94e76-153">tooresolve, użyj subskrypcji platformy Azure umożliwia tworzenie zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="94e76-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="94e76-154">Subskrypcje AD są toocreate nie jest w stanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94e76-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="94e76-155">Dla określonego znane ograniczenia, odwiedź stronę [ograniczenia powłoki chmury](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="94e76-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
