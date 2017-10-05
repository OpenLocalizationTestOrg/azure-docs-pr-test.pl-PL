---
title: Zainstaluj Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Zainstaluj 1.0 interfejsu wiersza polecenia platformy Azure dla Mac, Linux i Windows rozpocząć korzystanie z usług Azure"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="e6473-103">Zainstaluj Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e6473-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6473-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6473-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="e6473-105">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e6473-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="e6473-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e6473-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="e6473-107">W tym temacie opisano sposób instalowania 1.0 interfejsu wiersza polecenia Azure, który jest oparty na środowisku nodeJs i obsługuje wszystkie wywołania interfejsu API wdrożenie klasyczne, a także dużą liczbę działań wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6473-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="e6473-108">Należy używać [Azure CLI 2.0](/cli/azure/overview) nowych lub nowoczesne wdrożeń interfejsu wiersza polecenia i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e6473-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="e6473-109">Szybko zainstalować interfejs wiersza polecenia platformy Azure (Azure CLI 1.0) Aby użyć zestawu open source oparty na powłoce poleceń do tworzenia i zarządzania zasobami na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e6473-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="e6473-110">Istnieje kilka opcji, aby zainstalować te narzędzia i platform na komputerze:</span><span class="sxs-lookup"><span data-stu-id="e6473-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="e6473-111">**Pakiet npm** — Uruchom npm (Menedżer pakietów dla języka JavaScript), aby zainstalować najnowszy pakiet Azure CLI 1.0 na dystrybucji systemu Linux lub OS.</span><span class="sxs-lookup"><span data-stu-id="e6473-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="e6473-112">Wymaga środowiska node.js i npm na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6473-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="e6473-113">**Instalator** — Pobierz Instalator prosta instalacja na Mac lub Windows.</span><span class="sxs-lookup"><span data-stu-id="e6473-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="e6473-114">**Kontener docker** — rozpocząć korzystanie z najnowszych interfejsu wiersza polecenia w kontenerze Docker gotowy do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e6473-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="e6473-115">Wymaga Docker hosta na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6473-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="e6473-116">Aby uzyskać więcej opcji i tło, zobacz repozytorium projektu w [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="e6473-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="e6473-117">Po zainstalowaniu programu Azure CLI 1.0 [połącz go z subskrypcją platformy Azure](xplat-cli-connect.md) i uruchom **azure** poleceń z interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia i tak dalej) do pracy z zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e6473-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="e6473-118">Opcja 1: Zainstaluj pakiet npm</span><span class="sxs-lookup"><span data-stu-id="e6473-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="e6473-119">Aby zainstalować interfejsu wiersza polecenia z pakietu npm, upewnij się, zostały pobrane i zainstalowane [najnowsze Node.js i npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="e6473-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="e6473-120">Następnie uruchom **instalacji narzędzia npm** do zainstalowania pakietu wiersza polecenia platformy azure:</span><span class="sxs-lookup"><span data-stu-id="e6473-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="e6473-121">Na dystrybucje systemu Linux, należy użyć **sudo** do pomyślnego uruchomienia **npm** polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e6473-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="e6473-122">Jeśli musisz zainstalować lub zaktualizować Node.js i npm na dystrybucji systemu Linux lub OS, zaleca się zainstalowanie najnowszej wersji środowiska Node.js LTS (4.x).</span><span class="sxs-lookup"><span data-stu-id="e6473-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="e6473-123">Jeśli używasz starszej wersji, mogą wystąpić błędy instalacji.</span><span class="sxs-lookup"><span data-stu-id="e6473-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="e6473-124">Jeśli wolisz, Pobierz najnowszą Linux [pliku tar] [ linux-installer] lokalnie pakietu npm.</span><span class="sxs-lookup"><span data-stu-id="e6473-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="e6473-125">Następnie należy zainstalować pakiet npm pobranego w następujący sposób (na dystrybucje systemu Linux, konieczne może być **sudo**):</span><span class="sxs-lookup"><span data-stu-id="e6473-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="e6473-126">Opcja 2: Skorzystać z Instalatora</span><span class="sxs-lookup"><span data-stu-id="e6473-126">Option 2: Use an installer</span></span>
<span data-ttu-id="e6473-127">Jeśli używasz komputera Mac lub Windows następujące instalatorów interfejsu wiersza polecenia są dostępne do pobrania:</span><span class="sxs-lookup"><span data-stu-id="e6473-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="e6473-128">[Instalator systemu Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="e6473-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="e6473-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="e6473-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="e6473-130">W systemie Windows, możesz również pobrać [Instalatora platformy sieci Web](https://go.microsoft.com/?linkid=9828653) do zainstalowania interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6473-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="e6473-131">Ten Instalator daje możliwość zainstalowania dodatkowych zestaw Azure SDK i narzędzia wiersza polecenia po zainstalowaniu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6473-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="e6473-132">Opcja 3: Umieszczenie w kontenerze Docker</span><span class="sxs-lookup"><span data-stu-id="e6473-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="e6473-133">Jeśli po skonfigurowaniu komputera jako [Docker](https://docs.docker.com/engine/understanding-docker/) hosta, można uruchomić najnowsze 1.0 interfejsu wiersza polecenia platformy Azure w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="e6473-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="e6473-134">Uruchom następujące polecenie (na dystrybucje systemu Linux, konieczne może być **sudo**):</span><span class="sxs-lookup"><span data-stu-id="e6473-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="e6473-135">Uruchom polecenia interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="e6473-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="e6473-136">Po zainstalowaniu 1.0 interfejsu wiersza polecenia Azure, uruchom **azure** polecenie z interfejsu wiersza polecenia użytkownika (Bash, Terminal wiersza polecenia i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="e6473-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="e6473-137">Na przykład aby uruchomić polecenie Pomoc, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6473-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="e6473-138">W niektórych dystrybucji systemu Linux, może wystąpić błąd podobny do `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="e6473-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="e6473-139">Ten błąd jest dostarczany z ostatnich instalacji środowiska node.js, instalowana na /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="e6473-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="e6473-140">Aby rozwiązać problem, Utwórz link symboliczny do /usr/bin/node, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6473-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="e6473-141">Aby wyświetlić wersję 1.0 interfejsu wiersza polecenia platformy Azure został zainstalowany, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6473-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="e6473-142">Teraz wszystko jest gotowe!</span><span class="sxs-lookup"><span data-stu-id="e6473-142">Now you are ready!</span></span> <span data-ttu-id="e6473-143">Wszystkie polecenia interfejsu wiersza polecenia do pracy z własnych zasobów, dostęp do [nawiązać połączenia z subskrypcją platformy Azure z wiersza polecenia platformy Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e6473-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e6473-144">Przy pierwszym użyciu interfejsu wiersza polecenia Azure, zostanie wyświetlony komunikat z pytaniem, jeśli chcesz zezwolić firmie Microsoft na zbieranie informacji o użyciu.</span><span class="sxs-lookup"><span data-stu-id="e6473-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="e6473-145">Uczestnictwo jest dobrowolne.</span><span class="sxs-lookup"><span data-stu-id="e6473-145">Participation is voluntary.</span></span> <span data-ttu-id="e6473-146">Jeśli zdecydujesz się uczestniczyć, można zatrzymać w dowolnym momencie, uruchamiając `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="e6473-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="e6473-147">Aby włączyć udział w dowolnym momencie, uruchom polecenie `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="e6473-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="e6473-148">Aktualizowanie interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e6473-148">Update the CLI</span></span>
<span data-ttu-id="e6473-149">Firma Microsoft udostępnia często zaktualizowane wersje interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="e6473-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="e6473-150">Ponownie zainstaluj interfejs wiersza polecenia za pomocą Instalatora systemu operacyjnego lub uruchom najnowsze kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="e6473-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="e6473-151">Lub, jeśli masz najnowsze Node.js i npm zainstalowanych aktualizacji, wpisując następujące (na dystrybucje systemu Linux, konieczne może być **sudo**).</span><span class="sxs-lookup"><span data-stu-id="e6473-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="e6473-152">Włącz uzupełniania po naciśnięciu tabulatora</span><span class="sxs-lookup"><span data-stu-id="e6473-152">Enable tab completion</span></span>
<span data-ttu-id="e6473-153">Uzupełnianie po naciśnięciu tabulatora poleceń interfejsu wiersza polecenia jest obsługiwana dla komputerów Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="e6473-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="e6473-154">Aby włączyć ją w zsh, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6473-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="e6473-155">Aby włączyć ją w bash, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6473-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="e6473-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6473-156">Next steps</span></span>
* <span data-ttu-id="e6473-157">[Połącz z poziomu interfejsu wiersza polecenia do subskrypcji platformy Azure](xplat-cli-connect.md) do tworzenia i zarządzania zasobami Azure.</span><span class="sxs-lookup"><span data-stu-id="e6473-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="e6473-158">Aby dowiedzieć się więcej o Azure CLI, pobierania kodu źródłowego, zgłaszanie problemów lub przyczyniają się do projektu, odwiedź stronę [repozytorium GitHub dla interfejsu wiersza polecenia Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="e6473-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="e6473-159">Jeśli masz pytania dotyczące używania interfejsu wiersza polecenia Azure lub usługi Azure, odwiedź stronę [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="e6473-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
