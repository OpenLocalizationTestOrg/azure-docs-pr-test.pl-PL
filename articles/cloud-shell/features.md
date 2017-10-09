---
title: "aaaAzure funkcji chmury powłoki (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji powłoki chmury Azure"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="a99e8-103">Funkcje i narzędzia dla chmury Azure powłoki</span><span class="sxs-lookup"><span data-stu-id="a99e8-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="a99e8-104">Powłoka chmury Azure jest toomanage środowisko powłoki przeglądarki i tworzenie zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="a99e8-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="a99e8-105">Chmura powłoki oferuje przeglądarki dostępny, wstępnie skonfigurowane środowisko powłoki zarządzania zasobami Azure bez zwiększania hello instalacja, przechowywanie wersji i obsługa maszynę, samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="a99e8-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="a99e8-106">Powłoka chmury udostępnia maszyn, na podstawie żądań i w związku z tym maszyny stanu nie będzie zachowywane między sesjami.</span><span class="sxs-lookup"><span data-stu-id="a99e8-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="a99e8-107">Ponieważ powłoki chmury jest skompilowany dla sesji interaktywne, powłok automatycznie usunięte po upływie 20 minut braku aktywności powłoki.</span><span class="sxs-lookup"><span data-stu-id="a99e8-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="a99e8-108">Bash w powłoce chmury</span><span class="sxs-lookup"><span data-stu-id="a99e8-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="a99e8-109">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="a99e8-109">Tools</span></span>
|<span data-ttu-id="a99e8-110">Kategoria</span><span class="sxs-lookup"><span data-stu-id="a99e8-110">Category</span></span>   |<span data-ttu-id="a99e8-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a99e8-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="a99e8-112">Interpreter powłoki systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a99e8-112">Linux shell interpreter</span></span>|<span data-ttu-id="a99e8-113">Bash</span><span class="sxs-lookup"><span data-stu-id="a99e8-113">Bash</span></span><br> <span data-ttu-id="a99e8-114">Pokaż</span><span class="sxs-lookup"><span data-stu-id="a99e8-114">sh</span></span>               |
|<span data-ttu-id="a99e8-115">Narzędzia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a99e8-115">Azure tools</span></span>            |<span data-ttu-id="a99e8-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) i [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="a99e8-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="a99e8-117">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="a99e8-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="a99e8-118">Usługa Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="a99e8-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="a99e8-119">Edytory tekstów</span><span class="sxs-lookup"><span data-stu-id="a99e8-119">Text editors</span></span>           |<span data-ttu-id="a99e8-120">VIM</span><span class="sxs-lookup"><span data-stu-id="a99e8-120">vim</span></span><br> <span data-ttu-id="a99e8-121">nano</span><span class="sxs-lookup"><span data-stu-id="a99e8-121">nano</span></span><br> <span data-ttu-id="a99e8-122">emacs:</span><span class="sxs-lookup"><span data-stu-id="a99e8-122">emacs</span></span>       |
|<span data-ttu-id="a99e8-123">Kontrola źródła</span><span class="sxs-lookup"><span data-stu-id="a99e8-123">Source control</span></span>         |<span data-ttu-id="a99e8-124">git</span><span class="sxs-lookup"><span data-stu-id="a99e8-124">git</span></span>                    |
|<span data-ttu-id="a99e8-125">Narzędzi do kompilacji</span><span class="sxs-lookup"><span data-stu-id="a99e8-125">Build tools</span></span>            |<span data-ttu-id="a99e8-126">Wprowadź</span><span class="sxs-lookup"><span data-stu-id="a99e8-126">make</span></span><br> <span data-ttu-id="a99e8-127">maven</span><span class="sxs-lookup"><span data-stu-id="a99e8-127">maven</span></span><br> <span data-ttu-id="a99e8-128">npm</span><span class="sxs-lookup"><span data-stu-id="a99e8-128">npm</span></span><br> <span data-ttu-id="a99e8-129">PIP</span><span class="sxs-lookup"><span data-stu-id="a99e8-129">pip</span></span>         |
|<span data-ttu-id="a99e8-130">Kontenery</span><span class="sxs-lookup"><span data-stu-id="a99e8-130">Containers</span></span>             |<span data-ttu-id="a99e8-131">[Interfejs wiersza polecenia docker](https://github.com/docker/cli)/[Docker maszyny](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="a99e8-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="a99e8-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="a99e8-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="a99e8-133">Projekt</span><span class="sxs-lookup"><span data-stu-id="a99e8-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="a99e8-134">INTERFEJS WIERSZA POLECENIA DC/OS</span><span class="sxs-lookup"><span data-stu-id="a99e8-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="a99e8-135">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="a99e8-135">Databases</span></span>              |<span data-ttu-id="a99e8-136">Klienta MySQL</span><span class="sxs-lookup"><span data-stu-id="a99e8-136">MySQL client</span></span><br> <span data-ttu-id="a99e8-137">PostgreSql klienta</span><span class="sxs-lookup"><span data-stu-id="a99e8-137">PostgreSql client</span></span><br> [<span data-ttu-id="a99e8-138">Narzędzia sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a99e8-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="a99e8-139">Autorzy MSSQL skryptów</span><span class="sxs-lookup"><span data-stu-id="a99e8-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="a99e8-140">Inne</span><span class="sxs-lookup"><span data-stu-id="a99e8-140">Other</span></span>                  |<span data-ttu-id="a99e8-141">iPython klienta</span><span class="sxs-lookup"><span data-stu-id="a99e8-141">iPython Client</span></span><br> [<span data-ttu-id="a99e8-142">Chmura Foundry interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a99e8-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="a99e8-143">Obsługa języków</span><span class="sxs-lookup"><span data-stu-id="a99e8-143">Language support</span></span>
|<span data-ttu-id="a99e8-144">Język</span><span class="sxs-lookup"><span data-stu-id="a99e8-144">Language</span></span>   |<span data-ttu-id="a99e8-145">Wersja</span><span class="sxs-lookup"><span data-stu-id="a99e8-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="a99e8-146">.NET</span><span class="sxs-lookup"><span data-stu-id="a99e8-146">.NET</span></span>       |<span data-ttu-id="a99e8-147">1.01</span><span class="sxs-lookup"><span data-stu-id="a99e8-147">1.01</span></span>       |
|<span data-ttu-id="a99e8-148">Przejdź</span><span class="sxs-lookup"><span data-stu-id="a99e8-148">Go</span></span>         |<span data-ttu-id="a99e8-149">1.7</span><span class="sxs-lookup"><span data-stu-id="a99e8-149">1.7</span></span>        |
|<span data-ttu-id="a99e8-150">Java</span><span class="sxs-lookup"><span data-stu-id="a99e8-150">Java</span></span>       |<span data-ttu-id="a99e8-151">1.8</span><span class="sxs-lookup"><span data-stu-id="a99e8-151">1.8</span></span>        |
|<span data-ttu-id="a99e8-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="a99e8-152">Node.js</span></span>    |<span data-ttu-id="a99e8-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="a99e8-153">6.9.4</span></span>      |
|<span data-ttu-id="a99e8-154">Python</span><span class="sxs-lookup"><span data-stu-id="a99e8-154">Python</span></span>     |<span data-ttu-id="a99e8-155">2.7 i 3.5 (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="a99e8-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="a99e8-156">Bezpieczne uwierzytelnianie automatyczne</span><span class="sxs-lookup"><span data-stu-id="a99e8-156">Secure automatic authentication</span></span>
<span data-ttu-id="a99e8-157">Chmury powłoki bezpiecznie i automatycznie uwierzytelnia dostęp konta dla hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a99e8-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="a99e8-158">Azure trwałości plików</span><span class="sxs-lookup"><span data-stu-id="a99e8-158">Azure Files persistence</span></span>
<span data-ttu-id="a99e8-159">Ponieważ powłoki w chmurze jest przydzielony dla danego żądania przy użyciu tymczasowej maszyny, pliki poza Twojej $Home i maszyny stanu nie są zachowywane między sesjami.</span><span class="sxs-lookup"><span data-stu-id="a99e8-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="a99e8-160">pliki toopersist między sesjami, przeszukiwań powłoki w chmurze za pośrednictwem dołączanie plików na platformę Azure udostępniania przy pierwszym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="a99e8-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="a99e8-161">Po zakończeniu powłoki chmury dołączać automatycznie magazynu dla wszystkich przyszłych sesji.</span><span class="sxs-lookup"><span data-stu-id="a99e8-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="a99e8-162">Dowiedz się więcej na temat dołączania tooCloud udziałów plików na platformę Azure powłoki.</span><span class="sxs-lookup"><span data-stu-id="a99e8-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="a99e8-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a99e8-163">Next steps</span></span>
[<span data-ttu-id="a99e8-164">Szybki Start powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="a99e8-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="a99e8-165">
[Więcej informacji na temat usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="a99e8-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>