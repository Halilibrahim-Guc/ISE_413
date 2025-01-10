# ISE_413

Bootcamp 1:

0:47:0-2:20:0 arası service controller model oluşturma

22:36) Db class oluşturdu, Dbcontext den inherit ediyor.

Hemen öncesinde many to many oluşturmuştu

29:44) MVC de Program.cs içerisinde IoC Container tanımlıyorsun.
30:30) AddContext görmüyor ama IoC,bunun için MV sağ tık add diyip project reference demen lazım, BLL seçip add diyorsun. BLL de olulturduğu mvc de kullanmanı sağlıyor

![image](https://github.com/user-attachments/assets/e3c50c2d-cf8f-4f65-9ed6-ad0639c5e319)
37:22) Packege manager console açma ve add-migration v1, bu database oluşturuyor herhalde. Entity de structure değişimi yapıyorsan yeni bir db set e ihtiyacın var, o nedenle add migration yapıyorsun, database yaratmak için. Db class ne içerisindeyse default project onu seç, yani BLL!
Ardından update-database de

40:02) Ancak bunu kullanmak (run yapmak için) için mvc ye sağ tıkla, manage nuget package de, browse diyip tools indir.

43:57) view dan sql şeyini seçip databaseyi görüyorsun

48:20) templates ekle mvc ye, build et, eğer alırsan sağ tık yap ve exluede projeden
51:00) Controller ekliyor, mutlaka bll dal daki entitiy ler olacak model olarak controllerler. 3 kutucuktan 2. Sini alma
53) İçerisinde MVC controller oluşturuyor.

54:48) kullanmak için BLL içine Package Reference ekledi.

57) BLL için telrar ViewFeatures paketi ekledi nugetten
1:00:00) culture info Tr falan yapıyor, datetime, currency için formatı belirliyormuş
1:17:00) Service classları, her bir class için interface
1:21:00) hepsi ServiceBase abstract class ından türeme, crud operationları
1:24:00) readonly ler ile dependency/construction injection yaptık service içerisinde
1:25:00) readonly ile constructor da veya üstteki line de initialize yapabilirsn, ancak method içerisinde yapamazsın!
1:29:50) IspeciesService ana classına ctrl+. Yapıp hızlıca abstract class dan methodları çekti
1:34:50) her bir non navigational property için entity deki, model içerisinde implement edeceğiz!!
1:40:00) her querry bir collection döndürür
Trim ortadaki değil, baştaki ve sondaki boşlukları siler
1:44:50) eğer Name null olabilirse, trim() boşa gitmesin diye ? Koy.
Bu service içerisinde yaptımığı ız her şey interface üzerinden database üzerinde yeni recordlar oluşturmak için,

Crud operations yani
1:48:25) Index starting point miş mvc controllers içerisinde
1:50:50) for update operation, diğer recordların id lerini de kontrol et diyoruz any parantezinin başında
1:53:30) SingleOrDefault u dbset dışında diğer collectionlar da da kullanabilirmişiz
1:56:00) Non navigational olmayan her entitiy için properties i update etmeyi unutma!
1:58:00) silme işlemlerinde misal species silecen, ama pets olarak relational entitites var. Misal türü silersin ama içinde hayvan listesi vardır, o nedenle önce user ı uyar.

. Count > 0 .Any ile aynı şey
02:02:35) If any navigational property sisini kullanıyorsan bir entity nin, mutlaka .Include() (içinde query ile, s => s.Pets gibi) kullanman lazım!!!
02:08:30) Service oluşturduğun zaman, her bir injection için Program.cs içerisindeki IoC container içerisinde object initialize et o service ile alakalı!
02:11:50) AddSingleton anlatıyor

Operationlar için her zaman single object kullan demek. Object ölmeyecek, memory de kalacak application run etmeyi bitirene kadar.

AddTransient (bunu hiç kullanamaycağız) ise her injection happen, yeni objekt oluştur. Ama biz genelde AddScoped kullanıyoruz. Her request geldiğinde obje oluşup ölüyor
02:17:00) hoca asla bize view veya controller yazdırmayacak!!

Index bir controllerin generally beginnin operationu, buradaki her action otomatik olarak çalıştırılıyor.

