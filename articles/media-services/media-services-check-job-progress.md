---
title: "aaaMonitor postęp zadania przy użyciu platformy .NET"
description: "Dowiedz się, jak tootrack kod obsługi zdarzenia toouse postępu zadania i wysyłać aktualizacje stanu. Przykładowy kod Hello jest napisany w języku C# i używa hello SDK usługi Media Services dla platformy .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 530aa1d78437cd7c41b4d9a895f9a0e9de0ad49d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="9e223-104">Monitoruj postęp zadania przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9e223-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e223-105">Portal</span><span class="sxs-lookup"><span data-stu-id="9e223-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="9e223-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9e223-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="9e223-107">REST</span><span class="sxs-lookup"><span data-stu-id="9e223-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="9e223-108">Po uruchomieniu zadania często wymagają postępu zadania tootrack sposób.</span><span class="sxs-lookup"><span data-stu-id="9e223-108">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="9e223-109">Możesz sprawdzić postęp hello, definiując obsługi zdarzeń StateChanged (zgodnie z opisem w tym temacie) lub przy użyciu toomonitor magazynu kolejek Azure Media Services zadania powiadomienia (zgodnie z opisem w [to](media-services-dotnet-check-job-progress-with-queues.md) tematu).</span><span class="sxs-lookup"><span data-stu-id="9e223-109">You can check hello progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage toomonitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-toomonitor-job-progress"></a><span data-ttu-id="9e223-110">Zdefiniuj postęp zadania toomonitor procedury obsługi zdarzeń StateChanged</span><span class="sxs-lookup"><span data-stu-id="9e223-110">Define StateChanged event handler toomonitor job progress</span></span>
<span data-ttu-id="9e223-111">Poniższy przykład kodu Hello definiuje hello StateChanged — program obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9e223-111">hello following code example defines hello StateChanged event handler.</span></span> <span data-ttu-id="9e223-112">Ten program obsługi zdarzeń śledzi postęp zadania i udostępnia zaktualizowany stan, w zależności od stanu hello.</span><span class="sxs-lookup"><span data-stu-id="9e223-112">This event handler tracks job progress and provides updated status, depending on hello state.</span></span> <span data-ttu-id="9e223-113">Kod Hello również definiuje metodę LogJobStop hello.</span><span class="sxs-lookup"><span data-stu-id="9e223-113">hello code also defines hello LogJobStop method.</span></span> <span data-ttu-id="9e223-114">Ta metoda pomocnika rejestruje informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="9e223-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due toocancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write hello output tooa local file and toohello console. hello template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="9e223-115">Następny krok</span><span class="sxs-lookup"><span data-stu-id="9e223-115">Next step</span></span>
<span data-ttu-id="9e223-116">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="9e223-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e223-117">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="9e223-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

