---
title: nauki aaaData na powitania maszyny wirtualnej systemu Linux danych nauki | Dokumentacja firmy Microsoft
description: "Jak tooperform kilka typowych nauki danych zadań z hello maszyny Wirtualnej systemu Linux danych nauki."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="53058-103">Nauki danych na powitania maszyny wirtualnej systemu Linux danych nauki</span><span class="sxs-lookup"><span data-stu-id="53058-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="53058-104">W tym przewodniku przedstawiono sposób tooperform kilka typowych nauki danych zadania o hello maszyny Wirtualnej systemu Linux danych nauki.</span><span class="sxs-lookup"><span data-stu-id="53058-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="53058-105">Witaj Linux danych nauki maszyny wirtualnej (DSVM) jest obrazu maszyny wirtualnej na platformie Azure, który jest wstępnie zainstalowane z kolekcją narzędzi powszechnie używany do analizy danych i uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="53058-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="53058-106">składniki oprogramowania klucza Hello są wymienione w hello [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="53058-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="53058-107">Witaj obrazu maszyny Wirtualnej umożliwia łatwe tooget uruchomiona podczas nauki danych (w minutach), bez konieczności tooinstall i skonfiguruj każdy narzędzi hello pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="53058-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="53058-108">Można łatwo skalować hello maszyny Wirtualnej, jeśli to konieczne i zatrzymaj ją nieużywane.</span><span class="sxs-lookup"><span data-stu-id="53058-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="53058-109">Dlatego ten zasób jest zarówno elastyczne i ekonomiczne.</span><span class="sxs-lookup"><span data-stu-id="53058-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="53058-110">Hello zadania nauki danych zostało to pokazane w tym przewodniku wykonaj hello kroki opisane w hello [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="53058-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="53058-111">Ten proces obejmuje nauki toodata systematyczne podejście, umożliwiającą zespoły analityków danych tooeffectively współpracę cyklem hello tworzenia aplikacji inteligentnego.</span><span class="sxs-lookup"><span data-stu-id="53058-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="53058-112">w procesie nauki Hello danych umożliwia również iteracyjne framework analizy danych, które można wykonać przez osobę.</span><span class="sxs-lookup"><span data-stu-id="53058-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="53058-113">Możemy przeanalizować hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) zestawu danych w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="53058-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="53058-114">Jest to zestaw wiadomości e-mail, które są oznaczone jako wiadomości-śmieci lub pichcisz (tzn. nie są one spamu), i zawiera także statystykami dotyczącymi zawartości hello hello wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="53058-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="53058-115">statystyki Hello uwzględnione omówiono hello obok ale jedną sekcję.</span><span class="sxs-lookup"><span data-stu-id="53058-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53058-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="53058-116">Prerequisites</span></span>
<span data-ttu-id="53058-117">Przed użyciem maszyny wirtualnej systemu Linux danych nauki, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="53058-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="53058-118">**Subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="53058-118">An **Azure subscription**.</span></span> <span data-ttu-id="53058-119">Jeśli nie masz już jeden, zobacz [utworzyć bezpłatne konto platformy Azure obecnie](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="53058-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="53058-120">A [ **nauki danych Linux VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="53058-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="53058-121">Aby uzyskać informacje o inicjowaniu obsługi tej maszyny Wirtualnej, zobacz [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="53058-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="53058-122">[X2Go](http://wiki.x2go.org/doku.php) zainstalowany na tym komputerze i otworzyć sesję XFCE.</span><span class="sxs-lookup"><span data-stu-id="53058-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="53058-123">Aby uzyskać informacje o instalowaniu i konfigurowaniu **klienta X2Go**, zobacz [Instalowanie i konfigurowanie klienta X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="53058-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="53058-124">**Konta uczenie maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="53058-124">An **AzureML account**.</span></span> <span data-ttu-id="53058-125">Jeśli nie masz jeszcze jeden Załóż nowe hasło w hello [strony głównej uczenie maszynowe Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="53058-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="53058-126">Brak toohelp warstwy bezpłatna użycia, możesz rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="53058-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="53058-127">Pobierz zestaw hello spambase danych</span><span class="sxs-lookup"><span data-stu-id="53058-127">Download hello spambase dataset</span></span>
<span data-ttu-id="53058-128">Witaj [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) zestaw danych jest stosunkowo mały zestaw danych, który zawiera tylko 4601 przykłady.</span><span class="sxs-lookup"><span data-stu-id="53058-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="53058-129">Jest to toouse rozmiarów wykazać, że niektóre główne funkcje hello hello wirtualna analizy danych, ponieważ utrzymuje wymagań dotyczących zasobów hello niewielkie.</span><span class="sxs-lookup"><span data-stu-id="53058-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-130">Ten przewodnik został utworzony na D2 rozmiar v2 danych nauki maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="53058-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="53058-131">Ten rozmiar jest w stanie obsługiwać hello procedur w tym przewodniku DSVM.</span><span class="sxs-lookup"><span data-stu-id="53058-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="53058-132">Jeśli potrzebujesz więcej miejsca w magazynie, można tworzyć dodatkowe dyski i dołącz je tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53058-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="53058-133">Te dyski używać trwałego magazynu Azure, dlatego ich dane zostaną zachowane nawet wtedy, gdy jest ponownie udostępnić powitania serwera z powodu tooresizing lub jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="53058-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="53058-134">tooadd dysku i dołącz je tooyour maszyny Wirtualnej, wykonaj te instrukcje hello [dodać tooa dysku maszyny Wirtualnej systemu Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53058-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="53058-135">Kroki przy użyciu interfejsu wiersza polecenia platformy Azure (Azure CLI), który jest już zainstalowany na powitania DSVM hello.</span><span class="sxs-lookup"><span data-stu-id="53058-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="53058-136">Dlatego te procedury może odbywać się wyłącznie z hello samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53058-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="53058-137">Inną opcją tooincrease magazynu jest toouse [pliki Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="53058-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="53058-138">toodownload hello danych, Otwórz okno terminalu i uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="53058-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="53058-139">Witaj pobrany plik nie ma wiersz nagłówka, więc warto utworzyć innego pliku, który ma nagłówka.</span><span class="sxs-lookup"><span data-stu-id="53058-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="53058-140">Uruchom plik toocreate tego polecenia, z nagłówkami odpowiednie hello:</span><span class="sxs-lookup"><span data-stu-id="53058-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="53058-141">Następnie połącz hello dwa pliki z poleceniem hello:</span><span class="sxs-lookup"><span data-stu-id="53058-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="53058-142">Witaj dataset zawiera kilka typów statystyk w każdej wiadomości e-mail:</span><span class="sxs-lookup"><span data-stu-id="53058-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="53058-143">Kolumn, takich jak ***word\_Częst\_WORD*** wskazuje procent hello w wiadomości e-mail hello wyrazy, które odpowiadają *WORD*.</span><span class="sxs-lookup"><span data-stu-id="53058-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="53058-144">Na przykład jeśli *word\_Częst\_upewnij* ma wartość 1, a następnie zostały 1% wszystkich wyrazów w wiadomości e-mail hello *upewnij*.</span><span class="sxs-lookup"><span data-stu-id="53058-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="53058-145">Kolumn, takich jak ***char\_Częst\_CHAR*** wskazuje procent hello wszystkich znaków w wiadomości e-mail hello, które były *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="53058-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="53058-146">***kapitału\_Uruchom\_długość\_najdłuższym*** jest hello najdłuższy okres sekwencję wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="53058-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="53058-147">***kapitału\_Uruchom\_długość\_średni*** jest średnią długość hello wszystkich sekwencji wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="53058-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="53058-148">***kapitału\_Uruchom\_długość\_całkowita*** jest hello łączna długość wszystkich sekwencji wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="53058-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="53058-149">***spamu*** wskazuje, czy hello e-mail został uznany za spam, lub nie (1 = wiadomości-śmieci, 0 = nie spamu).</span><span class="sxs-lookup"><span data-stu-id="53058-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="53058-150">Eksploruj hello zestawu danych otwórz R firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="53058-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="53058-151">Teraz zbadać hello danych i wykonaj niektórych uczenia maszynowego podstawowe z hello R. wirtualna nauki danych jest dostarczany z [Microsoft R Otwórz](https://mran.revolutionanalytics.com/open/) wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="53058-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="53058-152">Hello bibliotek wielowątkowych matematyczne w tej wersji R oferuje lepszą wydajność niż w różnych wersjach jednowątkowy.</span><span class="sxs-lookup"><span data-stu-id="53058-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="53058-153">Otwórz R firmy Microsoft są także powtarzalności przy użyciu migawek z repozytorium pakietów hello sieci CRAN.</span><span class="sxs-lookup"><span data-stu-id="53058-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="53058-154">kopie tooget hello kodu próbek używanych w tym przewodniku hello w klonowania **Azure-maszyny-Learning-danych-nauki** repozytorium przy użyciu usługi git, który jest wstępnie zainstalowane na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53058-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="53058-155">Z wiersza polecenia git hello Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="53058-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="53058-156">Otwórz okno terminala i rozpocznij nową sesję R z konsolą interakcyjne hello R.</span><span class="sxs-lookup"><span data-stu-id="53058-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-157">Umożliwia także programu RStudio dla hello zgodnie z procedurami.</span><span class="sxs-lookup"><span data-stu-id="53058-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="53058-158">tooinstall programu RStudio, wykonanie tego polecenia w terminalu:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="53058-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="53058-159">Uruchom tooimport hello danych i skonfigurować środowisko hello:</span><span class="sxs-lookup"><span data-stu-id="53058-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="53058-160">toosee podsumowania statystyk dotyczących poszczególnych kolumn:</span><span class="sxs-lookup"><span data-stu-id="53058-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="53058-161">Do innego widoku danych hello:</span><span class="sxs-lookup"><span data-stu-id="53058-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="53058-162">Oznacza to, hello typu każdej zmiennej i hello najpierw kilka wartości hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="53058-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="53058-163">Witaj *spamu* kolumna została odczytana jako liczba całkowita, ale jest rzeczywiście kategorii zmiennej (lub współczynnik).</span><span class="sxs-lookup"><span data-stu-id="53058-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="53058-164">tooset jej typ:</span><span class="sxs-lookup"><span data-stu-id="53058-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="53058-165">toodo niektóre poznawcze analizy, użyj hello [ggplot2](http://ggplot2.org/) pakietu popularnych biblioteki graficznych dla języka R, która jest już zainstalowana na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53058-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="53058-166">Uwaga: z danych podsumowania hello wyświetlane wcześniej, będziemy mieć podsumowania statystyk od częstotliwości hello hello wykrzyknik znaku.</span><span class="sxs-lookup"><span data-stu-id="53058-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="53058-167">Załóżmy wykreślenia tych częstotliwości tutaj z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53058-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="53058-168">Ponieważ pasek hello zero pochylenie kreślenia hello umożliwia pozbyć się go:</span><span class="sxs-lookup"><span data-stu-id="53058-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="53058-169">Brak nieuproszczony gęstości powyżej 1, która wygląda interesujące.</span><span class="sxs-lookup"><span data-stu-id="53058-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="53058-170">Przyjrzyjmy się tylko te dane:</span><span class="sxs-lookup"><span data-stu-id="53058-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="53058-171">Następnie podziel go przez pichcisz vs spamu:</span><span class="sxs-lookup"><span data-stu-id="53058-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="53058-172">Te przykłady należy włączyć, należy toomake podobne wykresy hello tooexplore innych kolumn hello dane zawarte w nich.</span><span class="sxs-lookup"><span data-stu-id="53058-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="53058-173">Nauczenia i przetestowania modelu usługi uczenie Maszynowe</span><span class="sxs-lookup"><span data-stu-id="53058-173">Train and test an ML model</span></span>
<span data-ttu-id="53058-174">Teraz załóżmy train kilka uczenia maszynowego modele tooclassify wiadomości powitania w zestawie danych hello jako zawierające albo span lub pichcisz.</span><span class="sxs-lookup"><span data-stu-id="53058-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="53058-175">Firma Microsoft train model drzewa decyzyjnego i model lasu losowe w tej sekcji, a następnie sprawdź ich dokładność ich prognoz.</span><span class="sxs-lookup"><span data-stu-id="53058-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-176">Witaj rpart (cykliczne partycjonowania i drzew regresji) pakietu używane w hello następującego kodu jest już zainstalowana na powitania wirtualna analizy danych.</span><span class="sxs-lookup"><span data-stu-id="53058-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="53058-177">Po pierwsze możemy podzielić zestawu danych hello w zestawy szkoleniowe i testu:</span><span class="sxs-lookup"><span data-stu-id="53058-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="53058-178">A następnie utworzyć hello tooclassify drzewa decyzyjnego wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="53058-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="53058-179">W tym miejscu jest wynikiem hello:</span><span class="sxs-lookup"><span data-stu-id="53058-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="53058-181">jak wykonuje szkolenia hello toodetermine ustawić, użyj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="53058-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="53058-182">jak dobrze toodetermine wykonuje na powitania zestawu testowego:</span><span class="sxs-lookup"><span data-stu-id="53058-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="53058-183">Spróbujmy również modelu losowe lasu.</span><span class="sxs-lookup"><span data-stu-id="53058-183">Let's also try a random forest model.</span></span> <span data-ttu-id="53058-184">Losowe lasów wiele algorytmów uczenia i wyjściowych klasę, która jest tryb hello hello klasyfikacje ze wszystkich hello poszczególnych algorytmów.</span><span class="sxs-lookup"><span data-stu-id="53058-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="53058-185">Udostępniają one bardziej wydajny komputer uczenia podejście, jak Usuń hello tendencję decyzji toooverfit modelu drzewa zestawu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="53058-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="53058-186">Wdrażanie tooAzure modelu uczenia Maszynowego</span><span class="sxs-lookup"><span data-stu-id="53058-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="53058-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (uczenie maszynowe Azure) to usługa w chmurze, który umożliwia łatwe toobuild i wdrażanie modeli analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="53058-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="53058-188">Jedną z funkcji nieuprzywilejowany hello uczenie maszynowe Azure jest jego toopublish możliwości żadnych R działać jako usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="53058-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="53058-189">Witaj pakietu języka R uczenie maszynowe Azure nawiązuje toodo łatwe wdrożenia bezpośrednio z naszych sesji R hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="53058-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="53058-190">drzewa decyzyjne kodu toodeploy hello z poprzedniej sekcji hello należy toosign w tooAzure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="53058-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="53058-191">Należy identyfikator obszaru roboczego i toosign token autoryzacji w.</span><span class="sxs-lookup"><span data-stu-id="53058-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="53058-192">toofind te wartości i zainicjować hello uczenie maszynowe Azure zmiennych z nimi:</span><span class="sxs-lookup"><span data-stu-id="53058-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="53058-193">Wybierz **ustawienia** na powitania menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="53058-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="53058-194">Uwaga użytkownika **identyfikator obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="53058-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="53058-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="53058-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="53058-196">Wybierz **tokeny autoryzacji** z menu narzutów hello i notatki z **podstawowego tokenu autoryzacji**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="53058-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="53058-197">Witaj obciążenia **uczenie maszynowe Azure** pakietu, a następnie ustaw wartości zmiennych hello za pomocą Identyfikatora tokenu i obszar roboczy w sesji R na powitania DSVM:</span><span class="sxs-lookup"><span data-stu-id="53058-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="53058-198">Odrobinę uprościmy badane toomake modelu hello tego pokazu tooimplement łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="53058-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="53058-199">Wybierz hello trzy zmienne w hello decyzji najbliższego toohello katalogu głównego drzewa i utworzyć nowe drzewo przy użyciu tylko tych trzech zmiennych:</span><span class="sxs-lookup"><span data-stu-id="53058-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="53058-200">Potrzebujemy, funkcja prognozowania, która przyjmuje jako dane wejściowe funkcji hello i zwraca hello przewidywane wartości:</span><span class="sxs-lookup"><span data-stu-id="53058-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="53058-201">Publikowanie tooAzureML funkcja predictSpam hello przy użyciu hello **publishWebService** funkcji:</span><span class="sxs-lookup"><span data-stu-id="53058-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="53058-202">Ta funkcja przyjmuje hello **predictSpam** funkcji, tworzy usługi sieci web o nazwie **spamWebService** z zdefiniowane wejściach i wyjściach i zwraca informacje na temat hello nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="53058-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="53058-203">Wyświetl szczegóły hello opublikować usługi sieci web, w tym jego klucze interfejsu API punktu końcowego i dostęp za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="53058-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="53058-204">tootry hello go na pierwszych 10 wierszy hello zestawu testów:</span><span class="sxs-lookup"><span data-stu-id="53058-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="53058-205">Użyj innych dostępnych narzędzi</span><span class="sxs-lookup"><span data-stu-id="53058-205">Use other tools available</span></span>
<span data-ttu-id="53058-206">Witaj pozostałe sekcje pokazują, jak toouse niektóre narzędzia hello zainstalowane na hello maszyny Wirtualnej systemu Linux danych nauki. Poniżej znajduje się lista hello narzędzia opisem:</span><span class="sxs-lookup"><span data-stu-id="53058-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="53058-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="53058-207">XGBoost</span></span>
* <span data-ttu-id="53058-208">Python</span><span class="sxs-lookup"><span data-stu-id="53058-208">Python</span></span>
* <span data-ttu-id="53058-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="53058-209">Jupyterhub</span></span>
* <span data-ttu-id="53058-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="53058-210">Rattle</span></span>
* <span data-ttu-id="53058-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="53058-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="53058-212">Magazyn danych serwera SQL Server</span><span class="sxs-lookup"><span data-stu-id="53058-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="53058-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="53058-213">XGBoost</span></span>
<span data-ttu-id="53058-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) to narzędzie, które udostępnia implementację szybkich i dokładnych boosted drzewa.</span><span class="sxs-lookup"><span data-stu-id="53058-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="53058-215">XGBoost można również wywołać z języka python lub wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="53058-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="53058-216">Python</span><span class="sxs-lookup"><span data-stu-id="53058-216">Python</span></span>
<span data-ttu-id="53058-217">Do tworzenia aplikacji przy użyciu języka Python zostały zainstalowane w hello DSVM hello Anaconda Python dystrybucje 2.7 i 3.5.</span><span class="sxs-lookup"><span data-stu-id="53058-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-218">obejmuje Hello dystrybucji Anaconda [Condas](http://conda.pydata.org/docs/index.html), które mogą być używane toocreate niestandardowego środowiska dla języka Python, które mają różne wersje i/lub pakietów zainstalowanych w nich.</span><span class="sxs-lookup"><span data-stu-id="53058-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="53058-219">Umożliwia odczytu w niektórych hello spambase dataset i klasyfikowania wiadomości powitania maszynom wektorowa obsługa w scikit — Dowiedz się więcej:</span><span class="sxs-lookup"><span data-stu-id="53058-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="53058-220">operacje przewidywania dla toomake:</span><span class="sxs-lookup"><span data-stu-id="53058-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="53058-221">tooshow jak toopublish punkt końcowy uczenie maszynowe Azure umożliwia łatwiejsze modelu upewnij hello trzy zmienne jako robiliśmy po opublikowaniu firma Microsoft hello R modelu wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53058-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="53058-222">toopublish tooAzureML modelu hello:</span><span class="sxs-lookup"><span data-stu-id="53058-222">toopublish hello model tooAzureML:</span></span>

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="53058-223">To jest dostępne tylko dla języka python 2.7 i nie jest jeszcze obsługiwana w 3.5.</span><span class="sxs-lookup"><span data-stu-id="53058-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="53058-224">Uruchom z **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="53058-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="53058-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="53058-225">Jupyterhub</span></span>
<span data-ttu-id="53058-226">Witaj Anaconda dystrybucji w hello DSVM jest dostarczany z notesu Jupyter, kod języka Python, R lub Julia tooshare środowiska i platform i analizy.</span><span class="sxs-lookup"><span data-stu-id="53058-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="53058-227">notesu Jupyter Hello jest dostępny za pośrednictwem JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="53058-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="53058-228">Zaloguj się przy użyciu lokalnego nazwę użytkownika systemu Linux i hasło na ***https://\<nazwę DNS maszyny Wirtualnej lub adres IP\>: 8000 /***.</span><span class="sxs-lookup"><span data-stu-id="53058-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="53058-229">Wszystkie pliki konfiguracji dla JupyterHub znajdują się w katalogu **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="53058-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="53058-230">Kilka przykładowych notesów są już zainstalowane na powitania maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="53058-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="53058-231">Zobacz hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) notesu Python próbki.</span><span class="sxs-lookup"><span data-stu-id="53058-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="53058-232">Zobacz [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) przykładowe **R** notesu.</span><span class="sxs-lookup"><span data-stu-id="53058-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="53058-233">Zobacz hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) dla innej próbki **Python** notesu.</span><span class="sxs-lookup"><span data-stu-id="53058-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-234">Witaj Julia języka jest również dostępna z wiersza polecenia hello na powitania maszyny Wirtualnej systemu Linux danych nauki.</span><span class="sxs-lookup"><span data-stu-id="53058-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="53058-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="53058-235">Rattle</span></span>
<span data-ttu-id="53058-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (łatwo hello tooLearn narzędzie analityczne R) jest narzędziem graficznym R do wyszukiwania danych.</span><span class="sxs-lookup"><span data-stu-id="53058-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="53058-237">Ma ona intuicyjny interfejs, który umożliwia łatwe tooload, Eksploruj i przekształcania danych i tworzenie i oceny modeli.</span><span class="sxs-lookup"><span data-stu-id="53058-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="53058-238">Artykuł Hello [Rattle: A danych wyszukiwania graficznego interfejsu użytkownika dla R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) zawiera wskazówki, który demonstruje jego funkcje.</span><span class="sxs-lookup"><span data-stu-id="53058-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="53058-239">Zainstaluj i uruchom Rattle z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53058-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="53058-240">Instalacja nie jest wymagana na powitania DSVM.</span><span class="sxs-lookup"><span data-stu-id="53058-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="53058-241">Ale Rattle może monitować dodatkowe pakiety tooinstall podczas jego ładowania.</span><span class="sxs-lookup"><span data-stu-id="53058-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="53058-242">Rattle używa interfejsu oparte na karcie.</span><span class="sxs-lookup"><span data-stu-id="53058-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="53058-243">Większość kart hello odpowiada toosteps w hello [proces nauki danych](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), takie jak ładowanie danych lub jej eksplorację.</span><span class="sxs-lookup"><span data-stu-id="53058-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="53058-244">proces nauki danych Hello wypływających z lewym tooright przez hello karty.</span><span class="sxs-lookup"><span data-stu-id="53058-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="53058-245">Ale hello ostatniej karty zawiera dziennik uruchamiając Rattle poleceń hello R.</span><span class="sxs-lookup"><span data-stu-id="53058-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="53058-246">tooload i skonfigurować hello zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="53058-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="53058-247">Plik hello tooload, wybierz opcję hello **danych** karcie następnie</span><span class="sxs-lookup"><span data-stu-id="53058-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="53058-248">Wybierz opcję selektora hello dalej zbyt**Filename** i wybierz polecenie **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="53058-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="53058-249">Plik hello tooload.</span><span class="sxs-lookup"><span data-stu-id="53058-249">tooload hello file.</span></span> <span data-ttu-id="53058-250">Wybierz **Execute** w hello najwyższego rzędu przycisków.</span><span class="sxs-lookup"><span data-stu-id="53058-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="53058-251">Powinny pojawić się podsumowanie każdej kolumny, w tym jego typu danych zidentyfikowanych, czy dane wejściowe, cel lub innego typu zmienną i hello liczbę unikatowych wartości.</span><span class="sxs-lookup"><span data-stu-id="53058-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="53058-252">Rattle poprawnie identyfikuje hello **spamu** kolumny jako cel hello.</span><span class="sxs-lookup"><span data-stu-id="53058-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="53058-253">Wybierz hello spamu kolumny, a następnie hello zestaw **docelowy typ danych** za**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="53058-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="53058-254">dane hello tooexplore:</span><span class="sxs-lookup"><span data-stu-id="53058-254">tooexplore hello data:</span></span>

* <span data-ttu-id="53058-255">Wybierz hello **Eksploruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="53058-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="53058-256">Kliknij przycisk **podsumowania**, następnie **Execute**, toosee niektóre informacje na temat typów zmiennych hello i niektórych podsumowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="53058-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="53058-257">tooview innych typów danych statystycznych dotyczących każdej zmiennej, wybierz inne opcje, takie jak **Opisz** lub **podstawy**.</span><span class="sxs-lookup"><span data-stu-id="53058-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="53058-258">Witaj **Eksploruj** kartę można też toogenerate wiele interesującego geograficzne.</span><span class="sxs-lookup"><span data-stu-id="53058-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="53058-259">tooplot histogram hello danych:</span><span class="sxs-lookup"><span data-stu-id="53058-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="53058-260">Wybierz **dystrybucje**.</span><span class="sxs-lookup"><span data-stu-id="53058-260">Select **Distributions**.</span></span>
* <span data-ttu-id="53058-261">Sprawdź **Histogram** dla **word_freq_remove** i **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="53058-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="53058-262">Wybierz **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="53058-262">Select **Execute**.</span></span> <span data-ttu-id="53058-263">Powinny pojawić się, że oba gęstość geograficzne w oknie pojedynczego wykresu, jeżeli jest jasne wyrazie hello częściej pojawia się "musisz" wiadomości e-mail niż "Usuń".</span><span class="sxs-lookup"><span data-stu-id="53058-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="53058-264">krzywe korelacji Hello są również interesujące.</span><span class="sxs-lookup"><span data-stu-id="53058-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="53058-265">toocreate co:</span><span class="sxs-lookup"><span data-stu-id="53058-265">toocreate one:</span></span>

* <span data-ttu-id="53058-266">Wybierz **korelacji** jako hello **typu**, następnie</span><span class="sxs-lookup"><span data-stu-id="53058-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="53058-267">Wybierz **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="53058-267">Select **Execute**.</span></span>
* <span data-ttu-id="53058-268">Rattle wyświetli ostrzeżenie, że zaleca maksymalnie 40 zmiennych.</span><span class="sxs-lookup"><span data-stu-id="53058-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="53058-269">Wybierz **tak** tooview hello kreślenia.</span><span class="sxs-lookup"><span data-stu-id="53058-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="53058-270">Istnieją pewne interesujące korelacji, które znaleziona: "technologii" silnie skorelowane zbyt "HP" i "laboratoria", na przykład.</span><span class="sxs-lookup"><span data-stu-id="53058-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="53058-271">Ponadto jest skorelowany zbyt "650", ponieważ kod obszaru hello dawcy dataset hello jest 650.</span><span class="sxs-lookup"><span data-stu-id="53058-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="53058-272">Hello wartości liczbowych hello korelacji między wyrazami są dostępne w oknie Eksploruj hello.</span><span class="sxs-lookup"><span data-stu-id="53058-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="53058-273">Jest interesujące toonote, na przykład, że "technologii" negatywnie są skorelowane z "UR" i "cenę".</span><span class="sxs-lookup"><span data-stu-id="53058-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="53058-274">Rattle można przekształcać hello dataset toohandle niektórych typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="53058-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="53058-275">Na przykład można funkcje toorescale, przypisują brakujące wartości obsługi wartości odstających i Usuń zmienne lub uwagi z brakującymi danymi.</span><span class="sxs-lookup"><span data-stu-id="53058-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="53058-276">Rattle mogą też wskazać reguły skojarzenia między uwag i/lub zmienne.</span><span class="sxs-lookup"><span data-stu-id="53058-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="53058-277">Te karty wykraczają poza zakres tego przewodnika wstępne.</span><span class="sxs-lookup"><span data-stu-id="53058-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="53058-278">Rattle można również wykonywać analizy klastra.</span><span class="sxs-lookup"><span data-stu-id="53058-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="53058-279">Umożliwia wykluczenie niektórych funkcji toomake hello dane wyjściowe łatwiejsze tooread.</span><span class="sxs-lookup"><span data-stu-id="53058-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="53058-280">Na powitania **danych** , wybierz pozycję **Ignoruj** dalej tooeach hello zmiennych z wyjątkiem tych pozycji 10:</span><span class="sxs-lookup"><span data-stu-id="53058-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="53058-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="53058-281">word_freq_hp</span></span>
* <span data-ttu-id="53058-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="53058-282">word_freq_technology</span></span>
* <span data-ttu-id="53058-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="53058-283">word_freq_george</span></span>
* <span data-ttu-id="53058-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="53058-284">word_freq_remove</span></span>
* <span data-ttu-id="53058-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="53058-285">word_freq_your</span></span>
* <span data-ttu-id="53058-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="53058-286">word_freq_dollar</span></span>
* <span data-ttu-id="53058-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="53058-287">word_freq_money</span></span>
* <span data-ttu-id="53058-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="53058-288">capital_run_length_longest</span></span>
* <span data-ttu-id="53058-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="53058-289">word_freq_business</span></span>
* <span data-ttu-id="53058-290">spamu</span><span class="sxs-lookup"><span data-stu-id="53058-290">spam</span></span>

<span data-ttu-id="53058-291">Następnie wróć toohello **klastra** , wybierz pozycję **KMeans**i ustaw hello *liczby klastrów* too4.</span><span class="sxs-lookup"><span data-stu-id="53058-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="53058-292">Następnie **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="53058-292">Then **Execute**.</span></span> <span data-ttu-id="53058-293">w oknie danych wyjściowych hello są wyświetlane wyniki Hello.</span><span class="sxs-lookup"><span data-stu-id="53058-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="53058-294">Jeden klaster ma wysoką częstotliwość "george" i "hp" i prawdopodobnie jest uzasadnione służbowy adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="53058-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="53058-295">toobuild modelu uczenia maszynowego drzewa proste decyzji:</span><span class="sxs-lookup"><span data-stu-id="53058-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="53058-296">Wybierz hello **modelu** karcie</span><span class="sxs-lookup"><span data-stu-id="53058-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="53058-297">Wybierz **drzewa** jako hello **typu**.</span><span class="sxs-lookup"><span data-stu-id="53058-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="53058-298">Wybierz **Execute** toodisplay hello drzewa w postaci tekstu w hello okna wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="53058-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="53058-299">Wybierz hello **rysowania** tooview przycisk graficzny wersji.</span><span class="sxs-lookup"><span data-stu-id="53058-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="53058-300">Wygląda ona podobna drzewa toohello możemy uzyskany wcześniej przy użyciu *rpart*.</span><span class="sxs-lookup"><span data-stu-id="53058-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="53058-301">Jedną z funkcji nieuprzywilejowany hello Rattle jest jego możliwości toorun metody kilka uczenia maszynowego i szybko ich oceny.</span><span class="sxs-lookup"><span data-stu-id="53058-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="53058-302">Poniżej przedstawiono procedurę hello:</span><span class="sxs-lookup"><span data-stu-id="53058-302">Here is hello procedure:</span></span>

* <span data-ttu-id="53058-303">Wybierz **wszystkie** dla hello **typu**.</span><span class="sxs-lookup"><span data-stu-id="53058-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="53058-304">Wybierz **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="53058-304">Select **Execute**.</span></span>
* <span data-ttu-id="53058-305">Po zakończeniu kliknięcie dowolnego pojedynczego **typu**, takiej jak **SVM**i wyświetlić wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="53058-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="53058-306">Można także porównać wydajności hello modeli hello weryfikacji hello ustawić za pomocą hello **Evaluate** kartę. Na przykład Witaj **macierzy błąd** zaznaczenie zawiera macierz pomyłek hello, ogólny błąd i błąd uśrednionej klasy dla każdego modelu hello sprawdzania poprawności zestawu.</span><span class="sxs-lookup"><span data-stu-id="53058-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="53058-307">Można również wykreślenia krzywych ROC, analiza czułości i czy innych typów oceny modelu.</span><span class="sxs-lookup"><span data-stu-id="53058-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="53058-308">Po zakończeniu budowania modeli wybierz hello **dziennika** karcie tooview hello R kodu przez Rattle podczas sesji.</span><span class="sxs-lookup"><span data-stu-id="53058-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="53058-309">Możesz wybrać hello **wyeksportować** toosave przycisk go.</span><span class="sxs-lookup"><span data-stu-id="53058-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="53058-310">Jest to błąd w bieżącej wersji Rattle.</span><span class="sxs-lookup"><span data-stu-id="53058-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="53058-311">toomodify hello skryptu lub użyć toorepeat etapów później, należy wstawić przed znak # * wyeksportować ten dziennik... * w tekście hello hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="53058-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="53058-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="53058-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="53058-313">Witaj DSVM jest dostarczany z PostgreSQL zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="53058-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="53058-314">PostgreSQL jest złożone, open source relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="53058-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="53058-315">W tej sekcji przedstawiono sposób tooload naszych spamu zestawu danych do PostgreSQL, a następnie wykonasz zapytania.</span><span class="sxs-lookup"><span data-stu-id="53058-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="53058-316">Przed załadowaniem danych hello należy tooallow uwierzytelniania hasła z hello localhost.</span><span class="sxs-lookup"><span data-stu-id="53058-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="53058-317">W wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="53058-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="53058-318">Dolnej hello pliku konfiguracyjnego hello są kilka wierszy, które zawierają hello dozwolone połączenia:</span><span class="sxs-lookup"><span data-stu-id="53058-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="53058-319">Zmień hello "Lokalnych połączeń IPv4" wiersza toouse md5 zamiast ident, aby firma Microsoft może logować się przy użyciu nazwy użytkownika i hasła:</span><span class="sxs-lookup"><span data-stu-id="53058-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="53058-320">I ponownie uruchom usługę postgres hello:</span><span class="sxs-lookup"><span data-stu-id="53058-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="53058-321">psql toolaunch, terminalu interactive PostgreSQL jako użytkownik wbudowanych postgres hello, uruchom następujące polecenie w wierszu hello:</span><span class="sxs-lookup"><span data-stu-id="53058-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="53058-322">Utwórz nowe konto użytkownika, za pomocą hello tej samej nazwy użytkownika, jak hello konta systemu Linux, który jest obecnie zalogowany jako i nadaj mu hasło:</span><span class="sxs-lookup"><span data-stu-id="53058-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="53058-323">Następnie zaloguj się toopsql jako użytkownika:</span><span class="sxs-lookup"><span data-stu-id="53058-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="53058-324">I zaimportuj dane hello do nowej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="53058-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="53058-325">Teraz załóżmy Eksplorowanie danych hello i uruchom kilka zapytań przy użyciu **Squirrel SQL**, graficzne narzędzie, które umożliwia interakcję z bazami danych za pośrednictwem sterownik JDBC.</span><span class="sxs-lookup"><span data-stu-id="53058-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="53058-326">Rozpoczęto tooget, uruchomić Squirrel SQL z menu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="53058-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="53058-327">tooset zapasową sterownika hello:</span><span class="sxs-lookup"><span data-stu-id="53058-327">tooset up hello driver:</span></span>

* <span data-ttu-id="53058-328">Wybierz **Windows**, następnie **Wyświetl sterowniki**.</span><span class="sxs-lookup"><span data-stu-id="53058-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="53058-329">Kliknij prawym przyciskiem myszy **PostgreSQL** i wybierz **zmodyfikować sterownika**.</span><span class="sxs-lookup"><span data-stu-id="53058-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="53058-330">Wybierz **bardzo klasy ścieżki**, następnie **dodać**.</span><span class="sxs-lookup"><span data-stu-id="53058-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="53058-331">Wprowadź ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** dla hello **nazwę pliku** i</span><span class="sxs-lookup"><span data-stu-id="53058-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="53058-332">Wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="53058-332">Select **Open**.</span></span>
* <span data-ttu-id="53058-333">Wybierz z listy sterowniki, a następnie wybierz **org.postgresql.Driver** w **Nazwa klasy**i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="53058-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="53058-334">tooset hello połączenia toohello lokalnego serwera:</span><span class="sxs-lookup"><span data-stu-id="53058-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="53058-335">Wybierz **Windows**, następnie **wyświetlić aliasy.**</span><span class="sxs-lookup"><span data-stu-id="53058-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="53058-336">Wybierz hello  **+**  toomake przycisk Nowy alias.</span><span class="sxs-lookup"><span data-stu-id="53058-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="53058-337">Nadaj mu nazwę *bazy danych spamu*, wybierz **PostgreSQL** w hello **sterownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="53058-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="53058-338">Ustaw adres URL hello zbyt*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="53058-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="53058-339">Wprowadź użytkownika *username* i *hasło*.</span><span class="sxs-lookup"><span data-stu-id="53058-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="53058-340">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="53058-340">Click **OK**.</span></span>
* <span data-ttu-id="53058-341">Witaj tooopen **połączenia** okna, kliknij dwukrotnie hello ***spamu bazy danych*** alias.</span><span class="sxs-lookup"><span data-stu-id="53058-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="53058-342">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="53058-342">Select **Connect**.</span></span>

<span data-ttu-id="53058-343">toorun niektóre kwerendy:</span><span class="sxs-lookup"><span data-stu-id="53058-343">toorun some queries:</span></span>

* <span data-ttu-id="53058-344">Wybierz hello **SQL** kartę.</span><span class="sxs-lookup"><span data-stu-id="53058-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="53058-345">Wprowadź na przykład prostego zapytania `SELECT * from data;` w polu tekstowym kwerendy hello u góry hello hello SQL karty.</span><span class="sxs-lookup"><span data-stu-id="53058-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="53058-346">Naciśnij klawisz **Wprowadź Ctrl** toorun go.</span><span class="sxs-lookup"><span data-stu-id="53058-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="53058-347">Domyślnie Squirrel SQL zwraca hello pierwszych 100 wierszy z zapytania.</span><span class="sxs-lookup"><span data-stu-id="53058-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="53058-348">Istnieje wiele zapytań więcej tooexplore można uruchomić te dane.</span><span class="sxs-lookup"><span data-stu-id="53058-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="53058-349">Na przykład, jak hello częstotliwość hello word *upewnij* różnią się spamem i pichcisz?</span><span class="sxs-lookup"><span data-stu-id="53058-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="53058-350">Lub co to są właściwości hello poczty e-mail, które często zawierają *3d*?</span><span class="sxs-lookup"><span data-stu-id="53058-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="53058-351">Większość wiadomości e-mail, które mają wysokie wystąpienie *3d* są najwyraźniej wysyłania spamu, dlatego może być przydatne do tworzenia hello tooclassify model predykcyjny wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="53058-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="53058-352">Jeśli potrzebujesz uczenia maszynowego tooperform dane przechowywane w bazie danych programu PostgreSQL, rozważ użycie [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="53058-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="53058-353">Magazyn danych serwera SQL Server</span><span class="sxs-lookup"><span data-stu-id="53058-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="53058-354">Azure SQL Data Warehouse to oparta na chmurze i skalowalna w poziomie baza danych, która może przetwarzać ogromne ilości danych relacyjnych i nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="53058-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="53058-355">Aby uzyskać więcej informacji, zobacz [co to jest Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="53058-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="53058-356">dane toohello tooconnect magazynu i tworzenie tabeli hello hello uruchom następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="53058-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="53058-357">Następnie w wierszu sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="53058-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="53058-358">Kopiowanie danych za pomocą narzędzia bcp:</span><span class="sxs-lookup"><span data-stu-id="53058-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="53058-359">zakończenia wierszy Hello w pobrany plik hello są styl systemu Windows, ale bcp oczekuje typu UNIX, potrzebujemy bcp tootell, że w programie hello flagi - r.</span><span class="sxs-lookup"><span data-stu-id="53058-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="53058-360">I zapytania przy użyciu narzędzia sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="53058-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="53058-361">Można także zbadać z Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="53058-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="53058-362">Należy wykonać podobne kroki w przypadku PostgreSQL hello sterownik JDBC serwera MSSQL firmy Microsoft, za pomocą której można znaleźć w ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="53058-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53058-363">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53058-363">Next steps</span></span>
<span data-ttu-id="53058-364">Omówienie tematów, które umożliwia przeprowadzenie zadań hello, wchodzące w skład procesu nauki danych hello na platformie Azure, zobacz [proces nauki danych zespołu](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="53058-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="53058-365">Opis innych end-to-end wskazówki, które pokazują hello kroki hello proces nauki danych zespołu dla konkretnych scenariuszy, zobacz [wskazówki dotyczące procesu nauki danych zespołu](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="53058-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="53058-366">wskazówki dotyczące Hello również ilustrują sposób toocombine w chmurze i lokalnie narzędzia i usługi do toocreate przepływu pracy lub potoku inteligentnego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53058-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