![image](https://github.com/user-attachments/assets/ab703b2a-1fe3-435a-abc9-041a4e3a9665)
Viewimports a @using.BLL.models ekledik, böylece her view içinde bunları yazmak zorunda kalmayacağız

Bu noktadan sonra layout ve index içerisindeki html kodlarını açıklıyor

02:29:20) HTML. yaparsan bu bir html helper, c# içinde html kullanmanı sağlıyo herhalde

Asp-action ise tag helper herhalde
02:38:15) Controller içindeki kodları açıklıyor
02:52:00) controller içerisinde ModelOnly veya All yapabilirsin, ilki olursa hatalar gözükmeyecekmiş table daki

02:38:09 a kadar view da species index düzenledi birkaç yerde, onları da en sonunda yoruma dönüştürdü yani bişi yapmadı. MVC species controllere geçti.
03:16:00 a kadar hiçbir şey yazmadı, ama build yapıp üstteki web adresine /species/index yaptığında ekleme falan yapabildiği sayfaya gitti, ben publisher ve developer için denedim ama gidemedim :(
3:30:00 a kadar da species e web de işte kangal falan ekledi, kodda bişi yapmadı. 3:31:24 layout u summarize ediyor
03:34:55 layout ta geliştiriciler ve yayıncılar yazmayı öğrendim
03:43:55 Species controllere bakıyor tekrar, edit section için
Sonuna kadar hiç kod yazmadı, sadece controller anlattı

.
.
.

Bootcamp 2:

19:40 e kadar PetModel yaptı

Şimdi PetService (pet için crud operation yapacak olan class)
24:15) IService kısmı başka bir way, optional. Kullanmak zorunda değilsin.
32:32) Way 2 (generic interface) yi kullanarak way 1 deki 7 line den kurtulduk, again and again bunu yazmak zorunda değiliz.
33:09 way 1 gösteriyor
45:05) Name? yaptı çünkü o bir string, stringler null olabilir, bu nedenle hepsinde soru işareti kullanmamızı öneriyor
51:10) Pet delete yapmadan önce relational table (PetOwner) daki verilerin kaldırılması gerekiyor
51:40) RemoveRange() kullanırsınsan bir collection içinden collection kaldırmış olursun. Tek bir instance için remove kullan
52:38) PetOwner navigational property sini kullandığımız için query de Include(p=p.PetOwners) demek zorundayız!

54:35) PetService bitti, uygulamada kullanmak istiyoruz. Bu nedenle mvc içinde PetsController olarak inject etmemiz gerekiyor.
Bunun için de önce Program.cs içinde IoC container içinde addscoped yapacaksın.
56:20) AddSingleton kullanıyorsan uygulamada yalnızca bir object, instance ye sahipsin. Transient is not preferred. Generic interface kullanıyorsan way 2 kullan.
58:45) PetsController ekliyor. Her şey bizim için oluşturuldu, bir şey yapmamıza gerek yok.
01:01:11) Generic interface kullandığımız için PetsController içindeki IPetService hata veriyor, onu değiştireceksin! IService<Pet, PetModel> yazacaksın. 
Hoca bu structure göre ileride templates'i değiştirebilirmiş, o zaman böyle uğraşmamız gerekmezmiş.

01:03:30 yine başka bir yeri değiştirdi

Şimdi Pet view e bakıyor index ine
01:07:55) html helper ve tag helper anlaşılan bootcamp 1 de anlatmışım, tekrar geçmeye pek gerek yok dedi 

2 html helper kullanıyormuş hoca, diğerlerine istiyorsan bak, displayfor ve namefor dedi sanırım.

1:09:30 tekrar PetsController bakıyor, 10 da view e geçti
01:15:30) PetsController içinde dropdown list falan bahsediyor
01:21:00) PetsController create viewinde son satırı comment e çevirdi, nedenini söylüyor, edit te de varmış
Navigational property leri kullanıcıların görmesine gerek yok, çünkü onlarla etkileşime girmiyorlar, o nedenle service de dahil etmiyoruz.
01:24:27) eğer uygulama türkçe ise, calender ı ayarlaman lazım!! Bu nedenle calender css library kullan, bootstrap veya jquery gibi, web browser calender kullanmak kötü. 
Partial view oluştur bu nedenle.
1:21:35) views pets edit içinde de calender varmış onu da düzelteyim dedi
01:37:15 de hocanın kendi githubından açtığı datetimepicker kodunu kullanabilirsin.

