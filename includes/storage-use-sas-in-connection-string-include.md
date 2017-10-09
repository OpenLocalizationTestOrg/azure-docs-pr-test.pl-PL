<span data-ttu-id="859b3-101">Jeśli użytkownik ma adres URL sygnatury dostępu Współdzielonego dostępu współdzielonego, który daje dostęp tooresources na koncie magazynu, można użyć hello SAS w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="859b3-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="859b3-102">Ponieważ hello SAS zawiera Żądanie hello tooauthenticate wymaganych informacji hello, ciągu połączenia za pomocą sygnatury dostępu Współdzielonego zapewnia hello protokołu, punkt końcowy usługi hello i hello niezbędnych poświadczeń tooaccess hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="859b3-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="859b3-103">toocreate ciąg połączenia, który zawiera sygnaturę dostępu współdzielonego określić ciąg hello hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="859b3-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="859b3-104">Każdy punkt końcowy usługi jest opcjonalny, mimo że hello parametry połączenia muszą zawierać co najmniej jeden.</span><span class="sxs-lookup"><span data-stu-id="859b3-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="859b3-105">Jako najlepsze rozwiązanie zaleca się przy użyciu protokołu HTTPS z sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="859b3-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="859b3-106">Jeśli określisz sygnatury dostępu Współdzielonego w ciągu połączenia w pliku konfiguracji, może być konieczne tooencode znaki specjalne w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="859b3-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="859b3-107">Przykład sygnatury dostępu Współdzielonego usługi</span><span class="sxs-lookup"><span data-stu-id="859b3-107">Service SAS example</span></span>
<span data-ttu-id="859b3-108">Oto przykład parametrów połączenia, który obejmuje sygnatury dostępu Współdzielonego usługi magazynu obiektów Blob:</span><span class="sxs-lookup"><span data-stu-id="859b3-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="859b3-109">A Oto przykład hello tych samych parametrach połączenia z kodowaniem znaków specjalnych:</span><span class="sxs-lookup"><span data-stu-id="859b3-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="859b3-110">Przykład sygnatury dostępu Współdzielonego konta</span><span class="sxs-lookup"><span data-stu-id="859b3-110">Account SAS example</span></span>
<span data-ttu-id="859b3-111">Oto przykład parametrów połączenia, które obejmuje sygnatura dostępu Współdzielonego konta magazynu obiektów Blob i plików.</span><span class="sxs-lookup"><span data-stu-id="859b3-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="859b3-112">Należy zwrócić uwagę, określenia punktów końcowych dla obu usług:</span><span class="sxs-lookup"><span data-stu-id="859b3-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="859b3-113">A Oto przykład hello tych samych parametrach połączenia z kodowaniem adresu URL:</span><span class="sxs-lookup"><span data-stu-id="859b3-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

