---
title: Rozszerzanie eksperymentu z R | Dokumentacja firmy Microsoft
description: "Jak rozszerzyć funkcjonalność usługi Azure Machine Learning Studio za pomocą języka R przy użyciu modułu wykonania skryptu języka R."
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
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="03de3-103">Rozszerzanie eksperymentu przy użyciu języka R</span><span class="sxs-lookup"><span data-stu-id="03de3-103">Extend your experiment with R</span></span>
<span data-ttu-id="03de3-104">Funkcje usługi Azure Machine Learning Studio za pomocą języka R można rozszerzyć za pomocą [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="03de3-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="03de3-105">Ten moduł akceptuje wiele zestawów danych wejściowych i daje jednego zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="03de3-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="03de3-106">Możesz wpisać skrypt języka R w **skrypt języka R** parametr [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="03de3-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="03de3-107">Aby dostęp do każdego portu wejściowego modułu przy użyciu kodu podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="03de3-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="03de3-108">Wyświetlanie listy wszystkich aktualnie zainstalowane pakiety</span><span class="sxs-lookup"><span data-stu-id="03de3-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="03de3-109">Lista zainstalowanych pakietów można zmienić.</span><span class="sxs-lookup"><span data-stu-id="03de3-109">The list of installed packages can change.</span></span> <span data-ttu-id="03de3-110">Lista obecnie zainstalowanych pakietów można znaleźć w [R pakiety obsługiwanych przez usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="03de3-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="03de3-111">Możesz również można uzyskać pełną, bieżącą listę zainstalowanych pakietów wprowadzając następujący kod do [wykonanie skryptu języka R] [ execute-r-script] modułu:</span><span class="sxs-lookup"><span data-stu-id="03de3-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="03de3-112">To wysyła listę pakietów do portem wyjściowym [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="03de3-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="03de3-113">W celu wyświetlenia listy pakietów połączenia takich jak moduł konwersji [Konwertuj do formatu CSV] [ convert-to-csv] po lewej stronie danymi wyjściowymi [wykonanie skryptu języka R] [ execute-r-script] modułu Uruchom eksperyment, a następnie kliknij dane wyjściowe moduł konwersji i wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="03de3-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![Pobieranie danych wyjściowych modułu "Konwertuj do CSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="03de3-115">Importowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="03de3-115">Importing packages</span></span>
<span data-ttu-id="03de3-116">Można importować pakiety, które nie są już zainstalowane za pomocą następujących poleceń w [wykonanie skryptu języka R] [ execute-r-script] modułu:</span><span class="sxs-lookup"><span data-stu-id="03de3-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="03de3-117">gdzie `my_favorite_package.zip` plik zawiera pakiet.</span><span class="sxs-lookup"><span data-stu-id="03de3-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