Shared içerisinde DateTimePicker classı olulturacağız yani. Zaten hazır kod kullanınca datetimepicker hata veriyordu, demek class olulturmadığımdan.
1:41:00 a kadar bunu yaptı

1:43:00 a kadar da layout ta index ekleyip calender ı kontrol etti.
1:50:10 controller da her şey otomatik operation, otomatik olarak oluşturulmuş, bir şey yapmamıza gerek yokmuş, ancak anlamamız gerekiyormuş.
01:52:40) Create Post sectionu falan yapacak
02:08:10) Her pets species e sahip olmalı, bunu null olabilir yapmış sanırım, düzeltmeye gitti
02:09:45) int SpeciesId yaparsan, üstüne de required yazarsan error almadan required hale getirirsin pet için species i. Ancak bu extra information imiş, error message falan gerek yokmuş.
02:13:45) Öyle gender yazınca, yanına da kutucuk koyunca anlaşılmuyor, bunu isfemale yazalım isterseniz dedi.

02:14:45) PetModel de değiştirdi BLL models deki.
02:15:40) Eğer relational data alamıyorsan service içinfe Include etmen lazım species i
Relational data alamıyorsan unutma bunu

.
.
.

Bootcamp 3: Retrieve data from many to many relationship

Many to many operations anlatacakmış.

Genelde connectionstring i Program.cs de değil appsetting.json içine yazılıyormuş, onu yazıyor. 

Final ve final phase de appsettings içine yaz diyor, program cs değil!!
08:00)AppSettings oluşturuyor BLL Models içerisinde elle, appsettings.json içerisindeki title, description kısmı ile aynı.

Class'ı Static yaparak sadece tek instance oluşturabilirsin, ama yapmadı.

Program.cs içerisinde AppSettings oluşturmayı unutma
20) paint de pet in owner a ulaşması için önce petowner a ulaşması, oradan owner a ulaşması gerektiğini söylüyor.

PetOwner null olabilirmiş, ? Koydu ondan. 

PetOwner bir collection olduğu için, PetModel içerisinde PetOwners.Select kullanıyoruz.

21:50) Yani pet den petowner a ulaştık, oradan da owner ı seçip projection yaptık. Ayrıca sadece adıyla yetinme (final phase de hoca puan kıracakmış bundan), adı ve soyismini al.

Get a string collection, owner name ve surname içeren.
23:33) string collection concenate için string.Join kullan

<br> ise separater, arada boşluk olması için herhalde
26:32) List<owner> şeklinde yaparsan view de her element i itere etmen gerekirmiş.

29:10) PetService içerisinde ThenInclude() kullandık, çünkü petowner kullanmışız, oradan owner include etmişiz. İlk önce include ile petowner, ardından theninclude ile owner dahil etti

Final phase de trim kullanmaya gerek yokmuş.
32:49) Views dosyası Pets, Details.cshtml içerisinde way 1 ve 2 olarak nasıl değiştireceğini gösterdi

.
.
.

Bootcamp 4:

Many to many relationship de entery girme sanırım, database ye many to many raletion enter etme
04:39) duplica data olmamalı pet de, o nedenle SingleOrDefault

Multiple owner olması durumu için sadece many to many ler get ve set e sahip olur.
12:10) View da pets in create kısmında many to many için bir şey yapıştırdı, view species create den kopyala yapıştır yapıp değiştirdi
18:17) ownermodel içerisinde name ve surname için ortak string oluşturdu
26:00) bir şeyin view inde create içinde ViewBag.OwnerIds kısmı var, merake den viewbag e bakabilir dedi

.
.
.

Bootcamp 5: 
User authentication and authorization konusu
Bunun için DAL altında user ekliyoruz
Yeni oluşturduğun entity leri Db.cs içine koymayı unutma (role ve user)
07:42) add-migration yapıyor. Bu ve scaffolding için mutlaka projen build olmalı, yani syntax error olmamalı!!
Update database yap migration u uygulamak için
11:25) many to many relational entities dışında (petowner gibi) her bir entity  için model oluştur
13) Modeller kullanıcı ve Service den input alıp controller ve view a göndermek için kullanılır
15:50) Bir entity veya entity collection u asla model içerisinde property olarak kullanma! (Public Role Role gibi, public string Role kullanmak yerine)

Çünkü view da olabildiğince az kod yazmak istiyoruz.

Navigationalal Property null olabileceğinden ? İşareti Koymayı unutma, crud operasyonlarından dolayı null gelebiliyormuş.

