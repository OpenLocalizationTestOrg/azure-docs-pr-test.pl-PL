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
# <a name="install-hello-azure-cli-10"></a>Zainstaluj hello Azure CLI w wersji 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Interfejs wiersza polecenia platformy Azure 1.0](cli-install-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> W tym temacie opisano, jak wywołuje tooinstall hello Azure CLI 1.0, który jest oparty na środowisku nodeJs i obsługuje wszystkie wdrożenia klasycznego interfejsu API oraz dużą liczbę działań wdrożenia usługi Resource Manager. Należy używać hello [Azure CLI 2.0](/cli/azure/overview) nowych lub nowoczesne wdrożeń interfejsu wiersza polecenia i zarządzania.

Szybko zainstalować hello interfejsu wiersza polecenia platformy Azure (Azure CLI 1.0) toouse zestaw open source oparty na powłoce poleceń do tworzenia i zarządzania zasobami na platformie Microsoft Azure. Masz kilka opcji tooinstall tych narzędzi i platform na komputerze:

* **Pakiet npm** — wykonywania (Menedżera pakietów hello JavaScript) tooinstall hello najnowsze Azure CLI 1.0 pakietu npm na dystrybucji systemu Linux lub OS. Wymaga środowiska node.js i npm na tym komputerze.
* **Instalator** — Pobierz Instalator prosta instalacja na Mac lub Windows.
* **Kontener docker** — uruchamiania przy użyciu hello najnowszej CLI w kontenerze Docker gotowy do uruchomienia. Wymaga Docker hosta na komputerze.

Więcej opcji i tła dla repozytorium projektu hello na [GitHub](https://github.com/azure/azure-xplat-cli).

Po zainstalowaniu hello Azure CLI 1.0 [połącz go z subskrypcją platformy Azure](xplat-cli-connect.md) i wykonywania hello **azure** poleceń z interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia i tak dalej) toowork z zasobów platformy Azure.

## <a name="option-1-install-an-npm-package"></a>Opcja 1: Zainstaluj pakiet npm
Witaj tooinstall interfejsu wiersza polecenia z pakietu npm, upewnij się, że zostały pobrane i zainstalowane hello [najnowsze Node.js i npm](https://nodejs.org/en/download/package-manager/). Następnie uruchom **instalacji narzędzia npm** tooinstall hello azure cli pakietu:

```bash
npm install -g azure-cli
```

Na dystrybucje systemu Linux, może być konieczne toouse **sudo** toosuccessfully Uruchom hello **npm** polecenia w następujący sposób:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Jeśli muszą tooinstall lub Node.js i npm na dystrybucji systemu Linux lub OS aktualizacji, zaleca się zainstalowanie najnowszej wersji środowiska Node.js LTS hello (4.x). Jeśli używasz starszej wersji, mogą wystąpić błędy instalacji.

Jeśli wolisz, Pobierz hello najnowsze Linux [pliku tar] [ linux-installer] dla hello npm pakiet lokalnie. Następnie należy zainstalować pakiet npm pobrany hello w następujący sposób (na dystrybucje systemu Linux mogą wymagać toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opcja 2: Skorzystać z Instalatora
Jeśli używasz komputera Mac lub Windows hello po instalatorów interfejsu wiersza polecenia są dostępne do pobrania:

* [Instalator systemu Mac OS X][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> W systemie Windows, można również pobrać hello [Instalatora platformy sieci Web](https://go.microsoft.com/?linkid=9828653) hello tooinstall interfejsu wiersza polecenia. Dzięki temu Instalator hello tooinstall opcji dodatkowych zestaw Azure SDK i narzędzia wiersza polecenia po zainstalowaniu hello interfejsu wiersza polecenia.

## <a name="option-3-use-a-docker-container"></a>Opcja 3: Umieszczenie w kontenerze Docker
Jeśli po skonfigurowaniu komputera jako [Docker](https://docs.docker.com/engine/understanding-docker/) hosta, możesz uruchomić hello najnowsze 1.0 interfejsu wiersza polecenia platformy Azure w kontenerze Docker. Uruchom hello następujące polecenie (na dystrybucje systemu Linux mogą wymagać toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Uruchom polecenia interfejsu wiersza polecenia platformy Azure w wersji 1.0
Po zainstalowaniu hello Azure CLI w wersji 1.0, uruchom hello **azure** polecenie z interfejsu wiersza polecenia użytkownika (Bash, Terminal wiersza polecenia i tak dalej). Na przykład toorun hello pomoc polecenia, wpisz następujące hello:

```azurecli
azure help
```

> [!NOTE]
> W niektórych dystrybucji systemu Linux, może wystąpić błąd podobny zbyt`/usr/bin/env: ‘node’: No such file or directory`. Ten błąd jest dostarczany z ostatnich instalacji środowiska node.js, instalowana na /usr/bin/nodejs. toofix, utworzyć łącze symboliczne zbyt/usr/bin/węzła, uruchamiając polecenie:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

Wersja hello toosee hello Azure CLI 1.0 został zainstalowany, hello typu następujące:

```azurecli
azure --version
```

Teraz wszystko jest gotowe! wszystkie tooaccess hello toowork polecenia interfejsu wiersza polecenia przy użyciu własnych zasobów, [połączyć tooyour subskrypcji platformy Azure z hello Azure CLI](xplat-cli-connect.md).

> [!NOTE]
> Przy pierwszym użyciu interfejsu wiersza polecenia Azure, zobaczysz komunikat z pytaniem, czy ma tooallow informacje o użyciu toocollect firmy Microsoft. Uczestnictwo jest dobrowolne. Jeśli wybierzesz tooparticipate, można zatrzymać w dowolnym momencie, uruchamiając `azure telemetry --disable`. udział tooenable w dowolnym momencie uruchomić `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Aktualizacja hello interfejsu wiersza polecenia
Firma Microsoft udostępnia często zaktualizowane wersje hello wiersza polecenia platformy Azure. Zainstaluj ponownie hello interfejsu wiersza polecenia przy użyciu hello Instalatora systemu operacyjnego lub uruchom hello najnowsze kontenera Docker. Lub, jeśli mają hello najnowsze Node.js i npm zainstalowany, należy zaktualizować, wpisując następujące hello (na dystrybucje systemu Linux mogą wymagać toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Włącz uzupełniania po naciśnięciu tabulatora
Uzupełnianie po naciśnięciu tabulatora poleceń interfejsu wiersza polecenia jest obsługiwana dla komputerów Mac i Linux.

tooenable w zsh, uruchom:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable w bash, uruchom:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Następne kroki
* [Nawiązywanie połączenia z tooyour CLI hello subskrypcji platformy Azure](xplat-cli-connect.md) toocreate zasobów platformy Azure i zarządzanie nimi.
* toolearn więcej informacji na temat hello Azure CLI, pobrać kodu źródłowego, zgłaszanie problemów, lub współtworzenia toohello projektu, odwiedź hello [repozytorium GitHub hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Jeśli masz pytania dotyczące używania hello Azure CLI lub Azure, odwiedź stronę hello [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
