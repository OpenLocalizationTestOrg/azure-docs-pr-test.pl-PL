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
# <a name="install-the-azure-cli-10"></a>Zainstaluj Azure CLI 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Interfejs wiersza polecenia platformy Azure 1.0](cli-install-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> W tym temacie opisano sposób instalowania 1.0 interfejsu wiersza polecenia Azure, który jest oparty na środowisku nodeJs i obsługuje wszystkie wywołania interfejsu API wdrożenie klasyczne, a także dużą liczbę działań wdrożenia usługi Resource Manager. Należy używać [Azure CLI 2.0](/cli/azure/overview) nowych lub nowoczesne wdrożeń interfejsu wiersza polecenia i zarządzania.

Szybko zainstalować interfejs wiersza polecenia platformy Azure (Azure CLI 1.0) Aby użyć zestawu open source oparty na powłoce poleceń do tworzenia i zarządzania zasobami na platformie Microsoft Azure. Istnieje kilka opcji, aby zainstalować te narzędzia i platform na komputerze:

* **Pakiet npm** — Uruchom npm (Menedżer pakietów dla języka JavaScript), aby zainstalować najnowszy pakiet Azure CLI 1.0 na dystrybucji systemu Linux lub OS. Wymaga środowiska node.js i npm na tym komputerze.
* **Instalator** — Pobierz Instalator prosta instalacja na Mac lub Windows.
* **Kontener docker** — rozpocząć korzystanie z najnowszych interfejsu wiersza polecenia w kontenerze Docker gotowy do uruchomienia. Wymaga Docker hosta na komputerze.

Aby uzyskać więcej opcji i tło, zobacz repozytorium projektu w [GitHub](https://github.com/azure/azure-xplat-cli).

Po zainstalowaniu programu Azure CLI 1.0 [połącz go z subskrypcją platformy Azure](xplat-cli-connect.md) i uruchom **azure** poleceń z interfejsu wiersza polecenia (Bash, Terminal wiersza polecenia i tak dalej) do pracy z zasobami platformy Azure.

## <a name="option-1-install-an-npm-package"></a>Opcja 1: Zainstaluj pakiet npm
Aby zainstalować interfejsu wiersza polecenia z pakietu npm, upewnij się, zostały pobrane i zainstalowane [najnowsze Node.js i npm](https://nodejs.org/en/download/package-manager/). Następnie uruchom **instalacji narzędzia npm** do zainstalowania pakietu wiersza polecenia platformy azure:

```bash
npm install -g azure-cli
```

Na dystrybucje systemu Linux, należy użyć **sudo** do pomyślnego uruchomienia **npm** polecenia w następujący sposób:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Jeśli musisz zainstalować lub zaktualizować Node.js i npm na dystrybucji systemu Linux lub OS, zaleca się zainstalowanie najnowszej wersji środowiska Node.js LTS (4.x). Jeśli używasz starszej wersji, mogą wystąpić błędy instalacji.

Jeśli wolisz, Pobierz najnowszą Linux [pliku tar] [ linux-installer] lokalnie pakietu npm. Następnie należy zainstalować pakiet npm pobranego w następujący sposób (na dystrybucje systemu Linux, konieczne może być **sudo**):

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opcja 2: Skorzystać z Instalatora
Jeśli używasz komputera Mac lub Windows następujące instalatorów interfejsu wiersza polecenia są dostępne do pobrania:

* [Instalator systemu Mac OS X][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> W systemie Windows, możesz również pobrać [Instalatora platformy sieci Web](https://go.microsoft.com/?linkid=9828653) do zainstalowania interfejsu wiersza polecenia. Ten Instalator daje możliwość zainstalowania dodatkowych zestaw Azure SDK i narzędzia wiersza polecenia po zainstalowaniu interfejsu wiersza polecenia.

## <a name="option-3-use-a-docker-container"></a>Opcja 3: Umieszczenie w kontenerze Docker
Jeśli po skonfigurowaniu komputera jako [Docker](https://docs.docker.com/engine/understanding-docker/) hosta, można uruchomić najnowsze 1.0 interfejsu wiersza polecenia platformy Azure w kontenerze Docker. Uruchom następujące polecenie (na dystrybucje systemu Linux, konieczne może być **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Uruchom polecenia interfejsu wiersza polecenia platformy Azure w wersji 1.0
Po zainstalowaniu 1.0 interfejsu wiersza polecenia Azure, uruchom **azure** polecenie z interfejsu wiersza polecenia użytkownika (Bash, Terminal wiersza polecenia i tak dalej). Na przykład aby uruchomić polecenie Pomoc, wpisz następujące polecenie:

```azurecli
azure help
```

> [!NOTE]
> W niektórych dystrybucji systemu Linux, może wystąpić błąd podobny do `/usr/bin/env: ‘node’: No such file or directory`. Ten błąd jest dostarczany z ostatnich instalacji środowiska node.js, instalowana na /usr/bin/nodejs. Aby rozwiązać problem, Utwórz link symboliczny do /usr/bin/node, uruchamiając polecenie:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

Aby wyświetlić wersję 1.0 interfejsu wiersza polecenia platformy Azure został zainstalowany, wpisz następujące polecenie:

```azurecli
azure --version
```

Teraz wszystko jest gotowe! Wszystkie polecenia interfejsu wiersza polecenia do pracy z własnych zasobów, dostęp do [nawiązać połączenia z subskrypcją platformy Azure z wiersza polecenia platformy Azure](xplat-cli-connect.md).

> [!NOTE]
> Przy pierwszym użyciu interfejsu wiersza polecenia Azure, zostanie wyświetlony komunikat z pytaniem, jeśli chcesz zezwolić firmie Microsoft na zbieranie informacji o użyciu. Uczestnictwo jest dobrowolne. Jeśli zdecydujesz się uczestniczyć, można zatrzymać w dowolnym momencie, uruchamiając `azure telemetry --disable`. Aby włączyć udział w dowolnym momencie, uruchom polecenie `azure telemetry --enable`.

## <a name="update-the-cli"></a>Aktualizowanie interfejsu wiersza polecenia
Firma Microsoft udostępnia często zaktualizowane wersje interfejsu wiersza polecenia Azure. Ponownie zainstaluj interfejs wiersza polecenia za pomocą Instalatora systemu operacyjnego lub uruchom najnowsze kontenera Docker. Lub, jeśli masz najnowsze Node.js i npm zainstalowanych aktualizacji, wpisując następujące (na dystrybucje systemu Linux, konieczne może być **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Włącz uzupełniania po naciśnięciu tabulatora
Uzupełnianie po naciśnięciu tabulatora poleceń interfejsu wiersza polecenia jest obsługiwana dla komputerów Mac i Linux.

Aby włączyć ją w zsh, uruchom polecenie:

```bash
echo '. <(azure --completion)' >> .zshrc
```

Aby włączyć ją w bash, uruchom polecenie:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Następne kroki
* [Połącz z poziomu interfejsu wiersza polecenia do subskrypcji platformy Azure](xplat-cli-connect.md) do tworzenia i zarządzania zasobami Azure.
* Aby dowiedzieć się więcej o Azure CLI, pobierania kodu źródłowego, zgłaszanie problemów lub przyczyniają się do projektu, odwiedź stronę [repozytorium GitHub dla interfejsu wiersza polecenia Azure](https://github.com/azure/azure-xplat-cli).
* Jeśli masz pytania dotyczące używania interfejsu wiersza polecenia Azure lub usługi Azure, odwiedź stronę [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