(Ek bilgi: normalde kullanıcıdan ve veritabanından veri almak için 2 ayrı model kullanılırmış, ancak biz mvc kullanıdığımız için böyle yapıyormuşız. Web api gibi şeylerde ayrıymış)
21:30) UserService oluşturuyoruz.

23:34) IService kısmına ctrl+ basıp implement interface diyoruz, hızlıca oluşturuyor. 
UserService de basıp generate constructor diyoruz.

26:00) Query function u içerisinde login içlemleri yapılıyormuş!!
34:00) Finalde simple evaluation application soracakmış, instructor ları evaluate edecekmişiz. Hani kendi dersi hakkında değerlendirme formu yazmamız herhalde
37:25) ne zaman bir service oluştursan, IoC container ı check etmen lazım! AddScoped için
39:45) empty Controller oluşturuyor mvc controller içerisinde, mvc controller dan inherit edecek.

UserService okumak için readonly oluşturması lazımmış.

Action'un ismi Login yaptı.
42:50) Empty view oluşturdu actiona nameye tıklayıp

Aslında Razor View de yapabilirmiş. Ancak Empty razor view ekledik. Razor syntax ini hatırlamamız içinmiş


44:00) View ismi controller ismi ile aynı olacak, eğer farklı isim istiyorsan action içerisinde return View("Enter") demen lazım misal view ismi olarak enter için. Ama bunu önermiyor hoca.
59:24) finalde login için view i elle yazmamıza gerek yok scaffolding kullanabilirsiniz dedi. Logic i hatırlatmak için manuelly yapmış.

.
.
.

Bootcamp 6: (22 dk)
03) UserController içerisinde.

HttpPost oluşturuyor client ten login verisi alabilmek için. 

ValidateAntiForgeryToken kullanırsan eğer service de güvenli login için, login view indeki form içinde istediğin bir yere de bunu koyman lazım
07:50) user.cs içinde
{0} dersen place holder (string usernsme deki usernsme), {1} dersen ise aldığı parametreyi simgeler.

Required içerisinde Errormessage'yi customize ediyorduk.

09:45) UserController - Login action'u için kodu yazmaya devam
13:00) claim kullanıyoruz, cookie tutacak herhalde
16:44) Cookie için ctrl+. Basıp {} CookieAuthenticationDefaults using... Seçiyor, aktif hale getiriyor

17:40)SignInAsync metodunu kullanıyor.
Bir dahaki bootcamp async methods açıklayacak.

21:12) dersi bitiriyor, rolle leri falan database viewer da elle ekleyeceğiz herhalde.

IsPersistent = true dersen,

Tarayıcı kapatıp tekrar açsan bile cookie ölmüyor, otomatik giriş yapabiliyorsun.

.
.
.


Bootcamp 7 (39 dk):

Async kullanırken await kullanmazsan , sistem user cevabını beklemez, o nedenle await yapmayı unutma. Task in tamamlanmasını bekliyor.
03:50) SignOutAsync ekledi usercontroller e.

Register method bir entry girmekmiş, record create etmekmiş, zaten biliyoruz diye vermeyecekmiş
04:27) hoca muhtemelen login ve logout implement etmemizi isteyecekmiş, register kodunu verecekmiş.

Şunu isteyecek hoca: Generate 1 controller for crud operations 

Ve bizden Authorize attribute kullanmamızı ve check user role, configure our application according to these yapmamızı isteyecekmiş.
5:0) user authentication eklemek için please remember that make the configuration in program.cs!

09:30) Authentication için builder.Services.AddAuthentication gibi bir şey yapman lazım Program.cs içinde

Authentication için şimdilik bu 4 "options" şeyi yeterli.

09:50)
 app.UseAuthentication eklemeyi unutma!

Ve mutlaka bu app.UseAuthorizationdan önce gelecek!

Bir şeyi build.service yaptıysan program.cs içinde, mutlaka use yapmayı ds unutma sonradan!!


11:30) layout içerisinde login için kısmı yapıyoruz.
21:00) başta database içinde role, sonra user kısımlarını doldurdu elle
22:50) hata alıyorsan bu şekilde sitede bir şeyler yaparken, mutlaka query yanlıştır
35:45) register için hocanın kaynaklara bak, çünkü registering için IsActive True set etmen ve role yi user yapman lazımmış
36:00) View Home İndex içerisinde, eğer authenticated user ise ismi title ile birlikte gözükücek.
38:10) hoca finalde şunu soracak:

