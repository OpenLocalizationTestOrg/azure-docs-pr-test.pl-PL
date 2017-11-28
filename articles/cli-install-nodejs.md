---
title: aaaInstall hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Zainstaluj hello Azure CLI 1.0 dla komputerów Mac, Linux i Windows toostart przy użyciu usług Azure"
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
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="a9dad-103">Zainstaluj hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a9dad-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9dad-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9dad-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="a9dad-105">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="a9dad-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="a9dad-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a9dad-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="a9dad-107">W tym temacie opisano, jak wywołuje tooinstall hello Azure CLI 1.0, który jest oparty na środowisku nodeJs i obsługuje wszystkie wdrożenia klasycznego interfejsu API oraz dużą liczbę działań wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9dad-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="a9dad-108">Należy używać hello [Azure CLI 2.0](/cli/azure/overview) nowych lub nowoczesne wdrożeń interfejsu wiersza polecenia i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a9dad-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="a9dad-109">Szybko zainstalować hello interfejsu wiersza polecenia platformy Azure (Azure CLI 1.0) toouse zestaw open source oparty na powłoce poleceń do tworzenia i zarządzania zasobami na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dad-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="a9dad-110">Masz kilka opcji tooinstall tych narzędzi i platform na komputerze:</span><span class="sxs-lookup"><span data-stu-id="a9dad-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="a9dad-111">**Pakiet npm** — wykonywania (Menedżera pakietów hello JavaScript) tooinstall hello najnowsze Azure CLI 1.0 pakietu npm na dystrybucji systemu Linux lub OS.</span><span class="sxs-lookup"><span data-stu-id="a9dad-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="a9dad-112">Wymaga środowiska node.js i npm na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a9dad-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="a9dad-113">**Instalator** — Pobierz Instalator prosta instalacja na Mac lub Windows.</span><span class="sxs-lookup"><span data-stu-id="a9dad-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="a9dad-114">**Kontener docker** — uruchamiania przy użyciu hello najnowszej CLI w kontenerze Docker gotowy do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="a9dad-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="a9dad-115">Wymaga Docker hosta na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a9dad-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="a9dad-116">Więcej opcji i tła dla repozytorium projektu hello na [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="a9dad-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="a9dad-117">Po zainstalowaniu hello Azure CLI 1.0 [połącz go z subskrypcją platformy Azure](xplat-cli-connect.md) i wykonywania hello **azure** poleceń z interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia i tak dalej) toowork z zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dad-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="a9dad-118">Opcja 1: Zainstaluj pakiet npm</span><span class="sxs-lookup"><span data-stu-id="a9dad-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="a9dad-119">Witaj tooinstall interfejsu wiersza polecenia z pakietu npm, upewnij się, że zostały pobrane i zainstalowane hello [najnowsze Node.js i npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="a9dad-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="a9dad-120">Następnie uruchom **instalacji narzędzia npm** tooinstall hello azure cli pakietu:</span><span class="sxs-lookup"><span data-stu-id="a9dad-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="a9dad-121">Na dystrybucje systemu Linux, może być konieczne toouse **sudo** toosuccessfully Uruchom hello **npm** polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a9dad-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="a9dad-122">Jeśli muszą tooinstall lub Node.js i npm na dystrybucji systemu Linux lub OS aktualizacji, zaleca się zainstalowanie najnowszej wersji środowiska Node.js LTS hello (4.x).</span><span class="sxs-lookup"><span data-stu-id="a9dad-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="a9dad-123">Jeśli używasz starszej wersji, mogą wystąpić błędy instalacji.</span><span class="sxs-lookup"><span data-stu-id="a9dad-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="a9dad-124">Jeśli wolisz, Pobierz hello najnowsze Linux [pliku tar] [ linux-installer] dla hello npm pakiet lokalnie.</span><span class="sxs-lookup"><span data-stu-id="a9dad-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="a9dad-125">Następnie należy zainstalować pakiet npm pobrany hello w następujący sposób (na dystrybucje systemu Linux mogą wymagać toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="a9dad-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="a9dad-126">Opcja 2: Skorzystać z Instalatora</span><span class="sxs-lookup"><span data-stu-id="a9dad-126">Option 2: Use an installer</span></span>
<span data-ttu-id="a9dad-127">Jeśli używasz komputera Mac lub Windows hello po instalatorów interfejsu wiersza polecenia są dostępne do pobrania:</span><span class="sxs-lookup"><span data-stu-id="a9dad-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="a9dad-128">[Instalator systemu Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="a9dad-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="a9dad-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="a9dad-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="a9dad-130">W systemie Windows, można również pobrać hello [Instalatora platformy sieci Web](https://go.microsoft.com/?linkid=9828653) hello tooinstall interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9dad-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="a9dad-131">Dzięki temu Instalator hello tooinstall opcji dodatkowych zestaw Azure SDK i narzędzia wiersza polecenia po zainstalowaniu hello interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9dad-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="a9dad-132">Opcja 3: Umieszczenie w kontenerze Docker</span><span class="sxs-lookup"><span data-stu-id="a9dad-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="a9dad-133">Jeśli po skonfigurowaniu komputera jako [Docker](https://docs.docker.com/engine/understanding-docker/) hosta, możesz uruchomić hello najnowsze 1.0 interfejsu wiersza polecenia platformy Azure w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="a9dad-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="a9dad-134">Uruchom hello następujące polecenie (na dystrybucje systemu Linux mogą wymagać toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="a9dad-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="a9dad-135">Uruchom polecenia interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a9dad-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="a9dad-136">Po zainstalowaniu hello Azure CLI w wersji 1.0, uruchom hello **azure** polecenie z interfejsu wiersza polecenia użytkownika (Bash, Terminal wiersza polecenia i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="a9dad-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="a9dad-137">Na przykład toorun hello pomoc polecenia, wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a9dad-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="a9dad-138">W niektórych dystrybucji systemu Linux, może wystąpić błąd podobny zbyt`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="a9dad-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="a9dad-139">Ten błąd jest dostarczany z ostatnich instalacji środowiska node.js, instalowana na /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="a9dad-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="a9dad-140">toofix, utworzyć łącze symboliczne zbyt/usr/bin/węzła, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="a9dad-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="a9dad-141">Wersja hello toosee hello Azure CLI 1.0 został zainstalowany, hello typu następujące:</span><span class="sxs-lookup"><span data-stu-id="a9dad-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="a9dad-142">Teraz wszystko jest gotowe!</span><span class="sxs-lookup"><span data-stu-id="a9dad-142">Now you are ready!</span></span> <span data-ttu-id="a9dad-143">wszystkie tooaccess hello toowork polecenia interfejsu wiersza polecenia przy użyciu własnych zasobów, [połączyć tooyour subskrypcji platformy Azure z hello Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a9dad-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a9dad-144">Przy pierwszym użyciu interfejsu wiersza polecenia Azure, zobaczysz komunikat z pytaniem, czy ma tooallow informacje o użyciu toocollect firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9dad-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="a9dad-145">Uczestnictwo jest dobrowolne.</span><span class="sxs-lookup"><span data-stu-id="a9dad-145">Participation is voluntary.</span></span> <span data-ttu-id="a9dad-146">Jeśli wybierzesz tooparticipate, można zatrzymać w dowolnym momencie, uruchamiając `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="a9dad-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="a9dad-147">udział tooenable w dowolnym momencie uruchomić `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="a9dad-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="a9dad-148">Aktualizacja hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a9dad-148">Update hello CLI</span></span>
<span data-ttu-id="a9dad-149">Firma Microsoft udostępnia często zaktualizowane wersje hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dad-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="a9dad-150">Zainstaluj ponownie hello interfejsu wiersza polecenia przy użyciu hello Instalatora systemu operacyjnego lub uruchom hello najnowsze kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="a9dad-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="a9dad-151">Lub, jeśli mają hello najnowsze Node.js i npm zainstalowany, należy zaktualizować, wpisując następujące hello (na dystrybucje systemu Linux mogą wymagać toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="a9dad-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="a9dad-152">Włącz uzupełniania po naciśnięciu tabulatora</span><span class="sxs-lookup"><span data-stu-id="a9dad-152">Enable tab completion</span></span>
<span data-ttu-id="a9dad-153">Uzupełnianie po naciśnięciu tabulatora poleceń interfejsu wiersza polecenia jest obsługiwana dla komputerów Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="a9dad-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="a9dad-154">tooenable w zsh, uruchom:</span><span class="sxs-lookup"><span data-stu-id="a9dad-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="a9dad-155">tooenable w bash, uruchom:</span><span class="sxs-lookup"><span data-stu-id="a9dad-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="a9dad-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9dad-156">Next steps</span></span>
* <span data-ttu-id="a9dad-157">[Nawiązywanie połączenia z tooyour CLI hello subskrypcji platformy Azure](xplat-cli-connect.md) toocreate zasobów platformy Azure i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="a9dad-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="a9dad-158">toolearn więcej informacji na temat hello Azure CLI, pobrać kodu źródłowego, zgłaszanie problemów, lub współtworzenia toohello projektu, odwiedź hello [repozytorium GitHub hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="a9dad-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="a9dad-159">Jeśli masz pytania dotyczące używania hello Azure CLI lub Azure, odwiedź stronę hello [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="a9dad-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
