---
title: "Samouczek aaaQuickstart dla języka R Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj tego R programowania samouczek tooget uruchomiona szybko przy użyciu języka hello R w usłudze Azure Machine Learning Studio toocreate prognozowania rozwiązania."
keywords: "Szybki Start, języka r, r język programowania, samouczek programowania r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="5b433-104">Samouczek szybki start dotyczący hello R język programowania dla usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b433-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="5b433-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="5b433-105">Introduction</span></span>
<span data-ttu-id="5b433-106">Ten samouczek Szybki Start pomaga szybko rozpocząć rozszerzanie uczenia maszynowego Azure przy użyciu języka programowania hello R.</span><span class="sxs-lookup"><span data-stu-id="5b433-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="5b433-107">Postępuj zgodnie z tym R programowania toocreate samouczek, przetestować i wykonanie kodu języka R w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5b433-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="5b433-108">Podczas pracy z samouczkiem utworzysz kompletnego rozwiązania prognozowania przy użyciu języka hello R w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5b433-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="5b433-109">Microsoft Azure Machine Learning zawiera wiele modułów wydajny komputer uczenie i danych manipulowanie.</span><span class="sxs-lookup"><span data-stu-id="5b433-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="5b433-110">Hello zaawansowanych język R został opisany jako franca język hello analizy.</span><span class="sxs-lookup"><span data-stu-id="5b433-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="5b433-111">Happily manipulowanie analizy i danych w usłudze Azure Machine Learning można rozszerzyć za pomocą R. Ta kombinacja zapewnia hello skalowalność i łatwość wdrażania usługi Azure Machine Learning hello elastyczność i analiza głębokie r.</span><span class="sxs-lookup"><span data-stu-id="5b433-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="5b433-112">Prognozowanie i hello zestawu danych</span><span class="sxs-lookup"><span data-stu-id="5b433-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="5b433-113">Funkcja prognozowania jest powszechnie pracowników i bardzo przydatne metody analitycznej.</span><span class="sxs-lookup"><span data-stu-id="5b433-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="5b433-114">Wspólne używa zakresu z przewidywania sprzedaży elementów okresach Określanie optymalnego zapasów, zmienne makroekonomicznej toopredicting.</span><span class="sxs-lookup"><span data-stu-id="5b433-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="5b433-115">Funkcja prognozowania jest zazwyczaj wykonywane z modeli szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="5b433-116">Czas serii danych jest danych, w którym wartości hello ma indeks czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="5b433-117">Indeks czasu Hello może być regularnie, np. co miesiąc lub co minutę lub nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="5b433-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="5b433-118">Model szeregów czasowych jest na podstawie czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-118">A time series model is based on time series data.</span></span> <span data-ttu-id="5b433-119">język programowania Hello R zawiera elastyczną architekturę i szeroką gamę analiza czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="5b433-120">W tym przewodniku Szybki Start możemy zostanie praca z mleczarskie Kalifornijskiej i cenach danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="5b433-121">Te dane obejmują informacje miesięczne na powitania produkcji kilka mleczarskich i hello ceny mleka fat zwykłych stawek.</span><span class="sxs-lookup"><span data-stu-id="5b433-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="5b433-122">dane Hello używane w tym artykule, wraz ze skryptami R, mogą być [pobrana w tym miejscu][download].</span><span class="sxs-lookup"><span data-stu-id="5b433-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="5b433-123">Te dane został pierwotnie syntezatora z informacji dostępnych w hello uniwersytecie Wisconsin na http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="5b433-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="5b433-124">Organizacja</span><span class="sxs-lookup"><span data-stu-id="5b433-124">Organization</span></span>
<span data-ttu-id="5b433-125">Firma Microsoft będzie postęp kilku kroków jako dowiesz się, jak toocreate, testowanie i wykonanie kodu manipulowania R analizy i danych w środowisku Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="5b433-126">Najpierw przeanalizujemy podstawy hello przy użyciu języka hello R w środowisku Azure Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="5b433-127">Następnie możemy postępu toodiscussing różnych aspektów we/wy dla danych, kodu języka R i grafiki w środowisku Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="5b433-128">Firma Microsoft będzie skonstruować hello pierwsza część naszego prognozowania rozwiązania przez utworzenie kodu do czyszczenia danych i przekształcania.</span><span class="sxs-lookup"><span data-stu-id="5b433-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="5b433-129">Z naszych danych przygotowane zostaną wykonane analizę hello korelacji między kilka hello zmiennych w naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="5b433-130">Na koniec utworzymy model prognozowania szeregów czasowych okresach do produkcji mleka.</span><span class="sxs-lookup"><span data-stu-id="5b433-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="5b433-131"><a id="mlstudio"></a>Interakcje z języka R w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5b433-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="5b433-132">W tej sekcji przedstawia niektóre podstawowe informacje o interakcji z języka programowania hello R w środowisku usługi Machine Learning Studio hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="5b433-133">język Hello R udostępnia zaawansowane narzędzia toocreate dostosowane analizy i danych manipulowania modułów w środowisku Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="5b433-134">Użyję programu RStudio toodevelop, badanie i debugowania kodu R na małą skalę.</span><span class="sxs-lookup"><span data-stu-id="5b433-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="5b433-135">Ten kod jest następnie wycinanie i wklejanie w [wykonanie skryptu języka R] [ execute-r-script] modułu w toorun gotowy Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="5b433-136">Witaj modułu wykonania skryptu języka R</span><span class="sxs-lookup"><span data-stu-id="5b433-136">hello Execute R Script module</span></span>
<span data-ttu-id="5b433-137">W usłudze Machine Learning Studio, R skrypty są uruchamiane w ramach hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-138">Przykład Witaj [wykonanie skryptu języka R] [ execute-r-script] modułu w usłudze Machine Learning Studio jest pokazany na rysunku 1.</span><span class="sxs-lookup"><span data-stu-id="5b433-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R język programowania: hello modułu wykonania skryptu języka R wybrane w usłudze Machine Learning Studio][1]

<span data-ttu-id="5b433-140">*Rysunek 1. środowiska usługi Machine Learning Studio Hello przedstawiający modułu wykonania skryptu języka R hello wybrane.*</span><span class="sxs-lookup"><span data-stu-id="5b433-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="5b433-141">Odwoływanie tooFigure 1, Przyjrzyjmy się niektóre z kluczowych części środowiska usługi Machine Learning Studio hello do pracy z hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="5b433-142">Moduły Hello w eksperymencie hello są wyświetlane w okienku Centrum hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="5b433-143">Witaj górna część hello w prawym okienku zawiera tooview okna i edycji skryptów R.</span><span class="sxs-lookup"><span data-stu-id="5b433-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="5b433-144">Witaj dolnej części prawym okienku przedstawia niektóre właściwości hello [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="5b433-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="5b433-145">Dzienniki błędów i dane wyjściowe hello można wyświetlić, klikając odpowiednie punkty hello tego okienka.</span><span class="sxs-lookup"><span data-stu-id="5b433-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="5b433-146">Firma Microsoft będzie oczywiście w niniejszym dokumencie hello [wykonanie skryptu języka R] [ execute-r-script] bardziej szczegółowo na powitania pozostałej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="5b433-147">Podczas pracy z złożonych funkcji R, zalecamy edytować, testowania i debugowania w programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="5b433-148">Podobnie jak w przypadku dowolnego rozwoju oprogramowania przyrostowo rozszerzyć kodu i przetestować go na małych prostych przypadkach testowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="5b433-149">Następnie wycinanie i wklejanie funkcji do okna skryptu hello R hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-150">Takie podejście umożliwia tooharness zarówno hello programu RStudio zintegrowane środowisko programistyczne (IDE) i hello możliwości usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5b433-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="5b433-151">Wykonanie kodu języka R</span><span class="sxs-lookup"><span data-stu-id="5b433-151">Execute R code</span></span>
<span data-ttu-id="5b433-152">Kod języka R w hello [wykonanie skryptu języka R] [ execute-r-script] modułu zostanie wykonany po uruchomieniu hello eksperyment, klikając hello **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b433-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="5b433-153">Po zakończeniu wykonywania znacznik wyboru pojawią się na powitania [wykonanie skryptu języka R] [ execute-r-script] ikony.</span><span class="sxs-lookup"><span data-stu-id="5b433-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="5b433-154">Kodowanie obrony R dla usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b433-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="5b433-155">Jeśli tworzysz kodu R, na przykład usługi sieci web przy użyciu usługi Azure Machine Learning, należy ostatecznie zaplanować, jak kod zajmuje się nieoczekiwane dane wejściowe i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="5b433-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="5b433-156">toomaintain przejrzystości, I nie zostały uwzględnione sposób hello sprawdzanie lub obsługi wyjątków w większości podane przykłady kodu hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="5b433-157">Jednak jak możemy kontynuować I zapewni kilka przykładów funkcji przy użyciu możliwości obsługi wyjątków, R.</span><span class="sxs-lookup"><span data-stu-id="5b433-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="5b433-158">Jeśli potrzebujesz bardziej szczegółowy traktowanie Obsługa wyjątków języka R, najlepiej odczytu hello odpowiednie części podręcznika hello przez Wickham wymienionych w [dodatek B — dalsze informacje](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="5b433-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="5b433-159">Debugowania i testowania R w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5b433-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="5b433-160">tooreiterate, I zaleca się testowanie i debugowanie kodu języka R na małą skalę w programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="5b433-161">Istnieją jednak przypadki, w których konieczne tootrack dół problemów kodu języka R w hello [wykonanie skryptu języka R] [ execute-r-script] samej siebie.</span><span class="sxs-lookup"><span data-stu-id="5b433-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="5b433-162">Ponadto jest dobrym rozwiązaniem toocheck wyniki w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="5b433-163">Dane wyjściowe wykonania hello kodu języka R i na platformie Azure Machine Learning hello znajduje się głównie w dane_wyjściowe.log.</span><span class="sxs-lookup"><span data-stu-id="5b433-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="5b433-164">Dodatkowe informacje będą widoczne w error.log.</span><span class="sxs-lookup"><span data-stu-id="5b433-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="5b433-165">Jeśli w usłudze Machine Learning Studio występuje błąd podczas uruchamiania kodu języka R, pierwszy przebiegu działań powinny być toolook na error.log.</span><span class="sxs-lookup"><span data-stu-id="5b433-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="5b433-166">Ten plik może zawierać błąd przydatne wiadomości toohelp zrozumieć i poprawić ten błąd.</span><span class="sxs-lookup"><span data-stu-id="5b433-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="5b433-167">error.log tooview, kliknij przycisk **dziennik błędów w widoku** na powitania **w okienku właściwości** dla hello [wykonanie skryptu języka R] [ execute-r-script] zawierające błąd hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="5b433-168">Na przykład został uruchomiony hello następującego kodu R, niezdefiniowane y zmiennej w [wykonanie skryptu języka R] [ execute-r-script] modułu:</span><span class="sxs-lookup"><span data-stu-id="5b433-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="5b433-169">Ten kod nie powiedzie się tooexecute, co powoduje wystąpienie stanu błędu.</span><span class="sxs-lookup"><span data-stu-id="5b433-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="5b433-170">Kliknięcie **dziennik błędów w widoku** na powitania **w okienku właściwości** tworzy hello wyświetlania pokazany na rysunku 2.</span><span class="sxs-lookup"><span data-stu-id="5b433-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Komunikat o błędzie wyskakującego okienka][2]