Use user instance in only layout. Index view of the home action içerisinde kullanmamızı sormayacakmış büyük ihtimalle.
38:10) hoca finalde şunu soracak:

Use user instance in only layout. Index view of the home action içerisinde kullanmamızı sormayacakmış büyük ihtimalle.

.
.
.

Bootcamp 8 (17:40 dk):

Authentication yaptık, şimdi authorization yapacakmışız. Hangi user neyi yapabilir yani
01:40) her bir controller içerisinde:

[Authorize(Roles = "Admin")]  her bir actionun üzerine yazıp o actionları otorize edebilirsin teker teker, ya da controller ın tepesine yazabilirsin, böylece hepsini etkileyebilirsin
04:50) layout içerisinde @if user.IsInRole("Admin") kullanarak species linkini sadece admine görünür kıldık
06:00) Crud operations sadece admin tarafından yapılmalı, user lar pet list te bunu yapmamalı.

Ancak PetsController içerisinde user lar Index i görebilsin istiyoruz. Bu nedenle [AllowAnonymus] kullandık
09:15) if condition içerisinde user instancesi oluşturup IsInRole kullanarak ta check edebilir, admin değilse login ekranına yönlendirebilirsin, ama gerek yok.
11:30) Views Pets İndex içerisinde, create details gibi linklerin sadece authorizate kullanıcılar görmesini sağladık.
16:50) Bizim projemizdeki modeller dto class larmış Microsoft un diğer modellerinde herhalde

.
.
.

Bootcamp 9 (43:21 dk):

HttpServiceBase abstract class ını oluşturduk

Direk EzCTıs reposundaki koddan kopyala yapıştır yapıp anlatıyor hoca

![image](https://github.com/user-attachments/assets/055ccebd-9588-4d01-a5b0-7e86fc34291d)
Kullanmak için bll ye newtonsoft.json indir nuget Package manager den!!
12:07) HttpServiceBase yi program.cs içerisinde build etmeyi unutma!!

Ardından //Session kısmını yaz!!! TimeSpan kullanıyor hoca.

Ardından use session yapman gerekiyor!

Scoped is per request. İnjection ile yaratılacak, return olunca ölecek.
Singleton, injection ne zaman olsa, application running boyunca ölmeyecek.

18:30) Session kısmı sadece web applicationlarında çalışırmış ama, telefonda falan çalışmazmız herhalde. APL de kullanamazmışsın
19:00) Empty favoritescontroller oluşturuyor. Getsession ile alakalı bir şeyler. 

EzShopCtıs daki CartItem'in karşılığı herhalde. Favori listemize hayvanları ekleyeceğiz.
32:19) CartController e bakıyor FavoritesController yazmak için.
32:58) scaffolding kullanarak view oluşturuyor, FavoritesController içerisindeki Get() IActionResults sağ tıklayarak en baştaki add view a tıkladı. Empty olmayan Razor View seçti, Ezshopctıs örneğinde adı List olduğundan list yaptı, template yi de list seçti. Model class Pet(Bll.dal) seçti. 3 kutucuktan sadece use a layout page seçti


Hata aldı ama , 2 kez denedi olmadı. Db injection da sıkıntı varmış.
38:20) DbFactory oluşturup db yi connectionstring imize göre initialize ederek scaffolding sorununu çözüyormuşuz.

Sadece scaffolding sıkıntısı olursa ama, başka bir şeye yaramıyor.

Şimdi Scaffolding çalıştı.

.
.
.

Son, Bootcamp 10 (30 dakika)

Son View oluşturduğu Kısımdan devam.

List.cshtml de container-fluid falsn yapıp title değiştiriyor.
07:50) f2 ye ya da sağ tıka basıp rename diyip bir ismin tekrarlandığı her kısmı değiştirebilirsin.
Favorites controller üzerinde çalışıyor hoca
CartController dan kopyala yapıştır yaptığının üzerini düzenliyor
18:15) layout içerisinde linkleri koymayı unutma!!!
21:35) FavoritesController içerisindeki Get action u view de List olarak adlandırdığı için, return ederken "List" yazmamız gerekiyor.
28:20) EZShopAtılım örneğinde bunu yapmamış, burada görmüş olmuşuz
