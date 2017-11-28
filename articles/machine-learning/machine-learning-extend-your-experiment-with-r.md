---
title: aaaExtend eksperymentu z R | Dokumentacja firmy Microsoft
description: "Jak tooextend hello funkcje usługi Azure Machine Learning Studio za pomocą języka hello R przy użyciu modułu wykonania skryptu języka R hello."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="cbaeb-103">Rozszerzanie eksperymentu przy użyciu języka R</span><span class="sxs-lookup"><span data-stu-id="cbaeb-103">Extend your experiment with R</span></span>
<span data-ttu-id="cbaeb-104">Można rozszerzyć funkcjonalność hello Azure Machine Learning Studio za pomocą języka hello R przy użyciu hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="cbaeb-105">Ten moduł akceptuje wiele zestawów danych wejściowych i daje jednego zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="cbaeb-106">Skrypt języka R można wpisać w hello **skrypt języka R** parametru hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="cbaeb-107">Każdy port wejściowy modułu hello dostęp przy użyciu kodu podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="cbaeb-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="cbaeb-108">Wyświetlanie listy wszystkich aktualnie zainstalowane pakiety</span><span class="sxs-lookup"><span data-stu-id="cbaeb-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="cbaeb-109">można zmienić Hello listę zainstalowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-109">hello list of installed packages can change.</span></span> <span data-ttu-id="cbaeb-110">Lista obecnie zainstalowanych pakietów można znaleźć w [R pakiety obsługiwanych przez usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbaeb-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="cbaeb-111">Również Ci hello pełną, bieżącą listę zainstalowanych pakietów wprowadzając powitania po kodu na powitania [wykonanie skryptu języka R] [ execute-r-script] modułu:</span><span class="sxs-lookup"><span data-stu-id="cbaeb-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="cbaeb-112">To wysyła listę hello portem wyjściowym toohello pakietów hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="cbaeb-113">Pakiet hello tooview listy, takich jak połączyć moduł konwersji [przekonwertować tooCSV] [ convert-to-csv] toohello pozostawione dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script]modułu, uruchom eksperyment hello, następnie kliknij przycisk dane wyjściowe hello hello konwersji moduł i zaznacz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Pobieranie danych wyjściowych modułu "Przekonwertować tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="cbaeb-115">Importowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="cbaeb-115">Importing packages</span></span>
<span data-ttu-id="cbaeb-116">Można importować pakiety, które nie są już zainstalowane za pomocą następującego polecenia w hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu:</span><span class="sxs-lookup"><span data-stu-id="cbaeb-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="cbaeb-117">gdzie hello `my_favorite_package.zip` plik zawiera pakiet.</span><span class="sxs-lookup"><span data-stu-id="cbaeb-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
