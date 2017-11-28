---
title: "Używanie emotikonów Emoji w ramach usługi Azure Mobile Engagement"
description: "Jak używać emotikony Emoji w powiadomień wypychanych"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="60e36-103">Użyj emotikon Emoji w powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="60e36-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="60e36-104">Można uwzględnić Emoji emotikony w przypadku powiadomienie wypychane w kilku prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="60e36-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="60e36-105">Przede wszystkim należy znaleźć Emoji chcesz wysłać w wiadomości.</span><span class="sxs-lookup"><span data-stu-id="60e36-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="60e36-106">Upewnij się, że Emoji wybierasz będą obsługiwane przez urządzenie docelowe jako urządzenia produkującej zająć trochę czasu, można dodać nowo zatwierdzonych Emojis do platformy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="60e36-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="60e36-107">Na **Windows** — można przejść do tego [łącze](http://apps.timwhitlock.info/emoji/tables/unicode) i skopiuj ikonę "Native".</span><span class="sxs-lookup"><span data-stu-id="60e36-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="60e36-108">Na **Mac** — można znaleźć Emojis w słowniku aplikacji w obszarze Edycja -> Emoji & symboli.</span><span class="sxs-lookup"><span data-stu-id="60e36-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="60e36-109">Teraz, przejdź do **osiągnąć** karcie w portalu usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="60e36-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="60e36-110">Wybierz typ powiadomienia wypychane (anons sonduje itp).</span><span class="sxs-lookup"><span data-stu-id="60e36-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="60e36-111">W tym przykładzie wybrany powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="60e36-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="60e36-112">Określ innego pola powiadomienia, aż zostanie wyświetlony tekst powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="60e36-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="60e36-113">Jest to, którym można dodać emotikonu Emoji.</span><span class="sxs-lookup"><span data-stu-id="60e36-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="60e36-114">Można go umieścić w tytułu i/lub wiadomości.</span><span class="sxs-lookup"><span data-stu-id="60e36-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="60e36-115">Konieczne będzie przeciągnij i upuść lub skopiuj Emoji, który można znaleźć w powyższych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="60e36-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="60e36-116">Wypełnij pola inne powiadomienia i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="60e36-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="60e36-117">Przy próbie uruchomienia testu lub aktywować anons zobaczysz powiadomienie z emotikon określone.</span><span class="sxs-lookup"><span data-stu-id="60e36-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="60e36-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="60e36-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

