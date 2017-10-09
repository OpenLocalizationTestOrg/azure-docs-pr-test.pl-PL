---
title: "aaaOn lokalnych aplikacji z magazynem obiektów blob (w języku Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikacja konsolowa, która przekazuje tooAzure obrazu, a następnie wyświetla hello obraz w przeglądarce. Przykłady kodu w języku Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="2ebab-104">Aplikacji lokalnych przy użyciu magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2ebab-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="2ebab-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2ebab-105">Overview</span></span>
<span data-ttu-id="2ebab-106">Hello poniższym przykładzie pokazano sposób korzystania magazynu Azure do przechowywania obrazów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2ebab-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="2ebab-107">Kod Hello w tym artykule jest dla aplikacji konsoli, która przekazuje tooAzure obrazu, a następnie tworzy plik HTML, który wyświetla obraz powitania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="2ebab-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ebab-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ebab-108">Prerequisites</span></span>
* <span data-ttu-id="2ebab-109">Java Developer Kit (JDK), w wersji 1.6 lub nowszej, jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="2ebab-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="2ebab-110">Witaj zestawu Azure SDK jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="2ebab-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="2ebab-111">Hello JAR hello Azure bibliotek języka Java i wszelkie słoików odpowiednich zależności są zainstalowane i są w ścieżce kompilacji hello używany przez Twoje kompilator języka Java.</span><span class="sxs-lookup"><span data-stu-id="2ebab-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="2ebab-112">Informacje o instalowaniu hello biblioteki Azure dla języka Java, zobacz [hello Pobierz zestaw Azure SDK for Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2ebab-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="2ebab-113">Konto magazynu platformy Azure został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="2ebab-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="2ebab-114">Witaj nazwę konta i klucz konta usługi dla konta magazynu hello będą korzystali hello kodu w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2ebab-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="2ebab-115">Zobacz [jak tooCreate konta magazynu](storage-create-storage-account.md#create-a-storage-account) informacji o tworzeniu konta magazynu i [wyświetlanie i kopiowanie kluczy dostępu do magazynu](storage-create-storage-account.md#view-and-copy-storage-access-keys) informacje o pobieraniu hello klucz konta.</span><span class="sxs-lookup"><span data-stu-id="2ebab-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="2ebab-116">Utworzono plik obrazu lokalnego o nazwie przechowywanych na powitania ścieżka c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="2ebab-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="2ebab-117">Można również zmodyfikować **FileInputStream** konstruktora w toouse przykład hello ścieżkę i nazwę innego obrazu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="2ebab-118">tooupload magazynu obiektów blob platformy Azure toouse pliku</span><span class="sxs-lookup"><span data-stu-id="2ebab-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="2ebab-119">W tym miejscu przedstawiono procedury krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="2ebab-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="2ebab-120">Jeśli chcesz tooskip wyprzedzeniem hello całego kodu przedstawiono w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="2ebab-121">Rozpocząć hello kodu przy tym Importy dla klasy magazynu Azure core hello, klasy klienta obiektów blob platformy Azure hello hello klasy Java We/Wy i hello **URISyntaxException** klasy.</span><span class="sxs-lookup"><span data-stu-id="2ebab-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="2ebab-122">Deklarowanie klasy o nazwie **StorageSample**i zawierają hello otwierającego nawiasu **{**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="2ebab-123">W ramach hello **StorageSample** klasy, zadeklarować zmiennej ciągu, która będzie zawierała hello domyślnego punktu końcowego protokołu, nazwa konta magazynu i klucz dostępu do magazynu, zgodnie z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ebab-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="2ebab-124">Zastąp symbole zastępcze hello **Twojego\_konta\_nazwa** i **Twojego\_konta\_klucza** z własną nazwę konta i klucz konta odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="2ebab-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="2ebab-125">Dodaj w deklaracji pod kątem **głównego**, obejmują **spróbuj** zablokować, a także zawierać hello niezbędne otwartych nawiasów, **{**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="2ebab-126">Deklarowanie zmiennych hello następującego typu (powitalne opisy są do korzystania z nich w tym przykładzie):</span><span class="sxs-lookup"><span data-stu-id="2ebab-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="2ebab-127">**CloudStorageAccount**: hello tooinitialize używane konto obiektu z nazwy konta magazynu Azure, a klucz i toocreate obiektu blob klienta.</span><span class="sxs-lookup"><span data-stu-id="2ebab-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="2ebab-128">**CloudBlobClient**: używana usługa blob hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="2ebab-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="2ebab-129">**CloudBlobContainer**: używane toocreate kontenera obiektów blob, listę obiektów blob w kontenerach hello i usuwania hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2ebab-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="2ebab-130">**CloudBlockBlob**: tooupload używane kontener toothe pliku obrazu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2ebab-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="2ebab-131">Przypisz toohello wartość **konta** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2ebab-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="2ebab-132">Przypisz toohello wartość **serviceClient** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2ebab-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="2ebab-133">Przypisz toohello wartość **kontenera** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2ebab-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="2ebab-134">Możemy uzyskać tooa odwołanie do kontenera o nazwie **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="2ebab-135">Tworzenie kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="2ebab-135">Create hello container.</span></span> <span data-ttu-id="2ebab-136">Ta metoda utworzy kontener hello, jeśli nie istnieje (i zwracać **true**).</span><span class="sxs-lookup"><span data-stu-id="2ebab-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="2ebab-137">Jeśli istnieje hello kontenera, będzie zwracać **false**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="2ebab-138">Zamiast zbyt**createIfNotExists** jest hello **utworzyć** — metoda (co spowoduje zwrócenie błędu, jeśli hello kontener już istnieje).</span><span class="sxs-lookup"><span data-stu-id="2ebab-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="2ebab-139">Ustaw dostęp anonimowy hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2ebab-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="2ebab-140">Pobierz odwołanie toohello blokowego obiektu blob, który będzie reprezentował hello blob w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="2ebab-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="2ebab-141">Użyj hello **pliku** tooget konstruktora, który trzeba będzie przekazać pliku toohello utworzony lokalnie odwołań.</span><span class="sxs-lookup"><span data-stu-id="2ebab-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="2ebab-142">Upewnij się, że ten plik został utworzony przed uruchomieniem kodu hello.</span><span class="sxs-lookup"><span data-stu-id="2ebab-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="2ebab-143">Przekaż hello pliku lokalnego za pomocą toohello wywołania **CloudBlockBlob.upload** metody.</span><span class="sxs-lookup"><span data-stu-id="2ebab-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="2ebab-144">Witaj pierwszy parametr toohello **CloudBlockBlob.upload** jest metoda **FileInputStream** obiekt tego reprezentuje hello lokalnego pliku, który ma być przekazany tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="2ebab-145">drugi parametr Hello jest hello wyrażony w bajtach rozmiar, hello pliku.</span><span class="sxs-lookup"><span data-stu-id="2ebab-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="2ebab-146">Wywoływanie funkcji pomocnika o nazwie **MakeHTMLPage**, toomake podstawowe HTML strony, która zawiera  **&lt;obrazu&gt;**  element z hello źródła zestawu toohello blob, który znajduje się teraz w platformy Azure Konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="2ebab-147">Witaj kod **MakeHTMLPage** zostanie dokładnie omówione w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="2ebab-148">Drukowanie komunikatów o stanie i informacje o hello utworzona strona HTML.</span><span class="sxs-lookup"><span data-stu-id="2ebab-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="2ebab-149">Zamknij hello **spróbuj** bloku wstawiając nawiasu zamykającego: **}**</span><span class="sxs-lookup"><span data-stu-id="2ebab-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="2ebab-150">Obsługa hello następujące wyjątki:</span><span class="sxs-lookup"><span data-stu-id="2ebab-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="2ebab-151">**FileNotFoundException**: może zostać wygenerowany przez hello **FileInputStream** lub **FileOutputStream** konstruktorów.</span><span class="sxs-lookup"><span data-stu-id="2ebab-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="2ebab-152">**StorageException**: może zostać wygenerowany przez biblioteki usługi powitania klienta usługi Azure storage.</span><span class="sxs-lookup"><span data-stu-id="2ebab-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="2ebab-153">**URISyntaxException**: może zostać wygenerowany przez hello **ListBlobItem.getUri** metody.</span><span class="sxs-lookup"><span data-stu-id="2ebab-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="2ebab-154">**Wyjątek**: obsługa wyjątków ogólnych.</span><span class="sxs-lookup"><span data-stu-id="2ebab-154">**Exception**: Generic exception handling.</span></span>

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="2ebab-155">Zamknij **głównego** wstawiając nawiasu zamykającego: **}**</span><span class="sxs-lookup"><span data-stu-id="2ebab-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="2ebab-156">Utwórz metodę o nazwie **MakeHTMLPage** toocreate podstawowe HTML strony.</span><span class="sxs-lookup"><span data-stu-id="2ebab-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="2ebab-157">Ta metoda ma parametr typu **CloudBlobContainer**, które będzie używane tooiterate za pośrednictwem listy hello przekazane obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2ebab-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="2ebab-158">Ta metoda zgłosi wyjątki typu **FileNotFoundException**, który może zostać wygenerowany przez hello **FileOutputStream** konstruktora, i **URISyntaxException**, co może być zgłaszany przez hello **ListBlobItem.getUri** metody.</span><span class="sxs-lookup"><span data-stu-id="2ebab-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="2ebab-159">Obejmować nawias otwierający **{**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="2ebab-160">Tworzenie pliku lokalnego o nazwie **index.html**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="2ebab-161">Zapis pliku lokalnego toohello, dodanie hello  **&lt;html&gt;**,  **&lt;nagłówka&gt;**, i  **&lt;treści&gt;**  elementów.</span><span class="sxs-lookup"><span data-stu-id="2ebab-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="2ebab-162">Iterowanie za pomocą listy hello przekazane obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2ebab-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="2ebab-163">Dla każdego obiektu blob, na stronie powitania HTML utworzyć  **&lt;img&gt;**  element, który ma jego **src** atrybut wysłany do hello identyfikator URI obiektu hello blob, ponieważ znajduje się na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ebab-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="2ebab-164">Mimo że tylko jeden obraz został dodany w tym przykładzie, jeśli został dodany więcej, ten kod będzie Iterowanie wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="2ebab-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="2ebab-165">Dla uproszczenia w tym przykładzie przyjęto założenie, że każdy przekazany obiekt blob jest obrazem.</span><span class="sxs-lookup"><span data-stu-id="2ebab-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="2ebab-166">Jeśli użytkownik zaktualizował obiektów blob innego niż obrazy lub stronicowe obiekty BLOB zamiast blokowych obiektów blob, Dostosuj kod hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="2ebab-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="2ebab-167">Zamknij hello  **&lt;treści&gt;**  elementu i hello  **&lt;html&gt;**  elementu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="2ebab-168">Zamknij hello pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2ebab-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="2ebab-169">Zamknij **MakeHTMLPage** wstawiając nawiasu zamykającego: **}**</span><span class="sxs-lookup"><span data-stu-id="2ebab-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="2ebab-170">Zamknij **StorageSample** wstawiając nawiasu zamykającego: **}**</span><span class="sxs-lookup"><span data-stu-id="2ebab-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="2ebab-171">Oto Hello hello kompletny kod dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="2ebab-172">Pamiętaj symbole zastępcze hello toomodify **Twojego\_konta\_nazwa** i **Twojego\_konta\_klucza** toouse nazwę konta i konta klucz, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="2ebab-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="2ebab-173">W toouploading dodanie obrazu lokalnego pliku magazynu tooAzure, hello przykładowy kod tworzy namedindex.html pliku lokalnego, który można otworzyć w Twojej przeglądarce toosee Twojego załadowanego obrazu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="2ebab-174">Ponieważ kod hello zawiera nazwę konta i klucz konta usługi, upewnij się, że kod źródłowy jest bezpieczna.</span><span class="sxs-lookup"><span data-stu-id="2ebab-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="2ebab-175">toodelete kontenera</span><span class="sxs-lookup"><span data-stu-id="2ebab-175">toodelete a container</span></span>
<span data-ttu-id="2ebab-176">Ponieważ naliczane są opłaty za magazyn, może być toodelete **gettingstarted** kontenera po zakończeniu eksperymentowanie z tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="2ebab-177">toodelete kontener, użyj hello **CloudBlobContainer.delete** metody.</span><span class="sxs-lookup"><span data-stu-id="2ebab-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="2ebab-178">Witaj toocall **CloudBlobContainer.delete** metoda, proces inicjowania hello **CloudStorageAccount**, **ClodBlobClient**, i  **CloudBlobContainer** obiektów jest taki sam, jak pokazano na hello **createIfNotExist** metody.</span><span class="sxs-lookup"><span data-stu-id="2ebab-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="2ebab-179">Witaj poniżej znajduje się pełny przykład, że usuwa hello kontener o nazwie **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="2ebab-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

<span data-ttu-id="2ebab-180">Omówienie inne klasy magazynu obiektów blob i metody, zobacz [jak toouse magazynu obiektów Blob w języku Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2ebab-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ebab-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ebab-181">Next steps</span></span>
<span data-ttu-id="2ebab-182">Wykonaj te toolearn łącza więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ebab-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="2ebab-183">Magazyn Azure SDK dla języka Java</span><span class="sxs-lookup"><span data-stu-id="2ebab-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="2ebab-184">Odwołanie do zestawu SDK klienta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2ebab-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="2ebab-185">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2ebab-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="2ebab-186">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2ebab-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

