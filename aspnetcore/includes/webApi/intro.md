## <a name="overview"></a><span data-ttu-id="36be0-101">Panoramica</span><span class="sxs-lookup"><span data-stu-id="36be0-101">Overview</span></span>

<span data-ttu-id="36be0-102">Di seguito è riportata l'API che verrà creata:</span><span class="sxs-lookup"><span data-stu-id="36be0-102">Here is the API that you’ll create:</span></span>

|<span data-ttu-id="36be0-103">API</span><span class="sxs-lookup"><span data-stu-id="36be0-103">API</span></span> | <span data-ttu-id="36be0-104">Descrizione</span><span class="sxs-lookup"><span data-stu-id="36be0-104">Description</span></span>    | <span data-ttu-id="36be0-105">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="36be0-105">Request body</span></span>    | <span data-ttu-id="36be0-106">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="36be0-106">Response body</span></span>   |
|--- | ---- | ---- | ---- |
|<span data-ttu-id="36be0-107">GET /api/todo</span><span class="sxs-lookup"><span data-stu-id="36be0-107">GET /api/todo</span></span>  | <span data-ttu-id="36be0-108">Ottiene tutti gli elementi attività</span><span class="sxs-lookup"><span data-stu-id="36be0-108">Get all to-do items</span></span> | <span data-ttu-id="36be0-109">Nessuno</span><span class="sxs-lookup"><span data-stu-id="36be0-109">None</span></span> | <span data-ttu-id="36be0-110">Matrice di elementi attività</span><span class="sxs-lookup"><span data-stu-id="36be0-110">Array of to-do items</span></span>|
|<span data-ttu-id="36be0-111">GET /api/todo/{id}</span><span class="sxs-lookup"><span data-stu-id="36be0-111">GET /api/todo/{id}</span></span>  | <span data-ttu-id="36be0-112">Ottiene un elemento in base all'ID</span><span class="sxs-lookup"><span data-stu-id="36be0-112">Get an item by ID</span></span> | <span data-ttu-id="36be0-113">Nessuno</span><span class="sxs-lookup"><span data-stu-id="36be0-113">None</span></span> | <span data-ttu-id="36be0-114">Elemento attività</span><span class="sxs-lookup"><span data-stu-id="36be0-114">To-do item</span></span>|
|<span data-ttu-id="36be0-115">POST /api/todo</span><span class="sxs-lookup"><span data-stu-id="36be0-115">POST /api/todo</span></span> | <span data-ttu-id="36be0-116">Aggiunge un nuovo elemento</span><span class="sxs-lookup"><span data-stu-id="36be0-116">Add a new item</span></span> | <span data-ttu-id="36be0-117">Elemento attività</span><span class="sxs-lookup"><span data-stu-id="36be0-117">To-do item</span></span>  | <span data-ttu-id="36be0-118">Elemento attività</span><span class="sxs-lookup"><span data-stu-id="36be0-118">To-do item</span></span> |
|<span data-ttu-id="36be0-119">PUT /api/todo/{id}</span><span class="sxs-lookup"><span data-stu-id="36be0-119">PUT /api/todo/{id}</span></span> | <span data-ttu-id="36be0-120">Aggiorna un elemento esistente &nbsp;</span><span class="sxs-lookup"><span data-stu-id="36be0-120">Update an existing item &nbsp;</span></span>  | <span data-ttu-id="36be0-121">Elemento attività</span><span class="sxs-lookup"><span data-stu-id="36be0-121">To-do item</span></span> |  <span data-ttu-id="36be0-122">Nessuno</span><span class="sxs-lookup"><span data-stu-id="36be0-122">None</span></span> |
|<span data-ttu-id="36be0-123">DELETE /api/todo/{id}  &nbsp; &nbsp;</span><span class="sxs-lookup"><span data-stu-id="36be0-123">DELETE /api/todo/{id}  &nbsp;  &nbsp;</span></span> | <span data-ttu-id="36be0-124">Elimina un elemento &nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="36be0-124">Delete an item &nbsp;  &nbsp;</span></span>  | <span data-ttu-id="36be0-125">Nessuno</span><span class="sxs-lookup"><span data-stu-id="36be0-125">None</span></span>  | <span data-ttu-id="36be0-126">Nessuno</span><span class="sxs-lookup"><span data-stu-id="36be0-126">None</span></span>|

<br>

<span data-ttu-id="36be0-127">Il diagramma seguente mostra la struttura base dell'app.</span><span class="sxs-lookup"><span data-stu-id="36be0-127">The following diagram shows the basic design of the app.</span></span>

![Il client è rappresentato da una casella a sinistra e invia una richiesta e riceve una risposta dall'applicazione, una casella a destra.](../../tutorials/first-web-api/_static/architecture.png)

* <span data-ttu-id="36be0-132">Tutti gli elementi che usano l'API Web, come le app per dispositivi mobili, i browser e così via, possono essere definiti client.</span><span class="sxs-lookup"><span data-stu-id="36be0-132">The client is whatever consumes the web API (mobile app, browser, etc).</span></span> <span data-ttu-id="36be0-133">In questa esercitazione non si scriverà un client.</span><span class="sxs-lookup"><span data-stu-id="36be0-133">We aren’t writing a client in this tutorial.</span></span> <span data-ttu-id="36be0-134">Per eseguire il test dell'app, verrà usato [Postman](https://www.getpostman.com/) o [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html).</span><span class="sxs-lookup"><span data-stu-id="36be0-134">We'll use [Postman](https://www.getpostman.com/) or [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html) to test the app.</span></span>

* <span data-ttu-id="36be0-135">Un *modello* è un oggetto che rappresenta i dati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36be0-135">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="36be0-136">In questo caso l'unico modello è un elemento attività.</span><span class="sxs-lookup"><span data-stu-id="36be0-136">In this case, the only model is a to-do item.</span></span> <span data-ttu-id="36be0-137">I modelli sono rappresentati come classi C#, noti anche come oggetti **P**lain **O**ld **C**# **O**bject (POCO).</span><span class="sxs-lookup"><span data-stu-id="36be0-137">Models are represented as C# classes, also know as **P**lain **O**ld **C**# **O**bject (POCOs).</span></span>

* <span data-ttu-id="36be0-138">Un *controller* è un oggetto che gestisce le richieste HTTP e crea la risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="36be0-138">A *controller* is an object that handles HTTP requests and creates the HTTP response.</span></span> <span data-ttu-id="36be0-139">Questa app conterrà un singolo controller.</span><span class="sxs-lookup"><span data-stu-id="36be0-139">This app will have a single controller.</span></span>

* <span data-ttu-id="36be0-140">Per mantenere semplice l'esercitazione, l'app non usa un database persistente.</span><span class="sxs-lookup"><span data-stu-id="36be0-140">To keep the tutorial simple, the app doesn’t use a persistent database.</span></span> <span data-ttu-id="36be0-141">L'app di esempio archivia gli elementi attività in un database in memoria.</span><span class="sxs-lookup"><span data-stu-id="36be0-141">The sample app stores to-do items in an in-memory database.</span></span>