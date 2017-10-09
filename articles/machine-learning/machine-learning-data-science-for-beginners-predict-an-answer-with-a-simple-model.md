---
title: "aaaPredict odpowiedzi z modelu regresji proste — usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toocreate regresji prosty model toopredict cen w nauce danych dla początkujących 4 wideo. Obejmuje regresji liniowej z danych docelowych."
keywords: Tworzenie modelu, modelu prostego, prognozowanie cen, model regresji proste
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="fb5d4-105">Prognozowanie odpowiedzi za pomocą prostego modelu</span><span class="sxs-lookup"><span data-stu-id="fb5d4-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="fb5d4-106">Wideo 4: Nauki danych serii dla początkujących</span><span class="sxs-lookup"><span data-stu-id="fb5d4-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="fb5d4-107">Dowiedz się, jak toocreate toopredict modelu regresji proste hello cen romb w nauce danych dla początkujących 4 wideo.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-107">Learn how toocreate a simple regression model toopredict hello price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="fb5d4-108">Firma Microsoft będzie Rysuj modelu regresji z danych docelowych.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="fb5d4-109">Witaj tooget wykorzystanie serii hello, obejrzyj je wszystkie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="fb5d4-110">[Przejdź do listy toohello filmów wideo](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="fb5d4-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="fb5d4-111">Inne pliki wideo w tej serii</span><span class="sxs-lookup"><span data-stu-id="fb5d4-111">Other videos in this series</span></span>
<span data-ttu-id="fb5d4-112">*Nauki danych dla początkujących* to nauka toodata szybkie wprowadzenie w pięciu krótkie wideo.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="fb5d4-113">Wideo 1: [danych nauki odpowiedzi na pytania hello 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="fb5d4-114">Wideo 2: [jest gotowy do analizy danych danych?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="fb5d4-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="fb5d4-115">*(4 s 56 min)*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="fb5d4-116">Wideo 3: [Zadaj pytanie może odpowiedzieć z danymi](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 s 17 min)*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="fb5d4-117">Wideo 4: Odpowiedź z prostego modelu prognozowania</span><span class="sxs-lookup"><span data-stu-id="fb5d4-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="fb5d4-118">Wideo 5: [skopiować inne osoby pracy toodo danych nauki](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-118">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="fb5d4-119">Zapis: Przewidywanie odpowiedzi z modelu prostego</span><span class="sxs-lookup"><span data-stu-id="fb5d4-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="fb5d4-120">Zapraszamy toohello czwarty wideo w serii "Danych nauki dla początkujących" hello.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-120">Welcome toohello fourth video in hello "Data Science for Beginners" series.</span></span> <span data-ttu-id="fb5d4-121">W tym przypadku firma Microsoft budowanie prostego modelu i prognozowanie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="fb5d4-122">A *modelu* jest uproszczone artykuł o naszych danych.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="fb5d4-123">Będzie można wyświetlić I znaczenie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="fb5d4-124">Zbieranie odpowiednich, dokładne, połączenie, jest za mało danych</span><span class="sxs-lookup"><span data-stu-id="fb5d4-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="fb5d4-125">Załóżmy, że chcę tooshop romb.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-125">Say I want tooshop for a diamond.</span></span> <span data-ttu-id="fb5d4-126">Mam pierścień, który należał babcia toomy z ustawieniem dla romb 1.35 karatach i ma tooget informacje o tym, jaki będzie koszt.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-126">I have a ring that belonged toomy grandmother with a setting for a 1.35 carat diamond, and I want tooget an idea of how much it will cost.</span></span> <span data-ttu-id="fb5d4-127">I uwzględniać Notatnik i pióra hello biżuteria magazynu i I Zanotuj cen hello wszystkich karo hello w przypadku hello i ile porównać w carats.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-127">I take a notepad and pen into hello jewelry store, and I write down hello price of all of hello diamonds in hello case and how much they weigh in carats.</span></span> <span data-ttu-id="fb5d4-128">Począwszy od pierwszego romb hello - carats 1.01 jego i 7,366 $.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-128">Starting with hello first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="fb5d4-129">Teraz przejdź i wykonaj dla wszystkich hello innych diamentów w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-129">Now I go through and do this for all hello other diamonds in hello store.</span></span>

![Kolumny danych romb](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="fb5d4-131">Zwróć uwagę, że naszej listy ma dwie kolumny.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-131">Notice that our list has two columns.</span></span> <span data-ttu-id="fb5d4-132">Każda kolumna ma inny atrybut — wagę carats i cen — oraz każdy wiersz jest pojedynczego punktu danych reprezentujący pojedynczego romb.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="fb5d4-133">Faktycznie utworzyliśmy małą tutaj — zestawu danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="fb5d4-134">Zwróć uwagę, że spełnia kryteriów jakości:</span><span class="sxs-lookup"><span data-stu-id="fb5d4-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="fb5d4-135">dane Hello są **odpowiednich** -waga jest ostatecznie powiązanych tooprice</span><span class="sxs-lookup"><span data-stu-id="fb5d4-135">hello data is **relevant** - weight is definitely related tooprice</span></span>
* <span data-ttu-id="fb5d4-136">Ma ona **dokładne** -możemy dokładnie sprawdzone ceny hello możemy zapisać</span><span class="sxs-lookup"><span data-stu-id="fb5d4-136">It's **accurate** - we double-checked hello prices that we write down</span></span>
* <span data-ttu-id="fb5d4-137">Ma ona **połączone** — istnieją nie spacji w dowolnej z tych kolumn</span><span class="sxs-lookup"><span data-stu-id="fb5d4-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="fb5d4-138">I jak zajmiemy się tym, ma **za mało** tooanswer danych naszych zapytania</span><span class="sxs-lookup"><span data-stu-id="fb5d4-138">And, as we'll see, it's **enough** data tooanswer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="fb5d4-139">Zadaj pytanie sharp</span><span class="sxs-lookup"><span data-stu-id="fb5d4-139">Ask a sharp question</span></span>
<span data-ttu-id="fb5d4-140">Obecnie firma Microsoft będzie stanowić naszych zapytania w sposób sharp: "jaka będzie koszt toobuy romb karatach 1.35?"</span><span class="sxs-lookup"><span data-stu-id="fb5d4-140">Now we'll pose our question in a sharp way: "How much will it cost toobuy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="fb5d4-141">Naszej listy nie ma romb 1.35 karatach, dlatego firma Microsoft zapewnia toouse hello reszty tooget naszych danych toohello odpowiedzi na pytanie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have toouse hello rest of our data tooget an answer toohello question.</span></span>

## <a name="plot-hello-existing-data"></a><span data-ttu-id="fb5d4-142">Wykreślenia hello istniejących danych</span><span class="sxs-lookup"><span data-stu-id="fb5d4-142">Plot hello existing data</span></span>
<span data-ttu-id="fb5d4-143">Witaj najpierw robimy jest poziomej linii numer o nazwie osi toochart hello wagi.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-143">hello first thing we'll do is draw a horizontal number line, called an axis, toochart hello weights.</span></span> <span data-ttu-id="fb5d4-144">Hello zakres wag hello jest 0 too2, dlatego firma Microsoft będzie rysowanie linii obejmujący zakresu i umieścić znaczniki dla każdego połowa karatach.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-144">hello range of hello weights is 0 too2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="fb5d4-145">Następnie firma Microsoft będzie rysowanie cenę hello toorecord osi pionowej i podłącz go osi poziomej wagi toohello.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-145">Next we'll draw a vertical axis toorecord hello price and connect it toohello horizontal weight axis.</span></span> <span data-ttu-id="fb5d4-146">Są to w jednostkach kwoty.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-146">This will be in units of dollars.</span></span> <span data-ttu-id="fb5d4-147">Teraz mamy zestaw współrzędnych osi.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-147">Now we have a set of coordinate axes.</span></span>

![Osie wagi i cen](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="fb5d4-149">Firma Microsoft jest tootake będzie teraz te dane i wyłączyć go do *wykres punktowy*.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-149">We're going tootake this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="fb5d4-150">Jest to liczbowe zestawów danych doskonały sposób toovisualize.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-150">This is a great way toovisualize numerical data sets.</span></span>

<span data-ttu-id="fb5d4-151">Dla pierwszego punktu danych hello możemy eyeball pionowych linii w 1.01 carats.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-151">For hello first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="fb5d4-152">Następnie możemy eyeball poziomych linii w 7,366 $.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="fb5d4-153">Jeżeli spełniają one możemy zwrócić kropką.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="fb5d4-154">Reprezentuje naszym pierwszym romb.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-154">This represents our first diamond.</span></span>

<span data-ttu-id="fb5d4-155">Teraz możemy przejść przez każdego romb na tej liście i hello samo.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-155">Now we go through each diamond on this list and do hello same thing.</span></span> <span data-ttu-id="fb5d4-156">Kiedy jesteśmy za pośrednictwem jest będziemy mieć: licznych kropkami, jeden dla każdej romb.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![Wykres punktowy](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a><span data-ttu-id="fb5d4-158">Rysuj modelu hello hello punktów danych</span><span class="sxs-lookup"><span data-stu-id="fb5d4-158">Draw hello model through hello data points</span></span>
<span data-ttu-id="fb5d4-159">Teraz można spojrzeć na powitania kropki i squint kolekcji hello wygląda jak linia fat, rozmytego.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-159">Now if you look at hello dots and squint, hello collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="fb5d4-160">Możemy zająć naszych znacznika i rysowanie linii prostej za jego pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="fb5d4-161">Za pomocą rysowania linii, utworzyliśmy *modelu*.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="fb5d4-162">Należy traktować jako biorąc Witaj świecie rzeczywistym i wersji simplistic kreskówki go.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-162">Think of this as taking hello real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="fb5d4-163">Teraz kreskówki hello jest nieprawidłowy — hello wiersza nie jest akceptowana wszystkich hello punktów danych.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-163">Now hello cartoon is wrong - hello line doesn't go through all hello data points.</span></span> <span data-ttu-id="fb5d4-164">Jednak jest przydatne uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-164">But, it's a useful simplification.</span></span>

![Regresji liniowej](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="fb5d4-166">Witaj fakt, że kropki hello nie przechodzą dokładnie wiersza hello jest OK.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-166">hello fact that all hello dots don't go exactly through hello line is OK.</span></span> <span data-ttu-id="fb5d4-167">Analityków danych opisano to przez informujący model hello - wiersza hello —, a następnie każdego punktu ma niektóre *szumu* lub *wariancji* skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-167">Data scientists explain this by saying that there's hello model - that's hello line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="fb5d4-168">Brak hello doskonałe relacji podstawowej i oznacza to, że Witaj świecie do obsługi niepowtarzalne, rzeczywista dodające szumu i niedokładność.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-168">There's hello underlying perfect relationship, and then there's hello gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="fb5d4-169">Ponieważ próbujemy pytanie hello tooanswer *ile?* jest to *regresji*.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-169">Because we're trying tooanswer hello question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="fb5d4-170">I dlatego firma Microsoft korzysta z prostej, jest *regresji liniowej*.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-hello-model-toofind-hello-answer"></a><span data-ttu-id="fb5d4-171">Użyj hello modelu toofind hello odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fb5d4-171">Use hello model toofind hello answer</span></span>
<span data-ttu-id="fb5d4-172">Teraz mamy modelu i poprosimy go naszych pytanie: jaka będzie romb 1.35 karatach koszt?</span><span class="sxs-lookup"><span data-stu-id="fb5d4-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="fb5d4-173">tooanswer nasze pytanie, możemy oka 1.35 carats i rysowanie linii pionowej.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-173">tooanswer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="fb5d4-174">W przypadku, gdy jego przecina hello modelu wiersza, firma Microsoft eyeball osią linia pozioma toohello dolara ($).</span><span class="sxs-lookup"><span data-stu-id="fb5d4-174">Where it crosses hello model line, we eyeball a horizontal line toohello dollar axis.</span></span> <span data-ttu-id="fb5d4-175">Trafienia jego prawej strony na 10 000.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-175">It hits right at 10,000.</span></span> <span data-ttu-id="fb5d4-176">Wysięgnik!</span><span class="sxs-lookup"><span data-stu-id="fb5d4-176">Boom!</span></span> <span data-ttu-id="fb5d4-177">To już odpowiedzi hello: romb 1.35 karatach koszty około 10 000.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-177">That's hello answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Znajdź odpowiedzi hello na powitania modelu](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="fb5d4-179">Utwórz przedział ufności</span><span class="sxs-lookup"><span data-stu-id="fb5d4-179">Create a confidence interval</span></span>
<span data-ttu-id="fb5d4-180">Jest fizyczną toowonder jak ta prognozy są dokładne.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-180">It's natural toowonder how precise this prediction is.</span></span> <span data-ttu-id="fb5d4-181">Jest przydatne tooknow czy romb 1.35 karatach hello będą bardzo Zamknij za 10 000 lub wiele większej lub mniejszej.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-181">It's useful tooknow whether hello 1.35 carat diamond will be very close too$10,000, or a lot higher or lower.</span></span> <span data-ttu-id="fb5d4-182">toofigure tego, umożliwia rysowanie koperty wokół hello regresji wiersz, który zawiera większość hello kropek.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-182">toofigure this out, let's draw an envelope around hello regression line that includes most of hello dots.</span></span> <span data-ttu-id="fb5d4-183">Ten koperty jest wywoływana naszych *przedział ufności*: jest dość pewność, że ceny mieszczą się w tym koperty, ponieważ w przeszłości hello większość z nich.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in hello past most of them have.</span></span> <span data-ttu-id="fb5d4-184">Firma Microsoft Rysuj dwóch więcej poziome linie, z których wiersza 1.35 karatach hello przecina hello górny i dolny hello tego koperty protokołu.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-184">We can draw two more horizontal lines from where hello 1.35 carat line crosses hello top and hello bottom of that envelope.</span></span>

![Przedział ufności](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="fb5d4-186">Teraz możemy powiedzieć coś o naszych przedział ufności: możemy powiedzieć bez obaw czy cena hello romb 1.35 karatach jest około $ 10 000 -, ale może być możliwie jak $8000 i może być możliwie jak 12 000.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-186">Now we can say something about our confidence interval:  We can say confidently that hello price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="fb5d4-187">Skończymy, bez matematyczne lub komputerów</span><span class="sxs-lookup"><span data-stu-id="fb5d4-187">We're done, with no math or computers</span></span>
<span data-ttu-id="fb5d4-188">Robiliśmy, jakie analityków danych uzyskać płatną toodo i robiliśmy tylko za pomocą rysowania:</span><span class="sxs-lookup"><span data-stu-id="fb5d4-188">We did what data scientists get paid toodo, and we did it just by drawing:</span></span>

* <span data-ttu-id="fb5d4-189">Firma Microsoft zadawane pytania firma Microsoft może odpowiedzi z danymi</span><span class="sxs-lookup"><span data-stu-id="fb5d4-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="fb5d4-190">Budujemy *modelu* przy użyciu *regresji liniowej*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="fb5d4-191">Wprowadziliśmy *prognozowania*, wraz z *przedział ufności*</span><span class="sxs-lookup"><span data-stu-id="fb5d4-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="fb5d4-192">I nie używamy matematyczne lub komputery toodo go.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-192">And we didn't use math or computers toodo it.</span></span>

<span data-ttu-id="fb5d4-193">Teraz, jeśli tak samo, jak gdyby było więcej informacji...</span><span class="sxs-lookup"><span data-stu-id="fb5d4-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="fb5d4-194">Wytnij Hello z romb hello</span><span class="sxs-lookup"><span data-stu-id="fb5d4-194">hello cut of hello diamond</span></span>
* <span data-ttu-id="fb5d4-195">kolory (jak blisko romb hello jest białe toobeing)</span><span class="sxs-lookup"><span data-stu-id="fb5d4-195">color variations (how close hello diamond is toobeing white)</span></span>
* <span data-ttu-id="fb5d4-196">Liczba Hello dołączenia w romb hello</span><span class="sxs-lookup"><span data-stu-id="fb5d4-196">hello number of inclusions in hello diamond</span></span>

<span data-ttu-id="fb5d4-197">.. .i firma musiałaby większą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-197">...then we would have had more columns.</span></span> <span data-ttu-id="fb5d4-198">W takim przypadku matematyczne staje się przydatne.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="fb5d4-199">Jeśli masz więcej niż dwie kolumny jest toodraw twardym kropki w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-199">If you have more than two columns, it's hard toodraw dots on paper.</span></span> <span data-ttu-id="fb5d4-200">matematyczne Hello umożliwia bardzo dobrze nadające się tego wiersza lub dane tooyour płaszczyzny.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-200">hello math lets you fit that line or that plane tooyour data very nicely.</span></span>

<span data-ttu-id="fb5d4-201">Ponadto jeśli zamiast tylko kilku karo, było dwa tysiące lub dwóch milionów, a następnie wykonaj pracy znacznie szybciej z komputerem.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="fb5d4-202">Obecnie zajmowaliśmy jak regresji liniowej toodo i my wprowadzone prognozowania, przy użyciu danych.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-202">Today, we've talked about how toodo linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="fb5d4-203">Należy się toocheck limit hello innych plików wideo w "Danych nauki dla początkujących" z Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-203">Be sure toocheck out hello other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb5d4-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb5d4-204">Next steps</span></span>
* [<span data-ttu-id="fb5d4-205">Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="fb5d4-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="fb5d4-206">Pobierz wprowadzenie tooMachine uczenia w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fb5d4-206">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
