Jeśli użytkownik ma adres URL sygnatury dostępu Współdzielonego dostępu współdzielonego, który daje dostęp tooresources na koncie magazynu, można użyć hello SAS w parametrach połączenia. Ponieważ hello SAS zawiera Żądanie hello tooauthenticate wymaganych informacji hello, ciągu połączenia za pomocą sygnatury dostępu Współdzielonego zapewnia hello protokołu, punkt końcowy usługi hello i hello niezbędnych poświadczeń tooaccess hello zasobów.

toocreate ciąg połączenia, który zawiera sygnaturę dostępu współdzielonego określić ciąg hello hello następującego formatu:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Każdy punkt końcowy usługi jest opcjonalny, mimo że hello parametry połączenia muszą zawierać co najmniej jeden.

> [!NOTE]
> Jako najlepsze rozwiązanie zaleca się przy użyciu protokołu HTTPS z sygnatury dostępu Współdzielonego.
>
> Jeśli określisz sygnatury dostępu Współdzielonego w ciągu połączenia w pliku konfiguracji, może być konieczne tooencode znaki specjalne w adresie URL hello.
>
>

### <a name="service-sas-example"></a>Przykład sygnatury dostępu Współdzielonego usługi
Oto przykład parametrów połączenia, który obejmuje sygnatury dostępu Współdzielonego usługi magazynu obiektów Blob:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

A Oto przykład hello tych samych parametrach połączenia z kodowaniem znaków specjalnych:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Przykład sygnatury dostępu Współdzielonego konta
Oto przykład parametrów połączenia, które obejmuje sygnatura dostępu Współdzielonego konta magazynu obiektów Blob i plików. Należy zwrócić uwagę, określenia punktów końcowych dla obu usług:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

A Oto przykład hello tych samych parametrach połączenia z kodowaniem adresu URL:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