<span data-ttu-id="5b433-172">*Rysunek 2. Komunikat o błędzie wyskakujących.*</span><span class="sxs-lookup"><span data-stu-id="5b433-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="5b433-173">Wygląda na to, potrzebujemy toolook w komunikacie o błędzie dane_wyjściowe.log toosee hello R.</span><span class="sxs-lookup"><span data-stu-id="5b433-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="5b433-174">Polecenie hello [wykonanie skryptu języka R] [ execute-r-script] , a następnie kliknij polecenie hello **wyświetlić dane_wyjściowe.log** element na powitania **w okienku właściwości** toohello prawo.</span><span class="sxs-lookup"><span data-stu-id="5b433-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="5b433-175">Otwiera nowe okno przeglądarki i są widoczne następujące hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="5b433-176">Ten komunikat o błędzie zawiera nie niespodzianki i jasno identyfikuje hello problem.</span><span class="sxs-lookup"><span data-stu-id="5b433-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="5b433-177">wartość hello tooinspect wszystkich obiektów w R, możesz wydrukować pliku dane_wyjściowe.log toohello tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="5b433-178">reguły Hello badania obiektu wartości są zasadniczo hello takie same jak w sesji interaktywnej R.</span><span class="sxs-lookup"><span data-stu-id="5b433-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="5b433-179">Na przykład jeśli wpiszesz nazwę zmiennej w wierszu, wartość hello hello obiektu będzie drukowanej toohello dane_wyjściowe.log pliku.</span><span class="sxs-lookup"><span data-stu-id="5b433-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="5b433-180">Pakiety w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5b433-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="5b433-181">Usługa Azure Machine Learning jest dostarczany z ponad 350 wstępnie zainstalowane pakiety języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="5b433-182">Można użyć następującego kodu w hello hello [wykonanie skryptu języka R] [ execute-r-script] tooretrieve modułu listę hello wstępnie zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="5b433-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="5b433-183">Jeśli nie znasz hello ostatniego wiersza kodu w chwili hello, poniżej.</span><span class="sxs-lookup"><span data-stu-id="5b433-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="5b433-184">W hello pozostałej części tego dokumentu często omówimy użycia języka R w środowisku Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="5b433-185">Wprowadzenie tooRStudio</span><span class="sxs-lookup"><span data-stu-id="5b433-185">Introduction tooRStudio</span></span>
<span data-ttu-id="5b433-186">Programu RStudio jest powszechnie używaną IDE dla R. Użyję programu RStudio edycji, testowanie i debugowanie części kodu hello R używanych w tym przewodniku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="5b433-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="5b433-187">Po kodzie R przetestowane i gotowe, po prostu wyciąć i wkleić w edytorze programu RStudio hello w usłudze Machine Learning Studio [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="5b433-188">Jeśli nie masz hello R język programowania zainstalowana na tym komputerze pulpitu, zaleca się, że możesz to zrobić teraz.</span><span class="sxs-lookup"><span data-stu-id="5b433-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="5b433-189">Bezpłatne materiały do pobrania języka typu open source R są dostępne pod adresem hello kompleksowe R sieci (CRAN archiwum sieci) w [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="5b433-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="5b433-190">Brak dostępnych pliki do pobrania dla systemu Windows, Mac OS i Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="5b433-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="5b433-191">Wybierz pobliskich dublowania i postępuj zgodnie z instrukcjami pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="5b433-192">Ponadto sieci CRAN zawiera wiele pakietów manipulowania przydatne analizy i danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="5b433-193">W przypadku nowych tooRStudio należy pobrać i zainstalować wersję pulpitu hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="5b433-194">Można znaleźć powitalne programu RStudio w http://www.rstudio.com/products/RStudio/ pobiera systemu Windows, Mac OS i Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="5b433-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="5b433-195">Postępuj zgodnie z instrukcjami hello podane tooinstall programu RStudio na komputerze pulpitu.</span><span class="sxs-lookup"><span data-stu-id="5b433-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="5b433-196">TooRStudio samouczka Wprowadzenie jest dostępny na https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="5b433-197">I Podaj dodatkowe informacje na temat używania programu RStudio w [dodatek a.][appendixa].</span><span class="sxs-lookup"><span data-stu-id="5b433-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="5b433-198"><a id="scriptmodule"></a>Pobieranie danych i modułu wykonania skryptu języka R hello</span><span class="sxs-lookup"><span data-stu-id="5b433-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="5b433-199">W tej sekcji omówimy, jak pobrać dane do i z hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-200">Zapoznamy się, jak toohandle różne typy danych do odczytu do i z hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="5b433-201">Hello kompletny kod dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b433-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="5b433-202">Załadowanie i sprawdzenie, czy dane w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5b433-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="5b433-203"><a id="loading"></a>Zestaw danych hello obciążenia</span><span class="sxs-lookup"><span data-stu-id="5b433-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="5b433-204">Rozpoczniemy ładując hello **csdairydata.csv** pliku do usługi Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="5b433-205">Uruchom środowiska Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="5b433-206">Polecenie **+ nowy** na powitania lewy ekranu i wybierz dolny **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="5b433-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="5b433-207">Wybierz **z pliku lokalnego**, a następnie **Przeglądaj** tooselect hello pliku.</span><span class="sxs-lookup"><span data-stu-id="5b433-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="5b433-208">Upewnij się, że wybrano **pliku CSV ogólnego z nagłówkiem (.csv)** jako typ hello hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="5b433-209">Kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-209">Click hello check mark.</span></span>
* <span data-ttu-id="5b433-210">Po przekazaniu hello zestawu danych, powinny pojawić się hello nowy zestaw danych, klikając hello **zestawów danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="5b433-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="5b433-211">Tworzenie eksperymentu</span><span class="sxs-lookup"><span data-stu-id="5b433-211">Create an experiment</span></span>
<span data-ttu-id="5b433-212">Teraz, gdy mamy niektóre dane w usłudze Machine Learning Studio, potrzebujemy toocreate analizę hello toodo eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="5b433-213">Polecenie **+ nowy** na powitania lewy dolny i wybierz **eksperymentu**, następnie **pusty eksperyment**.</span><span class="sxs-lookup"><span data-stu-id="5b433-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="5b433-214">Nazwa eksperymentu, wybierając i modyfikowanie hello **eksperymentu utworzony na...**  tytuł u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="5b433-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="5b433-215">Na przykład zmiana zbyt**urzędu certyfikacji Nabiał analizy**.</span><span class="sxs-lookup"><span data-stu-id="5b433-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="5b433-216">Na powitania po lewej stronie eksperymentu hello, rozwiń **zapisane zestawów danych**, a następnie **Moje zestawów danych**.</span><span class="sxs-lookup"><span data-stu-id="5b433-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="5b433-217">Powinny pojawić się hello **cadairydata.csv** który został wcześniej przekazany.</span><span class="sxs-lookup"><span data-stu-id="5b433-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="5b433-218">Przeciąganie i upuszczanie hello **csdairydata.csv dataset** na powitania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="5b433-219">W hello **wyszukiwania eksperymentu elementów** pole na powitania górnej części okienka po lewej stronie powitania, typu [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="5b433-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="5b433-220">Zostanie wyświetlone modułu hello są wyświetlane na liście wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="5b433-221">Przeciąganie i upuszczanie hello [wykonanie skryptu języka R] [ execute-r-script] modułu na Twoje palety.</span><span class="sxs-lookup"><span data-stu-id="5b433-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="5b433-222">Połącz dane wyjściowe hello hello **csdairydata.csv dataset** toohello po lewej stronie dane wejściowe (**Dataset1**) z hello [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="5b433-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="5b433-223">**Nie zapomnij tooclick "Zapisz"!**</span><span class="sxs-lookup"><span data-stu-id="5b433-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="5b433-224">W tym momencie eksperymentu powinien wyglądać jak rysunek 3.</span><span class="sxs-lookup"><span data-stu-id="5b433-224">At this point your experiment should look something like Figure 3.</span></span>

![Witaj analizy Nabiał urzędu certyfikacji eksperymentów z zestawu danych i modułu wykonania skryptu języka R][3]

<span data-ttu-id="5b433-226">*Rysunek 3. Witaj analizy Nabiał urzędu certyfikacji Eksperymentuj z zestawu danych i modułu wykonania skryptu języka R.*</span><span class="sxs-lookup"><span data-stu-id="5b433-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="5b433-227">Sprawdź na powitania danych</span><span class="sxs-lookup"><span data-stu-id="5b433-227">Check on hello data</span></span>
<span data-ttu-id="5b433-228">Załóżmy mają wygląd hello dane, które firma Microsoft zostały załadowane na naszym doświadczeniu.</span><span class="sxs-lookup"><span data-stu-id="5b433-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="5b433-229">W eksperymencie powitania kliknij hello dane wyjściowe hello **cadairydata.csv dataset** i wybierz **wizualizacji**.</span><span class="sxs-lookup"><span data-stu-id="5b433-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="5b433-230">Powinny zostać wyświetlone informacje takie jak rysunek 4.</span><span class="sxs-lookup"><span data-stu-id="5b433-230">You should see something like Figure 4.</span></span>  

![Podsumowanie hello cadairydata.csv w zestawie danych][4]

<span data-ttu-id="5b433-232">*Rysunek 4. Podsumowanie hello cadairydata.csv dataset.*</span><span class="sxs-lookup"><span data-stu-id="5b433-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="5b433-233">W tym widoku widzimy wiele przydatnych informacji.</span><span class="sxs-lookup"><span data-stu-id="5b433-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="5b433-234">Zobaczysz hello pierwsze kilka wierszy tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="5b433-235">Zaznaczenie kolumny, hello sekcji Statystyki zawiera więcej informacji na temat hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="5b433-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="5b433-236">Na przykład hello typu funkcji wiersza pokazuje nam, jakie typy danych Azure Machine Learning Studio przypisane toohello kolumny.</span><span class="sxs-lookup"><span data-stu-id="5b433-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="5b433-237">Krótki przegląd podobny do tego jest wyboru związane z poprawnością dobra przed Rozpoczniemy toodo poważne pracę.</span><span class="sxs-lookup"><span data-stu-id="5b433-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="5b433-238">Pierwszy skrypt języka R</span><span class="sxs-lookup"><span data-stu-id="5b433-238">First R script</span></span>
<span data-ttu-id="5b433-239">W usłudze Azure Machine Learning Studio Utwórz prosty pierwszy R skryptu tooexperiment z.</span><span class="sxs-lookup"><span data-stu-id="5b433-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="5b433-240">Po utworzeniu i przetestowane hello następującego skryptu programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="5b433-241">Teraz potrzebuję tootransfer tooAzure tego skryptu Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="5b433-242">I może po prostu wyciąć i wkleić.</span><span class="sxs-lookup"><span data-stu-id="5b433-242">I could simply cut and paste.</span></span> <span data-ttu-id="5b433-243">Jednak w takim przypadku I przenieś Moje skrypt języka R za pomocą pliku zip.</span><span class="sxs-lookup"><span data-stu-id="5b433-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="5b433-244">Moduł wykonanie skryptu języka R toohello wprowadzania danych</span><span class="sxs-lookup"><span data-stu-id="5b433-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="5b433-245">Załóżmy ma przyjrzeć się toohello dane wejściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-246">W tym przykładzie firma Microsoft będzie odczytywać dane mleczarskich Kalifornijskiej hello na powitania [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="5b433-247">Istnieją trzy możliwe dane wejściowe dla hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-248">W zależności od aplikacji, można użyć dowolnego lub wszystkich tych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="5b433-249">Możliwe jest również doskonale uzasadnione toouse R skrypt, który nie wymaga danych wejściowych w ogóle.</span><span class="sxs-lookup"><span data-stu-id="5b433-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="5b433-250">Przyjrzyjmy się każdy z tych danych wejściowych z tooright po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5b433-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="5b433-251">Widać nazwy hello każdego wejścia hello umieszczając kursor nad hello danych wejściowych i odczytywania hello etykietka narzędzia.</span><span class="sxs-lookup"><span data-stu-id="5b433-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="5b433-252">Skrypt pakietu</span><span class="sxs-lookup"><span data-stu-id="5b433-252">Script Bundle</span></span>
<span data-ttu-id="5b433-253">Witaj danych wejściowych skryptu pakietu pozwala toopass hello zawartość pliku zip do [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-254">Można użyć jednego hello następujące polecenia tooread hello zawartość pliku zip hello w kodzie języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="5b433-255">Usługa Azure Machine Learning traktuje plików hello zip tak, jakby znajdują się w hello src / directory, w związku z czym należy tooprefix nazwy pliku o tej nazwie w katalogu.</span><span class="sxs-lookup"><span data-stu-id="5b433-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="5b433-256">Na przykład jeśli hello zip zawiera pliki hello `yourfile.R` i `yourData.rdata` w głównym hello hello zip, czy adres je jako `src/yourfile.R` i `src/yourData.rdata` przy użyciu `source` i `load`.</span><span class="sxs-lookup"><span data-stu-id="5b433-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="5b433-257">Omówiono już zestawy danych ładowania [podczas ładowania zestawu danych hello](#loading).</span><span class="sxs-lookup"><span data-stu-id="5b433-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="5b433-258">Po utworzeniu i przetestować skrypt hello R wyświetlone w poprzedniej sekcji hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="5b433-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="5b433-259">Zapisz skrypt hello R do. Plik R.</span><span class="sxs-lookup"><span data-stu-id="5b433-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="5b433-260">Można wywołać pliku skryptu "simpleplot. R".</span><span class="sxs-lookup"><span data-stu-id="5b433-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="5b433-261">Oto hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="5b433-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="5b433-262">Utwórz plik zip i skopiuj skrypt do tego pliku zip.</span><span class="sxs-lookup"><span data-stu-id="5b433-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="5b433-263">W systemie Windows, kliknij prawym przyciskiem myszy na powitania plik i wybierz **przesyłają**, a następnie **skompresowanego folderu**.</span><span class="sxs-lookup"><span data-stu-id="5b433-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="5b433-264">Spowoduje to utworzenie nowego pliku zip zawierającego powitania "simpleplot. Plik R".</span><span class="sxs-lookup"><span data-stu-id="5b433-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="5b433-265">Dodaj z pliku toohello **zestawów danych** w usłudze Machine Learning Studio, określając hello typ jako **zip**.</span><span class="sxs-lookup"><span data-stu-id="5b433-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="5b433-266">Plik zip hello powinna zostać wyświetlona w zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="5b433-267">Przeciąganie i upuszczanie plików zip hello z **zestawów danych** na powitania **kanwy ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="5b433-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="5b433-268">Połącz dane wyjściowe hello hello **zip danych** toohello ikona **pakietu skryptu** wejściowych z hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="5b433-269">Typ hello `source()` funkcji z nazwy pliku zip do okna Kod powitania dla hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-270">W przypadku mojej wpisane `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="5b433-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="5b433-271">Upewnij się, że możesz kliknąć pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5b433-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="5b433-272">Po zakończeniu tych czynności hello [wykonanie skryptu języka R] [ execute-r-script] modułu wykona hello R skryptu w pliku zip powitania po uruchomieniu hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="5b433-273">W tym momencie eksperymentu powinien wyglądać jak rysunek 5.</span><span class="sxs-lookup"><span data-stu-id="5b433-273">At this point your experiment should look something like Figure 5.</span></span>

![Przy użyciu eksperymentów zip skrypt języka R][6]

<span data-ttu-id="5b433-275">*Rysunek 5. Przy użyciu eksperymentów zip skrypt języka R.*</span><span class="sxs-lookup"><span data-stu-id="5b433-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="5b433-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="5b433-276">Dataset1</span></span>
<span data-ttu-id="5b433-277">Można przekazać prostokątne tabeli danych tooyour R kodu za pomocą hello Dataset1 danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="5b433-278">W naszym hello prostego skryptu `maml.mapInputPort(1)` funkcja odczytuje hello dane z portu 1.</span><span class="sxs-lookup"><span data-stu-id="5b433-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="5b433-279">Te dane jest przypisywana nazwa zmiennej dataframe tooa w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5b433-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="5b433-280">W naszym prostego skryptu hello pierwszy wiersz kodu wykonuje hello przypisania.</span><span class="sxs-lookup"><span data-stu-id="5b433-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="5b433-281">Wykonanie eksperymentu, klikając hello **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b433-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="5b433-282">Po zakończeniu wykonywania hello, kliknij polecenie hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie kliknij przycisk **widoku pliku dziennika** w okienku właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="5b433-283">Nowa strona powinna zostać wyświetlona w przeglądarce przedstawiający hello zawartość pliku dane_wyjściowe.log hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="5b433-284">Podczas przewijania w dół powinien zostać wyświetlony ekran podobny do następujących hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="5b433-285">Dalej w dół hello strona jest bardziej szczegółowe informacje o hello kolumn, które będą wyglądać jak poniżej hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="5b433-286">Wyniki są przeważnie zgodnie z oczekiwaniami, 228 uwag i 9 kolumn w hello dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="5b433-287">Widzimy hello nazwy kolumn, typ danych hello R i przykładowe każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="5b433-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="5b433-288">Ten sam wydruku jest łatwo dostępne z hello urządzenia R dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-289">Omówimy hello elementy wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="5b433-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="5b433-290">Dataset2</span></span>
<span data-ttu-id="5b433-291">Witaj zachowanie hello Dataset2 danych wejściowych jest identyczne toothat z Dataset1.</span><span class="sxs-lookup"><span data-stu-id="5b433-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="5b433-292">Przy użyciu tych danych wejściowych można przekazać drugiej tabeli prostokątne danych do kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="5b433-293">Witaj funkcja `maml.mapInputPort(2)`, z argumentem hello 2, jest używane toopass tych danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="5b433-294">Wykonanie skryptu języka R w danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5b433-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="5b433-295">Dane wyjściowe dataframe</span><span class="sxs-lookup"><span data-stu-id="5b433-295">Output a dataframe</span></span>
<span data-ttu-id="5b433-296">Można output hello zawartość dataframe R jako tabelę prostokątne za pośrednictwem portu hello Dataset1 wyników przy użyciu hello `maml.mapOutputPort()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="5b433-297">W naszym prostego skryptu języka R jest to wykonywane przez hello następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5b433-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="5b433-298">Po uruchomionych hello eksperymentu, kliknij na powitania port wyjściowy Dataset1 wyników, a następnie kliknij polecenie **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="5b433-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="5b433-299">Powinny zostać wyświetlone informacje takie jak rysunek 6.</span><span class="sxs-lookup"><span data-stu-id="5b433-299">You should see something like Figure 6.</span></span>

![Hello wizualizację danych wyjściowych hello hello Kalifornijskiej mleczarskich danych][7]

<span data-ttu-id="5b433-301">*Rysunek 6. Wizualizacja Hello hello dane wyjściowe hello Kalifornijskiej mleczarskich danych.*</span><span class="sxs-lookup"><span data-stu-id="5b433-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="5b433-302">Te dane wyjściowe wygląda toohello identyczne dane wejściowe, dokładnie tak, jak oczekiwaliśmy.</span><span class="sxs-lookup"><span data-stu-id="5b433-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="5b433-303">Dane wyjściowe R urządzenia</span><span class="sxs-lookup"><span data-stu-id="5b433-303">R Device output</span></span>
<span data-ttu-id="5b433-304">Witaj urządzenia dane wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] moduł zawiera dane wyjściowe wiadomości i grafiki.</span><span class="sxs-lookup"><span data-stu-id="5b433-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="5b433-305">Standardowe Wyjście i błąd standardowy komunikaty o błędach z języka R są wysyłane toohello port wyjściowy R urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="5b433-306">Witaj tooview R urządzenia wyjściowego, kliknij na powitania portu, a następnie na **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="5b433-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="5b433-307">Widzimy hello wyjście standardowe i błąd standardowy ze skryptu hello R na rysunku 7.</span><span class="sxs-lookup"><span data-stu-id="5b433-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Wyjście standardowe i błąd standardowy z hello portu urządzenia R][8]

<span data-ttu-id="5b433-309">*Rysunek 7. Wyjście standardowe i błąd standardowy z hello portu urządzenia R.*</span><span class="sxs-lookup"><span data-stu-id="5b433-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="5b433-310">Przewijanie w dół możemy wyświetlić dane wyjściowe grafiki hello z naszych skrypt języka R na rysunku 8.</span><span class="sxs-lookup"><span data-stu-id="5b433-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Dane wyjściowe grafiki hello portu urządzenia R][9]

<span data-ttu-id="5b433-312">*Rysunek 8. Graficzne dane wyjściowe z hello portu urządzenia R.*</span><span class="sxs-lookup"><span data-stu-id="5b433-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="5b433-313"><a id="filtering"></a>Filtrowanie danych i przekształcania</span><span class="sxs-lookup"><span data-stu-id="5b433-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="5b433-314">W tej sekcji zostaną wykonane niektóre podstawowe dane filtrowania i operacjami transformacji na powitania Kalifornijskiej mleczarskich danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="5b433-315">Końca hello w tej sekcji zostanie zostały dane w formacie odpowiedni w przypadku tworzenia modelu danych analitycznych.</span><span class="sxs-lookup"><span data-stu-id="5b433-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="5b433-316">W szczególności, w tej sekcji zostaną wykonane kilka typowych danych czyszczenia i przekształcenie zadań: wpisz przekształcania filtrowanie dataframes Dodawanie nowej kolumny obliczane, a wartość przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="5b433-317">Ta tła powinna ułatwić postępowania w przypadku hello wiele zmian w rzeczywistych problemów.</span><span class="sxs-lookup"><span data-stu-id="5b433-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="5b433-318">Hello pełną R kodu w tej sekcji znajduje się w pliku zip hello pobrany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b433-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="5b433-319">Typ przekształcenia</span><span class="sxs-lookup"><span data-stu-id="5b433-319">Type transformations</span></span>
<span data-ttu-id="5b433-320">Teraz, gdy firma Microsoft może odczytywać hello Kalifornijskiej mleczarskich danych do kodu hello R w hello [wykonanie skryptu języka R] [ execute-r-script] modułu, potrzebujemy tooensure, że dane hello w kolumnach hello ma hello przeznaczony typ i format.</span><span class="sxs-lookup"><span data-stu-id="5b433-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="5b433-321">R jest językiem typach określanych dynamicznie, co oznacza, że typy danych są przekształcone z jednego tooanother zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="5b433-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="5b433-322">typy danych atomic Hello w R to liczbowe, logicznych i znak.</span><span class="sxs-lookup"><span data-stu-id="5b433-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="5b433-323">Typ współczynnik Hello jest używane toocompactly przechowywania danych podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="5b433-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="5b433-324">Znacznie więcej informacji o typach danych można znaleźć w odwołaniach hello w [dodatek B — dalsze informacje](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="5b433-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="5b433-325">Podczas odczytywania danych tabelarycznych w R ze źródła zewnętrznego, zawsze jest dobrym rozwiązaniem hello toocheck, co typów w kolumnach hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="5b433-326">Może być kolumną typu znaków, ale w wielu przypadkach to będzie wyświetlany jako współczynnik lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="5b433-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="5b433-327">W innych przypadkach kolumny, które zdaniem użytkownika powinna być liczbowe jest reprezentowana przez dane znakowe, np. numer punktu "1,23" zamiast 1,23 jako liczbą zmiennoprzecinkową.</span><span class="sxs-lookup"><span data-stu-id="5b433-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="5b433-328">Na szczęście jest łatwe tooconvert jeden typ tooanother tak długo, jak mapowanie jest możliwe.</span><span class="sxs-lookup"><span data-stu-id="5b433-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="5b433-329">Na przykład "Nevada" nie można przekonwertować na wartość numeryczną, ale można go przekonwertować współczynnik tooa (podzielone na kategorie zmienna).</span><span class="sxs-lookup"><span data-stu-id="5b433-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="5b433-330">Inny przykład liczbowe 1 można przekonwertować na znak "1" lub współczynnik.</span><span class="sxs-lookup"><span data-stu-id="5b433-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="5b433-331">żadnego z tych konwersje Hello składnia jest prosty: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="5b433-332">Te funkcje konwersji typu obejmują następujące hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="5b433-333">Spojrzenie na powitania typy danych kolumn hello możemy danych wejściowych w poprzedniej sekcji hello: wszystkie kolumny są typu liczbowego, z wyjątkiem hello kolumnę z etykietą "Month", który jest typem znaku.</span><span class="sxs-lookup"><span data-stu-id="5b433-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="5b433-334">Umożliwia konwertowanie ten współczynnik tooa i hello wyniki testu.</span><span class="sxs-lookup"><span data-stu-id="5b433-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="5b433-335">Usunięto wiersz hello hello scatterplot macierzy i dodawane linii konwertowanie współczynnik tooa kolumny "Month" hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="5b433-336">W moim eksperymencie I będzie tylko wycinanie i wklejanie kodu hello R do okna Kod hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="5b433-337">Można również zaktualizować hello pliku zip i przekazać go tooAzure Machine Learning Studio, ale trwa to kilka kroków.</span><span class="sxs-lookup"><span data-stu-id="5b433-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="5b433-338">Umożliwia wykonanie tego kodu i sprawdź w dzienniku danych wyjściowych hello hello skrypt języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="5b433-339">Witaj odpowiednich danych z dziennika hello jest pokazano na rysunku 9.</span><span class="sxs-lookup"><span data-stu-id="5b433-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="5b433-340">*Rysunek 9. Podsumowanie dataframe hello ze zmienną Multi-Factor.*</span><span class="sxs-lookup"><span data-stu-id="5b433-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="5b433-341">Typ Hello miesiąc teraz zostanie wyświetlony komunikat "**współczynnik z 14 poziomy**".</span><span class="sxs-lookup"><span data-stu-id="5b433-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="5b433-342">Jest to problem, ponieważ w roku hello są tylko 12 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="5b433-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="5b433-343">Możesz również sprawdzić toosee, który hello typu w **Visualize** hello wynik Dataset jest port "**Categorical**".</span><span class="sxs-lookup"><span data-stu-id="5b433-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="5b433-344">Hello problem jest tym hello "Month", kolumna nie zawiera systematycznie kodowany.</span><span class="sxs-lookup"><span data-stu-id="5b433-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="5b433-345">W niektórych przypadkach miesiąca nosi kwietnia i w innych jest skracana jako kwietnia. Problem można rozwiązać przez przycinanie znaków too3 ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="5b433-346">Witaj wiersz kodu teraz wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="5b433-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="5b433-347">Ponownie hello eksperyment i wyświetlić hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="5b433-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="5b433-348">Witaj oczekuje się, że wyniki są wyświetlane na rysunku nr 10.</span><span class="sxs-lookup"><span data-stu-id="5b433-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="5b433-349">*Rysunek 10. Podsumowanie dataframe hello z poprawną liczbę poziomów współczynnik.*</span><span class="sxs-lookup"><span data-stu-id="5b433-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="5b433-350">Nasze zmiennej współczynnik ma teraz hello potrzeby 12 poziomów.</span><span class="sxs-lookup"><span data-stu-id="5b433-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="5b433-351">Filtrowanie ramki danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="5b433-351">Basic data frame filtering</span></span>
<span data-ttu-id="5b433-352">R dataframes obsługuje zaawansowane funkcje filtrowania.</span><span class="sxs-lookup"><span data-stu-id="5b433-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="5b433-353">Zestawy danych mogą być podzbiory przy użyciu filtrów logiczne według wierszy lub kolumn.</span><span class="sxs-lookup"><span data-stu-id="5b433-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="5b433-354">W wielu przypadkach będzie wymagane kryteria filtrowania złożonych.</span><span class="sxs-lookup"><span data-stu-id="5b433-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="5b433-355">Witaj odwołania w [dodatek B — dalsze informacje](#appendixb) zawierają przykłady szeroką gamę dataframes filtrowania.</span><span class="sxs-lookup"><span data-stu-id="5b433-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="5b433-356">Istnieje jeden bit filtrowania należy wykonać w naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="5b433-357">Jeśli przyjrzymy się hello kolumn w hello cadairydata dataframe, zobaczysz dwóch zbędne kolumny.</span><span class="sxs-lookup"><span data-stu-id="5b433-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="5b433-358">Hello pierwsza kolumna zawiera tylko numer wiersza, który nie jest bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="5b433-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="5b433-359">Witaj drugiej kolumny Year.Month, zawiera nadmiarowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="5b433-360">Firma Microsoft łatwo wykluczyć te kolumny za pomocą hello następującego kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="5b433-361">Od teraz w w tej sekcji zostanie tylko wyświetlić możesz dodatkowy kod dodaję hello hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="5b433-362">Dodam każdego nowego wiersza **przed** hello `str()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="5b433-363">Używać tej funkcji tooverify wyniki w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="5b433-364">Dodać powitania po wierszu kodu toomy R hello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="5b433-365">Uruchom ten kod w eksperymencie i sprawdź wynik hello hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="5b433-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="5b433-366">Wyniki te są wyświetlane w rysunek 11.</span><span class="sxs-lookup"><span data-stu-id="5b433-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="5b433-367">*Rysunek 11. Podsumowanie dataframe hello z dwóch kolumn będących jej usunąć.*</span><span class="sxs-lookup"><span data-stu-id="5b433-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="5b433-368">Dobre wieści!</span><span class="sxs-lookup"><span data-stu-id="5b433-368">Good news!</span></span> <span data-ttu-id="5b433-369">Uzyskujemy hello oczekiwano wyników.</span><span class="sxs-lookup"><span data-stu-id="5b433-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="5b433-370">Dodaj nową kolumnę</span><span class="sxs-lookup"><span data-stu-id="5b433-370">Add a new column</span></span>
<span data-ttu-id="5b433-371">modeli szeregów czasowych toocreate będzie ona wygodne toohave kolumny zawierające hello miesięcy od czasu uruchomienia hello hello szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="5b433-372">Utworzymy nową kolumnę "Month.Count".</span><span class="sxs-lookup"><span data-stu-id="5b433-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="5b433-373">toohelp organizowanie kodu hello utworzymy naszych pierwszej funkcji proste `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="5b433-374">Ta funkcja toocreate nową kolumnę w hello dataframe następnie zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="5b433-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="5b433-375">Nowy kod Hello ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="5b433-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="5b433-376">Teraz uruchomić eksperyment hello zaktualizowane i użyć hello danych wyjściowych dziennika tooview hello wyników.</span><span class="sxs-lookup"><span data-stu-id="5b433-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="5b433-377">W rysunku 12 przedstawiono te wyniki.</span><span class="sxs-lookup"><span data-stu-id="5b433-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="5b433-378">*Rysunek 12. Podsumowanie dataframe hello hello dodatkowe kolumny.*</span><span class="sxs-lookup"><span data-stu-id="5b433-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="5b433-379">Wygląda na to, wszystko działa.</span><span class="sxs-lookup"><span data-stu-id="5b433-379">It looks like everything is working.</span></span> <span data-ttu-id="5b433-380">W naszym dataframe zostały hello nową kolumnę z hello oczekiwanych wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="5b433-381">Przekształcenia wartości</span><span class="sxs-lookup"><span data-stu-id="5b433-381">Value transformations</span></span>
<span data-ttu-id="5b433-382">W tej sekcji zostaną wykonane na powitania wartości w niektórych hello kolumn z naszych dataframe niektórych prostych transformacji.</span><span class="sxs-lookup"><span data-stu-id="5b433-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="5b433-383">język Hello R obsługuje przekształcenia niemal dowolną wartość.</span><span class="sxs-lookup"><span data-stu-id="5b433-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="5b433-384">Witaj odwołania w [dodatek B — dalsze informacje](#appendixb) zawiera szeroką gamę przykłady.</span><span class="sxs-lookup"><span data-stu-id="5b433-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="5b433-385">Jeśli przyjrzymy się hello wartości podsumowań hello naszych dataframe powinny zostać wyświetlone informacje nieparzysta tutaj.</span><span class="sxs-lookup"><span data-stu-id="5b433-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="5b433-386">Więcej lodów niż mleko jest generowany w Kalifornijskiej?</span><span class="sxs-lookup"><span data-stu-id="5b433-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="5b433-387">Nie, oczywiście nie, jak to ma sensu sad jako ten fakt może być toosome NAS lovers lodów.</span><span class="sxs-lookup"><span data-stu-id="5b433-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="5b433-388">jednostki Hello są różne.</span><span class="sxs-lookup"><span data-stu-id="5b433-388">hello units are different.</span></span> <span data-ttu-id="5b433-389">Cena Hello jest w jednostkach nam kg, mleko jest w jednostkach 1 mln kg USA, lodów znajduje się w jednostkach 1000 nam galonach, i ser chałupniczej jest w jednostce 1000 jednostkach funt Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="5b433-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="5b433-390">Zakładając, że lodów waga na galon paliwa około jednostkach 6.5 funt, firma Microsoft może łatwo hello tooconvert mnożenia tych wartości, dzięki czemu są one w taki sam jednostek 1000 jednostkach funt.</span><span class="sxs-lookup"><span data-stu-id="5b433-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="5b433-391">Dla modelu prognozowania używamy mnożenia modelu trendu i okresach dostosowania tych danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="5b433-392">Transformacja dziennika pozwala nam toouse model liniowy, co upraszcza ten proces.</span><span class="sxs-lookup"><span data-stu-id="5b433-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="5b433-393">Można zastosować transformacji dziennika hello w hello sam funkcji, których mnożnik hello jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="5b433-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="5b433-394">W hello następującego kodu, można zdefiniować nową funkcję, `log.transform()`i zastosować je toohello wiersze zawierające hello wartości liczbowe.</span><span class="sxs-lookup"><span data-stu-id="5b433-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="5b433-395">Witaj R `Map()` hello tooapply używana jest funkcja `log.transform()` toohello funkcja wybrane kolumny z hello dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="5b433-396">`Map()`przypomina zbyt`apply()` , ale zezwala na więcej niż jedną listę argumentów toohello funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="5b433-397">Należy pamiętać, że lista mnożników dostarcza hello drugi argument toohello `log.transform()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="5b433-398">Witaj `na.omit()` funkcji jest używany jako nieco z tooensure oczyszczania nie ma brakujących lub dataframe hello niezdefiniowanej wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="5b433-399">Występuje dość bitowe w toku w hello `log.transform()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="5b433-400">Większość tego kodu jest wyszukiwanie potencjalnych problemów z argumentami hello lub zajmujących się wyjątki, które nadal mogą wystąpić podczas hello obliczenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="5b433-401">Tylko kilka wierszy kodu faktycznie hello obliczenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="5b433-402">Celem Hello programowania obrony hello jest tooprevent hello awarii jednej funkcji, który uniemożliwia przetwarzania przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="5b433-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="5b433-403">Niespodziewane błąd analizy długotrwałe może być dość irytujące dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5b433-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="5b433-404">tooavoid, który ograniczy tej sytuacji, domyślne wartości zwracanych musi być wybrana który uszkodzenie toodownstream przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="5b433-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="5b433-405">Komunikat jest również utworzonych tooalert użytkowników, którzy coś stała się problem.</span><span class="sxs-lookup"><span data-stu-id="5b433-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="5b433-406">Jeśli nie jesteś programowania toodefensive używanych w R, ten kod może wydawać się nieco utrudnione.</span><span class="sxs-lookup"><span data-stu-id="5b433-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="5b433-407">I przeprowadzi Cię przez najważniejsze czynności hello:</span><span class="sxs-lookup"><span data-stu-id="5b433-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="5b433-408">Wektor cztery komunikaty jest zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="5b433-408">A vector of four messages is defined.</span></span> <span data-ttu-id="5b433-409">Komunikaty te są używane toocommunicate informacji na temat niektórych hello ewentualne błędy i wyjątki, które mogą wystąpić o tym kodzie.</span><span class="sxs-lookup"><span data-stu-id="5b433-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="5b433-410">I zwróć wartość NA dla każdego przypadku.</span><span class="sxs-lookup"><span data-stu-id="5b433-410">I return a value of NA for each case.</span></span> <span data-ttu-id="5b433-411">Istnieje wiele możliwości, które mogą mieć mniej efekty uboczne.</span><span class="sxs-lookup"><span data-stu-id="5b433-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="5b433-412">Można wrócić wektor wartości zerowe lub hello oryginalnego wektora wejściowych, na przykład.</span><span class="sxs-lookup"><span data-stu-id="5b433-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="5b433-413">Testy są uruchamiane na hello argumenty toohello funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="5b433-414">W każdym przypadku, jeśli zostanie wykryty błąd, zwracana jest wartość domyślna i wiadomość jest generowany przez hello `warning()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="5b433-415">Używam `warning()` zamiast `stop()` jako ostatnie hello spowoduje przerwanie wykonywania, dokładnie co próbuję tooavoid.</span><span class="sxs-lookup"><span data-stu-id="5b433-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="5b433-416">Należy pamiętać, że pismo ten kod w stylu procedurach, tak jak w przypadku tego podejścia funkcjonalności sprawiał złożone i zasłoniętej.</span><span class="sxs-lookup"><span data-stu-id="5b433-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="5b433-417">obliczenia dziennika Hello są ujęte w `tryCatch()` tak, aby wyjątki nie spowoduje zatrzymania niespodziewane tooprocessing.</span><span class="sxs-lookup"><span data-stu-id="5b433-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="5b433-418">Bez `tryCatch()` większość błędów zgłaszane przez wynik funkcji R w sygnał zatrzymania, która obsługuje tylko dla niej.</span><span class="sxs-lookup"><span data-stu-id="5b433-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="5b433-419">Wykonanie tego kodu języka R w eksperymencie i przyjrzeć się hello wydrukowaniu danych wyjściowych w pliku dane_wyjściowe.log hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="5b433-420">Teraz będą widzieć hello przekształcenia wartości hello cztery kolumny w hello dziennika, jak pokazano na rysunku 13.</span><span class="sxs-lookup"><span data-stu-id="5b433-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="5b433-421">*Rysunek 13. Podsumowanie hello przekształcenia wartości hello dataframe.*</span><span class="sxs-lookup"><span data-stu-id="5b433-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="5b433-422">Firma Microsoft Zobacz zostały przekształcone hello wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-422">We see hello values have been transformed.</span></span> <span data-ttu-id="5b433-423">Teraz mleczności znacznie przekracza wszystkich innych produktu mleczarskiego środowiska produkcyjnego, odwołując się, że teraz czekamy na skali logarytmicznej.</span><span class="sxs-lookup"><span data-stu-id="5b433-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="5b433-424">W tym momencie nasze dane jest wyczyszczone, a firma Microsoft są gotowe do niektórych modelowania.</span><span class="sxs-lookup"><span data-stu-id="5b433-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="5b433-425">Spojrzenie na powitania wizualizacji podsumowanie hello zestaw wyników danych wyjściowych z naszych [wykonanie skryptu języka R] [ execute-r-script] modułu, widoczna tam będzie kolumny "Month" hello "Categorical" 12 unikatowych wartości, ponownie, podobnie jak możemy .</span><span class="sxs-lookup"><span data-stu-id="5b433-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="5b433-426"><a id="timeseries"></a>Obiekty serie czasu i analiza korelacji</span><span class="sxs-lookup"><span data-stu-id="5b433-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="5b433-427">W tej sekcji możemy eksplorowania kilka podstawowych obiektów serii czas R i analizować hello korelacji między niektóre zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="5b433-428">Naszym celem jest toooutput dataframe zawierającego hello Pairwise — informacje o powiązaniu na kilka odchyłki.</span><span class="sxs-lookup"><span data-stu-id="5b433-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="5b433-429">Hello pełny kod R dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b433-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="5b433-430">Czas obiektów serii R</span><span class="sxs-lookup"><span data-stu-id="5b433-430">Time series objects in R</span></span>
<span data-ttu-id="5b433-431">Jak już wspomniano, czas serii są serii danych wartości indeksowane według czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="5b433-432">Obiekty serii czas R są używane toocreate i zarządzaj nimi hello czasu indeksu.</span><span class="sxs-lookup"><span data-stu-id="5b433-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="5b433-433">Ma kilka zalet toousing czasu serii obiektów.</span><span class="sxs-lookup"><span data-stu-id="5b433-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="5b433-434">Czas serii obiektów Brak hello wielu szczegółów związanych z zarządzaniem hello czasu serii indeks wartości, które znajdują się w obiekcie hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="5b433-435">Ponadto obiekty serii czasu zezwolić toouse hello wiele metod serii czas do kreślenia, drukowanie, modelowania itp.</span><span class="sxs-lookup"><span data-stu-id="5b433-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="5b433-436">Hello klasa serii czasu POSIXct to powszechnie używane i jest stosunkowo proste.</span><span class="sxs-lookup"><span data-stu-id="5b433-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="5b433-437">Ta klasa serii czasu mierzy czas od początku hello epoki hello, 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="5b433-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="5b433-438">W tym przykładzie używamy POSIXct czasu serii obiektów.</span><span class="sxs-lookup"><span data-stu-id="5b433-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="5b433-439">Inne powszechnie używane klasy obiektu serii czas R obejmują zoo i xts, szeregów czasowych rozszerzonego.</span><span class="sxs-lookup"><span data-stu-id="5b433-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="5b433-440">Przykład obiektu serii czasu</span><span class="sxs-lookup"><span data-stu-id="5b433-440">Time series object example</span></span>
<span data-ttu-id="5b433-441">Rozpocznijmy naszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5b433-441">Let's get started with our example.</span></span> <span data-ttu-id="5b433-442">Przeciągnij i upuść **nowe** [wykonanie skryptu języka R] [ execute-r-script] modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="5b433-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="5b433-443">Połącz port wyjściowy hello Dataset1 wynik istniejących hello [wykonanie skryptu języka R] [ execute-r-script] portu hello nowych danych wejściowych modułu toohello Dataset1 [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="5b433-444">Tak jak pierwszy przykłady hello, jak firma Microsoft postępu za pośrednictwem przykład Witaj, w niektórych punktach I będą wyświetlane tylko hello przyrostowe dodatkowe wiersze kodu języka R w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="5b433-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="5b433-445">Odczytywanie hello dataframe</span><span class="sxs-lookup"><span data-stu-id="5b433-445">Reading hello dataframe</span></span>
<span data-ttu-id="5b433-446">Pierwszym krokiem umożliwia odczytu w dataframe i upewnij się, że uzyskujemy hello oczekiwano wyników.</span><span class="sxs-lookup"><span data-stu-id="5b433-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="5b433-447">Witaj następujący kod należy wykonać zadania hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="5b433-448">Teraz uruchom hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-448">Now, run hello experiment.</span></span> <span data-ttu-id="5b433-449">Dziennik Hello hello nowy kształt wykonanie skryptu języka R powinien wyglądać rysunku 14.</span><span class="sxs-lookup"><span data-stu-id="5b433-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="5b433-450">*Rysunek 14. Podsumowanie dataframe hello w module wykonanie skryptu języka R hello.*</span><span class="sxs-lookup"><span data-stu-id="5b433-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="5b433-451">Te dane są hello oczekiwano typu i formatu.</span><span class="sxs-lookup"><span data-stu-id="5b433-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="5b433-452">Należy zauważyć, że kolumna "Month" hello współczynnika typu i ma hello oczekiwana liczba poziomów.</span><span class="sxs-lookup"><span data-stu-id="5b433-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="5b433-453">Tworzenie obiektów serii czasu</span><span class="sxs-lookup"><span data-stu-id="5b433-453">Creating a time series object</span></span>
<span data-ttu-id="5b433-454">Potrzebujemy tooadd dataframe tooour czasu serii obiektu.</span><span class="sxs-lookup"><span data-stu-id="5b433-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="5b433-455">Zastąp bieżący kod hello hello następujący komunikat, który dodaje kolumnę nowej klasy POSIXct.</span><span class="sxs-lookup"><span data-stu-id="5b433-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="5b433-456">Teraz Sprawdź dziennik hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-456">Now, check hello log.</span></span> <span data-ttu-id="5b433-457">Powinien on wyglądać rys. 15.</span><span class="sxs-lookup"><span data-stu-id="5b433-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="5b433-458">*Rysunek 15. Podsumowanie dataframe hello z obiektem serii czasu.*</span><span class="sxs-lookup"><span data-stu-id="5b433-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="5b433-459">Firma Microsoft może zapoznaj się z hello podsumowania tej nowej kolumny hello jest w rzeczywistości klasy POSIXct.</span><span class="sxs-lookup"><span data-stu-id="5b433-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="5b433-460">Poznawanie i przekształcanie danych hello</span><span class="sxs-lookup"><span data-stu-id="5b433-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="5b433-461">Przyjrzyjmy się niektóre zmienne hello w tym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="5b433-462">Macierz scatterplot to dobry sposób tooproduce szybko wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="5b433-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="5b433-463">Jestem I zastępowanie hello `str()` funkcji w hello poprzedni kod języka R z hello następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5b433-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="5b433-464">Uruchom ten kod i zobacz, co się stanie.</span><span class="sxs-lookup"><span data-stu-id="5b433-464">Run this code and see what happens.</span></span> <span data-ttu-id="5b433-465">kreślenia Hello w hello portu urządzenia R powinien wyglądać rysunek 16.</span><span class="sxs-lookup"><span data-stu-id="5b433-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Macierz Scatterplot wybranych zmiennych][17]

<span data-ttu-id="5b433-467">*Rysunek 16. Macierz Scatterplot wybranych zmiennych.*</span><span class="sxs-lookup"><span data-stu-id="5b433-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="5b433-468">Witaj relacji między tymi zmiennymi jest niektórych odd-looking struktury.</span><span class="sxs-lookup"><span data-stu-id="5b433-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="5b433-469">Prawdopodobnie wynika to z trendów w danych hello i hello fakt, że firma Microsoft nie ustalić hello zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="5b433-470">Analiza korelacji</span><span class="sxs-lookup"><span data-stu-id="5b433-470">Correlation analysis</span></span>
<span data-ttu-id="5b433-471">tooperform korelacji analizy potrzebujemy tooboth cofnąć trendów i standaryzowanie hello zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="5b433-472">Firma Microsoft może po prostu użyć hello R `scale()` funkcji, która koncentruje się jak również skaluje zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="5b433-473">Ta funkcja może być również szybsze.</span><span class="sxs-lookup"><span data-stu-id="5b433-473">This function might well run faster.</span></span> <span data-ttu-id="5b433-474">Jednak ma tooshow należy zapoznać się przykładem obrony programing w języku R.</span><span class="sxs-lookup"><span data-stu-id="5b433-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="5b433-475">Witaj `ts.detrend()` funkcja pokazano poniżej wykonuje obie te operacje.</span><span class="sxs-lookup"><span data-stu-id="5b433-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="5b433-476">Witaj następujące dwa wiersze kodu cofnąć tendencji hello danych i zapewnij standaryzację hello wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="5b433-477">Występuje dość bitowe w toku w hello `ts.detrend()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="5b433-478">Większość tego kodu jest wyszukiwanie potencjalnych problemów z argumentami hello lub zajmujących się wyjątki, które nadal mogą wystąpić podczas hello obliczenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="5b433-479">Tylko kilka wierszy kodu faktycznie hello obliczenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="5b433-480">Już Omówiliśmy przykład obrony Programowanie w [wartości przekształcenia](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="5b433-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="5b433-481">Zarówno bloki obliczenia są ujęte w `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="5b433-482">Niektóre błędy ułatwia oryginalnego wektora wejściowych znaczeniu tooreturn hello, a w pozostałych przypadkach wrócić wektor zer.</span><span class="sxs-lookup"><span data-stu-id="5b433-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="5b433-483">Należy pamiętać, że hello regresji liniowej używane do usuwania analizy trendów regresji serii czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="5b433-484">Zmienna predykcyjne Hello jest obiekt serii czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="5b433-485">Raz `ts.detrend()` zdefiniowano Trwa stosowanie zmiennych toohello zainteresowanie naszych dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="5b433-486">Firma Microsoft musi wymuszone hello wyświetlonej listy utworzone przez `lapply()` dataframe toodata przy użyciu `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="5b433-487">Z powodu obrony aspektów `ts.detrend()`, popraw tooprocess awarii jednej ze zmiennych hello nie zapobiega przetwarzania hello innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5b433-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="5b433-488">Witaj końcowego wiersza kodu tworzy scatterplot parowania.</span><span class="sxs-lookup"><span data-stu-id="5b433-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="5b433-489">Po uruchomieniu kodu hello R, wyniki hello hello scatterplot są wyświetlane w rysunek 17.</span><span class="sxs-lookup"><span data-stu-id="5b433-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Scatterplot parowania w szeregu czasowym cofnąć trend i standardowych][18]

<span data-ttu-id="5b433-491">*Rysunek 17. Pairwise — scatterplot szeregów czasowych cofnąć trend i standardowych.*</span><span class="sxs-lookup"><span data-stu-id="5b433-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="5b433-492">Możesz porównać te toothose wyniki pokazano na rysunku 16.</span><span class="sxs-lookup"><span data-stu-id="5b433-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="5b433-493">Z hello trend usunięte i hello zmienne standaryzowane, widzimy znacznie mniej strukturze hello relacje między tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="5b433-494">Poniżej przedstawiono Hello kodu toocompute hello korelacji jako obiekty KKS R.</span><span class="sxs-lookup"><span data-stu-id="5b433-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="5b433-495">Uruchomienie tego kodu tworzy dziennika hello pokazano na rysunku 18.</span><span class="sxs-lookup"><span data-stu-id="5b433-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="5b433-496">*Rysunek 18. Lista KKS obiektów z hello parowania korelacji analizy.*</span><span class="sxs-lookup"><span data-stu-id="5b433-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="5b433-497">Brak wartości korelacji dla każdego opóźnienie.</span><span class="sxs-lookup"><span data-stu-id="5b433-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="5b433-498">Żaden z tych wartości korelacji nie jest wystarczająco duży toobe znaczące.</span><span class="sxs-lookup"><span data-stu-id="5b433-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="5b433-499">Firma Microsoft w związku z tym stwierdzić, czy możemy modelu każdej zmiennej niezależnie.</span><span class="sxs-lookup"><span data-stu-id="5b433-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="5b433-500">Dane wyjściowe dataframe</span><span class="sxs-lookup"><span data-stu-id="5b433-500">Output a dataframe</span></span>
<span data-ttu-id="5b433-501">Firma Microsoft ma obliczana korelacji parowania hello jako listę obiektów KKS R.</span><span class="sxs-lookup"><span data-stu-id="5b433-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="5b433-502">Przedstawia nieco problem, jako hello port wyjściowy zestaw danych wyników wymaga naprawdę dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="5b433-503">Ponadto hello KKS obiekt znajduje się lista i chcemy tylko wartości hello w pierwszym elementem hello tej listy korelacji hello na powitania różnych odchyłki.</span><span class="sxs-lookup"><span data-stu-id="5b433-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="5b433-504">Witaj następującego kodu wyodrębnia hello opóźnienie wartości z listy hello KKS obiektów, które są także list.</span><span class="sxs-lookup"><span data-stu-id="5b433-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="5b433-505">pierwszy wiersz kodu Hello jest nieco trudnych, a niektóre informacje mogą pomóc w go zrozumieć.</span><span class="sxs-lookup"><span data-stu-id="5b433-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="5b433-506">Praca z hello wewnątrz limit mamy hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5b433-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="5b433-507">Witaj "**[[**"operator z argumentem hello"**1**" wybiera hello wektor korelacji w odchyłki hello z hello pierwszy element listy obiektów KKS hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="5b433-508">Witaj `do.call()` hello ma zastosowanie funkcja `rbind()` funkcja za pośrednictwem hello elementy listy hello zwraca przez `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="5b433-509">Witaj `data.frame()` funkcja wymusza traktowanie wyniku hello zwracany przez `do.call()` tooa dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="5b433-510">Należy pamiętać, że hello wiersz nazwy znajdują się w kolumnie hello dataframe.</span><span class="sxs-lookup"><span data-stu-id="5b433-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="5b433-511">W ten sposób zachowuje hello wiersz nazwy, gdy znajdują się dane wyjściowe hello [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="5b433-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="5b433-512">Wykonywanie kodu hello hello dane wyjściowe są wyświetlane w rysunek 19 podczas I **wizualizacja** hello dane wyjściowe na powitania portu wynik zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="5b433-513">Hello wiersz nazwy znajdują się w pierwszej kolumnie hello, zgodnie z założeniami.</span><span class="sxs-lookup"><span data-stu-id="5b433-513">hello row names are in hello first column, as intended.</span></span>

![Dane wyjściowe wyniki analizy korelacji hello][20]

<span data-ttu-id="5b433-515">*Rysunek 19. Dane wyjściowe z analizy korelacji hello wyniki.*</span><span class="sxs-lookup"><span data-stu-id="5b433-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="5b433-516"><a id="seasonalforecasting"></a>Przykład serii czasu: okresach prognozowania</span><span class="sxs-lookup"><span data-stu-id="5b433-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="5b433-517">Naszych danych jest teraz w postaci nadające się do analizy, a Ustaliliśmy, że nie ma żadnych znaczących korelacji między hello zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="5b433-518">Umożliwia przenoszenie na i Utwórz szeregów czasowych, funkcja prognozowania modelu.</span><span class="sxs-lookup"><span data-stu-id="5b433-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="5b433-519">Użycie tego modelu firma Microsoft będzie prognozy Kalifornijskiej mleczności dla hello 12 miesięcy 2013.</span><span class="sxs-lookup"><span data-stu-id="5b433-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="5b433-520">Nasze modelu prognozowania można używać ma dwa składniki, trend składnika i składnik okresach.</span><span class="sxs-lookup"><span data-stu-id="5b433-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="5b433-521">prognozy pełną Hello jest produktem hello te dwa składniki.</span><span class="sxs-lookup"><span data-stu-id="5b433-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="5b433-522">Ten typ modelu nosi nazwę modelu mnożenia.</span><span class="sxs-lookup"><span data-stu-id="5b433-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="5b433-523">Alternatywą Hello jest model dodatku.</span><span class="sxs-lookup"><span data-stu-id="5b433-523">hello alternative is an additive model.</span></span> <span data-ttu-id="5b433-524">Zastosowaliśmy ma zainteresowań, co sprawia, że analiza tractable zmiennych toohello przekształcania dziennika.</span><span class="sxs-lookup"><span data-stu-id="5b433-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="5b433-525">Hello pełny kod R dla tej sekcji znajduje się w pliku zip hello pobrany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b433-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="5b433-526">Tworzenie dataframe hello do analizy</span><span class="sxs-lookup"><span data-stu-id="5b433-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="5b433-527">Rozpocznij od dodania **nowe** [wykonanie skryptu języka R] [ execute-r-script] modułu tooyour eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="5b433-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="5b433-528">Połącz hello **zestaw wyników danych** dane wyjściowe istniejących hello [wykonanie skryptu języka R] [ execute-r-script] toohello modułu **Dataset1** wejściowych hello nowego modułu.</span><span class="sxs-lookup"><span data-stu-id="5b433-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="5b433-529">wynik Hello powinien wyglądać jak rysunek 20.</span><span class="sxs-lookup"><span data-stu-id="5b433-529">hello result should look something like Figure 20.</span></span>

![Witaj eksperymentować hello dodany nowy moduł wykonanie skryptu języka R][21]

<span data-ttu-id="5b433-531">*Rysunek 20. Witaj eksperymentować hello dodany nowy moduł wykonanie skryptu języka R.*</span><span class="sxs-lookup"><span data-stu-id="5b433-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="5b433-532">Jako hello korelacji analizy, które firma Microsoft właśnie został ukończony, potrzebujemy tooadd kolumny z obiektem POSIXct czasu serii.</span><span class="sxs-lookup"><span data-stu-id="5b433-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="5b433-533">Witaj następującego kodu będzie w tym właśnie.</span><span class="sxs-lookup"><span data-stu-id="5b433-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="5b433-534">Uruchom ten kod i przyjrzyj się hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="5b433-534">Run this code and look at hello log.</span></span> <span data-ttu-id="5b433-535">wynik Hello powinien wyglądać rysunek 21.</span><span class="sxs-lookup"><span data-stu-id="5b433-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="5b433-536">*Rysunek 21. Podsumowanie hello dataframe.*</span><span class="sxs-lookup"><span data-stu-id="5b433-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="5b433-537">Z tym wynikiem są nam gotowe toostart nasze analizy.</span><span class="sxs-lookup"><span data-stu-id="5b433-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="5b433-538">Tworzenie zestawu danych szkolenia</span><span class="sxs-lookup"><span data-stu-id="5b433-538">Create a training dataset</span></span>
<span data-ttu-id="5b433-539">Z dataframe hello skonstruowany potrzebujemy toocreate zestawu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="5b433-540">Te dane będzie zawierać wszystkie hello uwag, z wyjątkiem hello ostatnie 12 hello roku 2013, czyli naszego zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="5b433-541">następujące Hello kodu dataframe hello podzestawy i tworzy powierzchni hello mleczarskich zmiennych produkcyjnego i ceny.</span><span class="sxs-lookup"><span data-stu-id="5b433-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="5b433-542">Utworzyć następnie powierzchni hello produkcyjnego i cen zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5b433-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="5b433-543">Funkcji anonimowej jest używane toodefine niektórych wspomaga dla powierzchni, a następnie iteracja hello lista hello innych dwa argumenty z `Map()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="5b433-544">Jeśli myślisz, że dla pętli będą działały prawidłowo w tym miejscu, są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="5b433-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="5b433-545">Jednak ponieważ funkcjonalności języka R I am zastosowania podejścia funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="5b433-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="5b433-546">Wykonywanie kodu hello tworzy hello serii szeregów czasowych geograficzne z danych wyjściowych urządzenia R hello pokazano na rysunku 22.</span><span class="sxs-lookup"><span data-stu-id="5b433-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="5b433-547">Należy pamiętać, że tej osi czasu hello jest wyrażona w jednostkach dat, nieuprzywilejowany korzyści czasu hello metody kreślenia serii.</span><span class="sxs-lookup"><span data-stu-id="5b433-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Pierwszy z serii wykresy czasu Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Sekundy czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Innych czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Czwarta czasu serii wykresów Kalifornijskiej mleczarskich danych produkcyjnych i cen](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="5b433-552">*Rysunek 22. Czas serii wykresów mleczarskie Kalifornijskiej i cen danych.*</span><span class="sxs-lookup"><span data-stu-id="5b433-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="5b433-553">Wzór trendu</span><span class="sxs-lookup"><span data-stu-id="5b433-553">A trend model</span></span>
<span data-ttu-id="5b433-554">Wytworzeniu obiektów serie czasu i o przyjrzeliśmy danych hello, Zacznijmy tooconstruct wzór trendu hello danych produkcyjnych mleka Polski.</span><span class="sxs-lookup"><span data-stu-id="5b433-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="5b433-555">Można to zrobić dzięki regresji serii czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-555">We can do this with a time series regression.</span></span> <span data-ttu-id="5b433-556">Jednak jest jasno z hello kreślenia czy firma Microsoft będzie konieczne więcej niż tooaccurately nachylenie i punkt przecięcia modelu hello obserwowanych trendów w danych szkoleniowych hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="5b433-557">Podana hello małą skalę hello danych, I będzie kompilacji hello wzór trendu w programu RStudio i następnie wycinanie i wklejanie modelu wynikowego hello do usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5b433-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="5b433-558">Programu RStudio zapewnia interaktywne środowisko dla tego typu analizy interakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="5b433-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="5b433-559">Jako pierwsza próba I ponowi wielomianu regresji uprawnienia się too3.</span><span class="sxs-lookup"><span data-stu-id="5b433-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="5b433-560">Brak rzeczywistych niebezpieczeństwo nadmiernie dopasowanie tych rodzajów modeli.</span><span class="sxs-lookup"><span data-stu-id="5b433-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="5b433-561">W związku z tym jest najlepszym tooavoid najwyższego rzędu warunki.</span><span class="sxs-lookup"><span data-stu-id="5b433-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="5b433-562">Hello `I()` funkcja zapobiega interpretacji hello treści (interpretuje hello zawartość "jak jest") i umożliwia toowrite dosłownie interpretowany funkcja równanie regresji.</span><span class="sxs-lookup"><span data-stu-id="5b433-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="5b433-563">Spowoduje to wygenerowanie hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5b433-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="5b433-564">Z wartości P (Pr (> | t |)) w tym danych wyjściowych widać, że hello kwadratów termin nie może być istotne.</span><span class="sxs-lookup"><span data-stu-id="5b433-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="5b433-565">Będę używać hello `update()` funkcji toomodify tego modelu przez usunięcie hello kwadrat terminu.</span><span class="sxs-lookup"><span data-stu-id="5b433-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="5b433-566">Spowoduje to wygenerowanie hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5b433-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="5b433-567">To wygląda lepiej.</span><span class="sxs-lookup"><span data-stu-id="5b433-567">This looks better.</span></span> <span data-ttu-id="5b433-568">Wszystkie warunki hello są istotne.</span><span class="sxs-lookup"><span data-stu-id="5b433-568">All of hello terms are significant.</span></span> <span data-ttu-id="5b433-569">Jednak wartość 2e 16 hello wartości domyślnej i nie powinny być pobierane za poważnie.</span><span class="sxs-lookup"><span data-stu-id="5b433-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="5b433-570">Jako test związane z poprawnością upewnijmy wykres serii czasu hello Kalifornijskiej mleczarskie danych z krzywej trend hello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="5b433-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="5b433-571">Po dodaniu hello następującego kodu w hello Azure Machine Learning [wykonanie skryptu języka R] [ execute-r-script] toocreate modelu (nie programu RStudio) hello modelu i utworzyć wykres.</span><span class="sxs-lookup"><span data-stu-id="5b433-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="5b433-572">wynik Hello jest wyświetlany na rysunku 23.</span><span class="sxs-lookup"><span data-stu-id="5b433-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Danych produkcyjnych mleka Kalifornijskiej z modelem trend pokazano](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="5b433-574">*Rysunek 23. Polski mleka danych produkcyjnych z modelem trend wyświetlane.*</span><span class="sxs-lookup"><span data-stu-id="5b433-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="5b433-575">Wygląda na to, dość dobrze dopasowania modelu trend hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="5b433-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="5b433-576">Ponadto nie wydaje dowód toobe uwierzytelniając odpowiadający takie jak nietypowych wierci się hello krzywej modelu.</span><span class="sxs-lookup"><span data-stu-id="5b433-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="5b433-577">Okresach modelu</span><span class="sxs-lookup"><span data-stu-id="5b433-577">Seasonal model</span></span>
<span data-ttu-id="5b433-578">Z modelem trendu w ręcznie firma Microsoft musi mieć toopush na i zawiera efekty okresach hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="5b433-579">Używamy hello miesiąc roku hello jako zmienną fikcyjny obowiązują hello model liniowy toocapture hello kolejnych miesięcy.</span><span class="sxs-lookup"><span data-stu-id="5b433-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="5b433-580">Należy pamiętać, że podczas wprowadzania współczynnik zmiennych do modelu, hello intercept musi nie można obliczyć.</span><span class="sxs-lookup"><span data-stu-id="5b433-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="5b433-581">Jeśli nie jest to zrobić, formuła hello jest nadmiernie określonego i R spowoduje porzucenie jedną hello potrzeby czynników, ale zachować hello intercept terminu.</span><span class="sxs-lookup"><span data-stu-id="5b433-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="5b433-582">Ponieważ mamy modelu zadowalające trend możemy użyć hello `update()` hello tooadd funkcja nowe warunki toohello istniejącego modelu.</span><span class="sxs-lookup"><span data-stu-id="5b433-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="5b433-583">Hello -1 w formule aktualizacji hello porzuca hello intercept terminu.</span><span class="sxs-lookup"><span data-stu-id="5b433-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="5b433-584">Kontynuowanie w programu RStudio chwili hello:</span><span class="sxs-lookup"><span data-stu-id="5b433-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="5b433-585">Spowoduje to wygenerowanie hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5b433-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="5b433-586">Widzimy modelu hello już ma termin przechwycenia i ma 12 miesiąca istotne czynniki.</span><span class="sxs-lookup"><span data-stu-id="5b433-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="5b433-587">Jest to dokładnie co możemy toosee.</span><span class="sxs-lookup"><span data-stu-id="5b433-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="5b433-588">Można wprowadzić inny czas serii wykresu hello Kalifornijskiej mleczarskie danych toosee jak działa hello okresach modelu.</span><span class="sxs-lookup"><span data-stu-id="5b433-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="5b433-589">Po dodaniu hello następującego kodu w hello Azure Machine Learning [wykonanie skryptu języka R] [ execute-r-script] toocreate hello modelu i utworzyć wykres.</span><span class="sxs-lookup"><span data-stu-id="5b433-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="5b433-590">Uruchomienie tego kodu w usłudze Azure Machine Learning tworzy wykres hello pokazano na rysunku 24.</span><span class="sxs-lookup"><span data-stu-id="5b433-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Polski mleczności z modelu w tym okresach efekty](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="5b433-592">*Rysunek 24. Polski mleczności z modelu w tym okresach efekty.*</span><span class="sxs-lookup"><span data-stu-id="5b433-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="5b433-593">Hello jest raczej wspieranie danych dopasowania toohello pokazano na rysunku 24.</span><span class="sxs-lookup"><span data-stu-id="5b433-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="5b433-594">Wygląd uzasadnione zarówno hello trend, jak i efekt okresach hello (odmiany miesięczne).</span><span class="sxs-lookup"><span data-stu-id="5b433-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="5b433-595">Kolejny test na nasz model umożliwia również przyjrzeć się reszty hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="5b433-596">Hello następujące oblicza kod hello przewidywane wartości z naszych dwa modele, oblicza reszty hello hello okresach modelu i następnie geograficzne pozostałości te hello danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="5b433-597">pozostałe kreślenia Hello jest wyświetlany w 25 rysunku.</span><span class="sxs-lookup"><span data-stu-id="5b433-597">hello residual plot is shown in Figure 25.</span></span>

![Reszty hello okresach modelu dla danych szkoleniowych hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="5b433-599">*Rysunek 25. Reszty hello okresach modelu dla danych szkoleniowych hello.*</span><span class="sxs-lookup"><span data-stu-id="5b433-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="5b433-600">Te składniki resztkowe Szukaj uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="5b433-600">These residuals look reasonable.</span></span> <span data-ttu-id="5b433-601">Brak określonej struktury, jednak uwzględnione hello recesji hello 2008 2009, które bez uwzględnienia nasz model szczególnie dobrze.</span><span class="sxs-lookup"><span data-stu-id="5b433-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="5b433-602">pokazano na rysunku 25 kreślenia Hello przydaje się do wykrywania wszelkich wzorce zależnych od czasu w reszty hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="5b433-603">jawne podejście Hello przetwarzania i kreślenia reszty hello, I używać miejsc reszty hello w kolejności czasu na powierzchni hello.</span><span class="sxs-lookup"><span data-stu-id="5b433-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="5b433-604">Jeśli na powitania drugiej strony I ma wykreślić `milk.lm$residuals`, kreślenia hello nie była w kolejności czasu.</span><span class="sxs-lookup"><span data-stu-id="5b433-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="5b433-605">Można również użyć `plot.lm()` tooproduce serii wykresów diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="5b433-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="5b433-606">Ten kod tworzy serii wykresów diagnostycznych pokazano na rysunku 26.</span><span class="sxs-lookup"><span data-stu-id="5b433-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Pierwszy diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Drugi powierzchni diagnostycznych dla modelu okresach hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Trzecia diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Czwarta diagnostycznych powierzchni hello okresach modelu](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="5b433-611">*Rysunek 26. Diagnostyka geograficzne hello okresach modelu.*</span><span class="sxs-lookup"><span data-stu-id="5b433-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="5b433-612">Istnieje kilka punktów wysokiej znaczenie zidentyfikowany w tych powierzchni, ale nie toocause nas bardzo ważne.</span><span class="sxs-lookup"><span data-stu-id="5b433-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="5b433-613">Ponadto możemy stwierdzić, z hello normalny Q-Q kreślenia czy reszty hello Zamknij toonormally rozproszonych, ważne założeń modeli liniowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="5b433-614">Ocena prognozowania i modelu</span><span class="sxs-lookup"><span data-stu-id="5b433-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="5b433-615">Istnieje tylko jeden więcej toocomplete toodo operacją naszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5b433-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="5b433-616">Firma Microsoft konieczne toocompute prognozy i pomiar błąd hello względem hello rzeczywiste dane.</span><span class="sxs-lookup"><span data-stu-id="5b433-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="5b433-617">Nasze prognozy będą hello 12 miesięcy 2013.</span><span class="sxs-lookup"><span data-stu-id="5b433-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="5b433-618">Firma Microsoft może obliczeniowe miary błąd dla tych danych rzeczywistych toohello prognozy, który nie jest częścią naszego zestawu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="5b433-619">Ponadto firma Microsoft porównanie wydajności na powitania 18 lat toohello danych szkoleniowych 12 miesięcy od danych testowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="5b433-620">Używane są liczby metryk wydajności hello toomeasure modeli szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="5b433-621">W tym przypadku użyjemy hello błędu głównego średniej kwadratowej (RMS).</span><span class="sxs-lookup"><span data-stu-id="5b433-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="5b433-622">Witaj następująca funkcja oblicza błąd hello RMS między dwóch serii.</span><span class="sxs-lookup"><span data-stu-id="5b433-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="5b433-623">Jak hello `log.transform()` funkcja omówiono w Witaj "Wartość przekształcenia" sekcji, jest bardzo dużo kod błędu sprawdzania i wyjątków odzyskiwania w tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b433-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="5b433-624">zastosować zasady Hello są hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="5b433-624">hello principles employed are hello same.</span></span> <span data-ttu-id="5b433-625">Witaj praca odbywa się w dwóch miejscach w `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="5b433-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="5b433-626">Najpierw szeregów czasowych hello są exponentiated, ponieważ firma Microsoft odbywała się wcześniej Praca z dziennikami hello hello wartości.</span><span class="sxs-lookup"><span data-stu-id="5b433-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="5b433-627">Po drugie błędu RMS hello jest kolumną obliczaną.</span><span class="sxs-lookup"><span data-stu-id="5b433-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="5b433-628">Załóżmy wyposażony hello toomeasure funkcja błędu RMS, kompilacji i wyjściowych dataframe, zawierające błędy hello usługi RMS.</span><span class="sxs-lookup"><span data-stu-id="5b433-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="5b433-629">Firma Microsoft będzie zawierać warunki dla samego modelu trend hello i hello pełny model o okresach czynników.</span><span class="sxs-lookup"><span data-stu-id="5b433-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="5b433-630">Witaj następujący kod hello zadania przy użyciu hello dwa liniowej modele, które firma Microsoft ma być skonstruowany.</span><span class="sxs-lookup"><span data-stu-id="5b433-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="5b433-631">Uruchomienie tego kodu generuje hello dane wyjściowe pokazano rysunek 27 na powitania port wyjściowy zestaw danych z wyników.</span><span class="sxs-lookup"><span data-stu-id="5b433-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Porównanie usług RMS błędów dla modeli hello][26]

<span data-ttu-id="5b433-633">*Rysunek 27. Porównanie błędy usług RMS dla modeli hello.*</span><span class="sxs-lookup"><span data-stu-id="5b433-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="5b433-634">Z tymi wynikami widzimy, że dodawanie hello okresach czynniki toohello model zmniejsza błędu RMS hello znacznie.</span><span class="sxs-lookup"><span data-stu-id="5b433-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="5b433-635">Nie za zaskakująco hello RMS błąd hello szkolenia danych bit jest mniejsza niż dla hello prognozy.</span><span class="sxs-lookup"><span data-stu-id="5b433-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="5b433-636"><a id="appendixa"></a>Dodatek A: Przewodnik tooRStudio</span><span class="sxs-lookup"><span data-stu-id="5b433-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="5b433-637">Programu RStudio jest bardzo dobrze udokumentowane, więc w tym dodatku I zapewni niektórych toohello łącza kluczowe sekcje tooget dokumentacji programu RStudio hello, uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="5b433-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="5b433-638">Tworzenie projektów</span><span class="sxs-lookup"><span data-stu-id="5b433-638">Creating projects</span></span>
   
   <span data-ttu-id="5b433-639">Można porządkować i zarządzać kodem R do projektów przy użyciu programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="5b433-640">w dokumentacji Hello używa projektów znajduje się w temacie https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="5b433-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="5b433-641">Najlepiej wykonać te kroki, a następnie utwórz projekt hello R przykłady kodu w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="5b433-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="5b433-642">Edytowanie i wykonywanie kodu języka R</span><span class="sxs-lookup"><span data-stu-id="5b433-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="5b433-643">Programu RStudio zapewnia zintegrowane środowisko umożliwiające edytowanie i wykonywanie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="5b433-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="5b433-644">Dokumentację można znaleźć w https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="5b433-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="5b433-645">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="5b433-645">Debugging</span></span>
   
   <span data-ttu-id="5b433-646">Programu RStudio obejmuje zaawansowane możliwości debugowania.</span><span class="sxs-lookup"><span data-stu-id="5b433-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="5b433-647">Dokumentacja dla tych funkcji jest na https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="5b433-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="5b433-648">funkcje rozwiązywania punktu przerwania Hello są udokumentowane w https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="5b433-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="5b433-649"><a id="appendixb"></a>Dodatek B: Dalsze informacje.</span><span class="sxs-lookup"><span data-stu-id="5b433-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="5b433-650">R, ten samouczek obejmuje hello podstawy programowania z jakich należy toouse hello języka R w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5b433-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="5b433-651">Jeśli nie masz doświadczenia w obsłudze R, dwie instrukcje są dostępne w sieci CRAN:</span><span class="sxs-lookup"><span data-stu-id="5b433-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="5b433-652">R dla początkujących przez Emmanuel Paradis jest toostart dobrym miejscem, w http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="5b433-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="5b433-653">TooR wprowadzenie przez W. N.</span><span class="sxs-lookup"><span data-stu-id="5b433-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="5b433-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="5b433-654">Venables et.</span></span> <span data-ttu-id="5b433-655">Al.</span><span class="sxs-lookup"><span data-stu-id="5b433-655">al.</span></span> <span data-ttu-id="5b433-656">Przechodzi nieco bardziej szczegółowo w http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="5b433-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="5b433-657">Istnieje wiele — książki na R, które mogą pomóc Ci rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="5b433-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="5b433-658">Poniżej przedstawiono kilka, które mogę być przydatne:</span><span class="sxs-lookup"><span data-stu-id="5b433-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="5b433-659">Witaj grafikę programowania R: A samouczek z oprogramowania statystycznie przez Matloff Normanowi jest tooprogramming znakomity wprowadzenie w języku R.</span><span class="sxs-lookup"><span data-stu-id="5b433-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="5b433-660">R Cookbook przez Teetor Pawła zapewnia problemu i rozwiązanie podejście toousing R.</span><span class="sxs-lookup"><span data-stu-id="5b433-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="5b433-661">R w akcji Robert Kabacoff jest innym przydatne książki wstępne.</span><span class="sxs-lookup"><span data-stu-id="5b433-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="5b433-662">Hello pomocnika szybkie R witryny sieci Web jest zasobem przydatne w http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="5b433-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="5b433-663">R Inferno przez oparzenia Patrick jest zaskakująco żartobliwy książki, która zajmuje się liczbę trudnych i trudne tematy, które mogą wystąpić, gdy Programowanie w książce R. hello jest dostępny bezpłatnie na http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="5b433-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="5b433-664">Jeśli chcesz nowości w zaawansowanych tematów w R mają wygląd książki hello zaawansowane R przez Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="5b433-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="5b433-665">Witaj wersję online tego podręcznika jest dostępny bezpłatnie na http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="5b433-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="5b433-666">Katalog R czasu serii pakietów można znaleźć w hello widoku zadań sieci CRAN do analizy serii czasowych: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="5b433-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="5b433-667">Informacje w określonym czasie serii obiektu pakietów należy zapoznać się toohello dokumentacji dla tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="5b433-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="5b433-668">Książka Hello wprowadzające szeregu czasowego z R Cowpertwait Pawła i Andrew Metcalfe zawiera R toousing wprowadzenie do analizy serii czasowych.</span><span class="sxs-lookup"><span data-stu-id="5b433-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="5b433-669">Wiele więcej teoretycznego teksty zawierają przykłady R.</span><span class="sxs-lookup"><span data-stu-id="5b433-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="5b433-670">Niektóre dużą zasobów internetowych:</span><span class="sxs-lookup"><span data-stu-id="5b433-670">Some great internet resources:</span></span>

* <span data-ttu-id="5b433-671">DataCamp: DataCamp szkoleniowcem R wygodna hello przeglądarki z lekcje wideo i kodowania ćwiczeń.</span><span class="sxs-lookup"><span data-stu-id="5b433-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="5b433-672">Brak interaktywnych samouczków na powitania najnowsze techniki R i pakietów.</span><span class="sxs-lookup"><span data-stu-id="5b433-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="5b433-673">Podjęcie wolnego interaktywnego samouczka R hello na https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="5b433-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="5b433-674">Przewodnik po uzyskiwanie uruchomiony z R z Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="5b433-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="5b433-675">Zawiera krótki samouczek R przez czarne Kelly z http://www.cyclismo.org/tutorial/R/ Clarkson University</span><span class="sxs-lookup"><span data-stu-id="5b433-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="5b433-676">R zasobów 60 + wymienionych w http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="5b433-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
