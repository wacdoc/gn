# Emopu’ã nde jeheguiete SMTP ñe’ẽmondo mondóva servidor

## ñe’ẽ ñepyrũrã

SMTP ikatu ojogua directamente servicio umi cloud ñemuhagui, haꞌeháicha:

* [Amazon SES SMTP rehegua](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali arai correo electrónico empuje](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Ikatu avei emopu’ã nde servidor de correo - ñemondo ilimitádo, hepykue tuichakue sa’i.

Iguýpe, rohechauka paso a paso mba’éichapa ikatu ñamopu’ã ñande servidor de correo.

## Servidor jeporavo rehegua

Pe servidor SMTP oñemboguapýva ijehegui oikotevẽ peteĩ IP público oguerekóva puerto 25, 456 ha 587 ojepeꞌavaꞌekue.

Umi arai público ojeporúva jepi omboty ko’ã puerto por defecto, ha ikatu ojeipe’a oñeme’ẽvo peteĩ orden de trabajo, ha katu ijetu’ueterei opa mba’e rire.

Areko rekomenda ojejogua hag̃ua peteĩ karameg̃ua oguerekóva ko’ã puerto ojepe’áva ha oipytyvõva omohenda hag̃ua dominio réra inverso.

Ko’ápe, arrecomenda [Contabo](https://contabo.com) .

Contabo ha'e peteî proveedor de alojamiento oîva Múnich, Alemania-pe, oñemopyendáva 2003 jave orekóva precio competitivo-itereíva.

Eiporavóramo Euro viru ojejogua hag̃ua, hepykue ivaratovéta (peteĩ servidor orekóva 8GB memoria ha 4 CPU hepykue 529 yuan rupi peteĩ arýpe, ha pe instalación ñepyrũrã repykue ndojehepyme’ẽi peteĩ arýpe g̃uarã).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Oñemoĩ jave peteĩ pedido, remark `prefer AMD` , ha pe servidor orekóva AMD CPU oguerekóta rendimiento iporãvéva.

Ko’ãvape, ajagarráta Contabo VPS techapyrãramo ahechauka hag̃ua mba’éichapa ikatu remopu’ã nde servidor de correo.

## Ubuntu sistema ñemboheko

Sistema operativo ko’ápe ha’e Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Pe servidor ssh-pegua ohechaukáramo `Welcome to TinyCore 13!` (ojehechaháicha taꞌãngamýi iguýpe), heꞌise pe sistema noñemoĩriha gueteri. Embogue ssh ha eha’arõ mbovymi aravo eike jey hag̃ua.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ojekuaa vove `Welcome to Ubuntu 22.04.1 LTS` , ñepyrũrã oñemohu’ã, ha ikatu eñepyrũ ko’ã tembiaporã reheve.

### [Ojeporavóva] Emoñepyrũ tekoha ñemoakãrapu’ãrã

Ko paso ha’e opcional.

Iporãve hag̃ua, amoĩ software ubuntu ñemboguapy ha sistema ñemboheko [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) -pe.

Emongu’e ko tembiapoukapy emoĩ hag̃ua peteĩ jekutu rupive.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Umi puruhára chino, eipuru ko tembiapoukapy hendaguépe, ha ñe’ẽ, aravo’i ha mba’e oñemboguapy ijeheguiete.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo ombohape IPV6

Emboguata IPV6 ikatu hag̃uáicha SMTP omondo avei ñe’ẽmondo IPV6 dirección reheve.

emohenda `/etc/sysctl.conf` rehegua

Emoambue térã emoĩve ko’ã línea

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Ejapo seguimiento [contabo mbo’epy reheve: Emoĩve IPv6 joaju nde servidor-pe](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Emohenda `/etc/netplan/01-netcfg.yaml` , emoĩ mbovymi línea ojehechaukaháicha taꞌãngamýi iguýpe (Contabo VPS vore configuración por defecto oguerekóma koꞌã línea, embogue mante).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Upéi `netplan apply` ojejapo hag̃ua efecto configuración modificada.

Osẽ porã rire pe ñemboheko, ikatu eipuru `curl 6.ipw.cn` rehecha hag̃ua ipv6 dirección nde red okapegua.

## Eclona pe mohendaha ryru ops

```
git clone https://github.com/wactax/ops.soft.git
```

## Emoheñói peteĩ kuatia’atã SSL isãsóva nde dominio rérape g̃uarã

Oñemondóvo kuatiañe’ẽ oikotevẽ peteĩ kuatia’atã SSL oñemboheko ha oñefirma hag̃ua.

Roipuru [acme.sh](https://github.com/acmesh-official/acme.sh) romoheñói hag̃ua kuatia’atã.

acme.sh haꞌehína peteĩ tembipuru ojefirma hag̃ua certificado automatizado código abierto rehegua,

Eike almacén configuración ops.soft-pe, emongu’e `./ssl.sh` , ha ojejapóta peteĩ carpeta `conf` **directorio yvateguápe** .

Eheka ne DNS puruhára [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) -gui, emohenda `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Upéi emongu’e `./ssl.sh 123.com` emoheñói hag̃ua `123.com` ha `*.123.com` kuatia’atã nde dominio rérape g̃uarã.

Peteĩha jeguata omoĩta ijeheguiete [acme.sh](https://github.com/acmesh-official/acme.sh) ha omoĩta peteĩ tembiapo oñembosako’íva oñembopyahu hag̃ua ijehegui. Ikatu rehecha `crontab -l` , oĩ peteĩ línea peichagua.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Pe tape kuatia’atã oñembohekopyrévape g̃uarã ha’e peteĩ mba’e ojoguáva `/mnt/www/.acme.sh/123.com_ecc。`

Certificado ñembopyahu ohenóita `conf/reload/123.com.sh` script, emohenda ko script, ikatu emoĩ tembiapoukapy haꞌeháicha `nginx -s reload` embopyahu hag̃ua certificado caché umi aplicación ojoajúva rehegua.

## Emopu’ã SMTP servidor chasquid ndive

[chasquid](https://github.com/albertito/chasquid) haꞌehína peteĩ servidor SMTP código abierto ojehaíva Go ñeꞌeme.

Peteĩ sustituto ramo umi programa yma guare servidor de correo rehegua haꞌeháicha Postfix ha Sendmail, chasquid isãso ha ndahasýi ojepuru hag̃ua, ha avei ndahasýi desarrollo secundario-pe g̃uarã.

Run `./chasquid/init.sh 123.com` oñemboguapyva’erã ijehegui peteĩ clic-pe (emyengovia 123.com nde dominio réra remondóva reheve).

## Emohenda Correo electrónico Firma DKIM rehegua

DKIM ojepuru oñemondo hag̃ua firma correo electrónico rehegua ani hag̃ua ojeguereko kuatiañeꞌepyre spam ramo.

Pe tembiapoukapy oñemboguata porã rire, oñeporandúta ndéve emohenda hag̃ua DKIM kuatiañeꞌepyre (ojehechaháicha koꞌape).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Emoĩnte peteĩ registro TXT nde DNS-pe (ojehechaháicha ko’ápe).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Ohecha servicio estado & registro-kuéra

 `systemctl status chasquid` Ehecha servicio reko.

Pe estado de funcionamiento normal ha e ojehechaháicha ta anga iguýpe

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` térã `journalctl -xeu chasquid` ikatu ohecha jejavy registro.

## Dominio réra ñemboheko jey

Pe dominio réra inverso haꞌehína oheja hag̃ua IP tenda oñemyatyrõ hag̃ua dominio réra ojoajúvape.

Oñemohenda peteĩ dominio réra inverso ikatu ojoko umi correo electrónico ojehechakuaa hag̃ua spam ramo.

Ojeguerahauka jave pe kuatiañeꞌepyre, pe servidor ogueraháva ojapóta análisis dominio réra inverso rehegua IP dirección servidor omondovaꞌekuépe omoañete hag̃ua pe servidor omondovaꞌekue oguerekópa peteĩ dominio inverso réra añetegua.

Pe servidor omondova’ekue ndorekóiramo peteĩ dominio réra inverso térã pe dominio inverso réra ndojoajúiramo IP dirección ndive pe servidor omondova’ekue, pe servidor ogueraháva ikatu ohechakuaa pe correo electrónico spam ramo térã ombotove.

Eike [https://my.contabo.com/rdns-pe](https://my.contabo.com/rdns) ha emohenda ojehechaukaháicha ko’ápe

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Oñemohenda rire dominio réra inverso, nemanduꞌavaꞌerã emohenda hag̃ua resolución tenonde gotyo dominio réra ipv4 ha ipv6 servidor-pe.

## Emohenda chasquid.conf karameg̃ua réra

Emoambue `conf/chasquid/chasquid.conf` pe valor dominio réra inverso rehegua.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Upéi emongu’e `systemctl restart chasquid` emoñepyrũ jey hag̃ua servicio.

## Conf jekopytyjoja git ryru-pe

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Techapyrã, ajapo peteĩ copia de seguridad carpeta conf rehegua che proceso github-pe kóicha

Ojapo raẽ peteĩ almacén privado

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Eike conf directorio-pe ha emondo almacén-pe

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Ombojoapy pe omondova’ekue

ñañi

```
chasquid-util user-add i@wac.tax
```

Ikatu omoĩve omondova’ekue

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Emoañete ñe’ẽñemi oñemohenda porãpa

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Oñemoĩ rire puruhára, `chasquid/domains/wac.tax/users` oñembopyahúta, nemandu’áke emondo hag̃ua almacén-pe.

## DNS omoĩ SPF kuatia

SPF ( Sender Policy Framework ) haꞌehína peteĩ tecnología jekuaaukarã correo electrónico rehegua ojeporúva ojejoko hag̃ua ñembotavy correo electrónico rehegua.

Omoañete identidad peteĩ correo omondova’ekue ohechávo IP omondova’ekue ojoajúpa umi registro DNS dominio réra he’íva ha’eha, ojokóva umi estafador omondo haĝua correo electrónico japu.

Oñemoĩvo SPF registro ikatu ojoko umi correo electrónico ojehechakuaa hag̃ua spam ramo ikatuháicha.

Nde servidor réra dominio ndoipytyvõiramo SPF tipo, emoĩnte TXT tipo registro.

Techapyrã, SPF `wac.tax` rehegua ha’e ko’ãva

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF `_spf.wac.tax` pe g̃uarã

`v=spf1 a:smtp.wac.tax ~all`

Ñañamindu’u arekoha `include:_spf.google.com` ko’ápe, kóva amohenda haguére `i@wac.tax` dirección mondóva ramo Google correo-pe upe rire.

## DNS ñemboheko DMARC

DMARC haꞌehína (Marandu jekuaauka, Ñemombeꞌupy & Ñemboguatarã dominio-pegua) ñemombyky.

Ojepuru ojejapyhy hag̃ua SPF rebote (ikatu ojejavy configuración rupive, térã ambue tapicha nde ha’e gua’u omondo hag̃ua spam).

Oñemoĩve TXT registro `_dmarc` , .

Pe contenido ha’e ko’ãva

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Peteĩteĩ parámetro heꞌiséva haꞌehína kóicha

### p (Política rehegua) .

Ohechauka mbaꞌeichaitépa oñemboguata umi kuatiañeꞌepyre ndohupytýiva SPF (Sender Policy Framework) térã DKIM (DomainKeys Identified Mail) jekuaauka. Pe parámetro p ikatu oñemboguapy peteĩva mbohapy valor apytégui:

* mba’eve: Ndojejapói mba’eveichagua tembiapo, pe resultado verificación rehegua añoite oñemongaru jey pe omondova’ekuépe mecanismo de informe correo electrónico rupive.
* Cuarentena: Emoĩ pe kuatiañe’ẽ ndohasáiva verificación pe carpeta spam-pe, ha katu nombotovemo’ãi pe correo directamente.
* ombotove: Embotove directamente umi correo electrónico ndojapóiva verificación.

### fo (Opciones de fracaso) .

Omombeꞌu mboýpa oguereko marandu omeꞌejeýva mecanismo de informe. Ikatu oñemboguapy peteĩva ko’ã mba’ekuaarãme:

* 0: Omombeꞌu mbaꞌekuaarã jekuaaukarã opaite marandu rehegua
* 1: Emombe’u marandu ndohupytýiva verificación añoite
* d: Emombe’u mante umi mba’e’apo’ỹ dominio réra jekuaaukarã
* s: omombe’únte umi mba’e’apo’ỹ SPF jekuaaukarã
* l: Omombe’u mante umi mba’e’apo’ỹ DKIM jekuaaukarã

### rua & ruf rehegua

* rua (Omombe’u URI marandu Agregado-pe g̃uarã): Correo electrónico dirección ojeguerahauka hag̃ua marandu agregado
* ruf (Omombe’u URI marandu Forense-pe g̃uarã): dirección de correo electrónico ojehupyty hag̃ua marandu detallado

## Emoĩ MX registro embohasa hag̃ua correo electrónico Google Mail-pe

Ndajuhúigui peteĩ correo corporativo isãsóva oipytyvõva dirección universal (Catch-All, ikatu ohupyty oimeraẽva correo electrónico oñemondova’ekue ko dominio rérape, ojejoko’ỹre prefijo-kuéra rehe), aiporu chasquid ambohasa hag̃ua opaite correo electrónico che correo Gmail-pe.

**Oiméramo reguereko nde mba’e’oka empresa rehegua ojepagáva, ani remoambue MX ha embohasa ko tembiaporã.**

Emohenda `conf/chasquid/domains/wac.tax/aliases` , emohenda ñembohasa ryru

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` ohechauka opaite ñe’ẽmondo, `i` ha’e ñe’ẽmondo ñepyrũrã puruhára omondova’ekue omoheñóiva yvateve. Oñembohasa hag̃ua kuatiañeꞌepyre, peteĩteĩva puruhára oikotevẽ omoĩ peteĩ línea.

Upéi emoĩ pe registro MX (aapunta directamente dirección dominio réra inverso rehegua ko’ápe, ojehechaukaháicha primera línea-pe ta’anga iguýpe).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Oñemohu’ã rire ñemboheko, ikatu reipuru ambue ñe’ẽmondo remondo hag̃ua ñe’ẽmondo `i@wac.tax` ha `any123@wac.tax` rehecha hag̃ua ikatúpa rehupyty ñe’ẽmondo Gmail-pe.

Ndaipóriramo, ehecha chasquid registro ( `grep chasquid /var/log/syslog` ).

## Emondo peteĩ correo electrónico i@wac.tax-pe Google Mail rupive

Google Mail ohupyty rire pe correo, naturalmente aha’arõ ambohovái `i@wac.tax` reheve i.wac.tax@gmail.com rangue.

Eike [https://mail.google.com/mail/u/1/#settings/accounts-pe](https://mail.google.com/mail/u/1/#settings/accounts) ha eñemboguejy "Emoĩve ambue dirección de correo electrónico".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Upéi, emoinge pe código verificación rehegua ohupytyva’ekue pe correo electrónico oñembohasávape.

Ipahápe, ikatu oñemohenda dirección omondova’ekue por defecto ramo (opción ombohovái hag̃ua peteĩchagua dirección reheve ndive).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Péicha, romohu’ãma SMTP correo servidor ñemopyenda ha upekuévo roipuru Google Mail romondo ha roguerahauka hag̃ua ñe’ẽmondo.

## Emondo peteĩ correo electrónico prueba rehegua ehecha hag̃ua osẽ porãpa pe configuración

Oike `ops/chasquid`

Emombaꞌapo `direnv allow` emohenda hag̃ua dependencia (direnv oñemboguapyvaꞌekue peteĩ llave ñepyrũrãme ha oñembojoapy peteĩ gancho shell-pe)

upéi eñani

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Umi parámetro he’iséva ha’e kóicha

* puruhára: SMTP puruhára réra
* ohasa: SMTP ñe’ẽñemi
* to: ohupytyva’ekue

Ikatu remondo peteĩ correo electrónico prueba rehegua.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Oñemoñe’ẽ ojepuru hag̃ua Gmail ojegueraha hag̃ua umi correo electrónico prueba rehegua ojehecha hag̃ua osẽ porãpa umi configuración.

### TLS cifrado estándar rehegua

Ohechaukaháicha taꞌãngamýi iguýpe, oĩ ko ñemboty michĩva, heꞌiséva SSL kuatiañeꞌepyre oñembohapéma hague.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Upéi eñemboguejy "Ehechauka Correo Electrónico Original".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM rehegua

Ohechaukaháicha taꞌãngamýi iguýpe, Gmail kuatiañeꞌe ypykue página ohechauka DKIM, heꞌiséva DKIM ñemboheko osẽ porãha.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Ejesareko Recibido rehe pe correo electrónico original iñakãme, ha ikatu rehecha pe dirección omondova’ekue ha’eha IPV6, he’iséva IPV6 oñemboheko porãha avei.
