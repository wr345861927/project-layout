<!-- This translation uses ancient form of written Hindi, so please DO NOT insert/replace words with modern varients. -->
# मानक Go परियोजना अभिन्यास

अनुवाद:

<!-- Insert new entries lexicographically by language code. -->
* [Español](README_es.md)
* [Français](README_fr.md)
* [Indonesian](README_id.md)
* [Italiano](README_it.md)
* [日本語](README_ja.md)
* [한국어 문서](README_ko.md)
* [Português](README_ptBR.md)
* [Română](README_ro.md)
* [Русский](README_ru.md)
* [Türkçe](README_tr.md)
* [Українська](README_ua.md)
* [Vietnamese](README_vi.md)
* [简体中文](README_zh-CN.md) - ???
* [正體中文](README_zh-TW.md)
* [简体中文](README_zh.md)
* [English](README.md)
* [Беларускі](README_by.md)

## अवलोकन

यह Go एप्लिकेशन[^1] परियोजनाओं[^2] के लिए एक बुनियादी अभिन्यास[^3] है। ध्यान दें कि यह सामग्री के संदर्भ में बुनियादी है क्योंकि यह केवल सामान्य अभिन्यास[^3] पर ध्यान केंद्रित करता है न कि इसके अंदर क्या है। यह बुनियादी भी है क्योंकि यह बहुत उच्च स्तर का है और यह इस संदर्भ में विस्तृत विवरण में नहीं जाता है कि आप अपनी परियोजना[^2] को और भी आगे कैसे संरचित[^4] कर सकते हैं। उदाहरण के लिए, यह आपके पास उपस्थित परियोजना[^2] संरचना[^4] को स्वच्छ वास्तुकला जैसी किसी चीज़ से ढकने का प्रयास नहीं करता है।

यह **मूल[^5] Go डेवलपर[^6] दल द्वारा परिभाषित आधिकारिक मानक[^0] नहीं है**। यह Go परितंत्र में सामान्य ऐतिहासिक और उभरती परियोजना[^2] अभिन्यास[^3] नमूनों[^7] का एक समूह है। इनमें से कुछ नमूनें[^7] दूसरों की तुलना में अधिक लोकप्रिय हैं। इसमें किसी भी बड़े वास्तविक एप्लिकेशन[^1] के लिए सामान्य सहायक फ़ोल्डरों[^8] के साथ-साथ कई छोटे संवर्द्धन भी हैं। ध्यान दें कि **मूल[^5] Go दल Go परियोजनाओं[^2] की संरचना[^4] के बारे में सामान्य दिशानिर्देशों का एक बड़ा सेट प्रदान करते है** और जब इसे आयात[^10] किया जाता है और जब इसे स्थापित[^11] किया जाता है तो आपकी परियोजना[^2] के लिए इसका क्या अर्थ होता है। अधिक विवरण के लिए आधिकारिक Go दस्तावेज़ों[^9] में [`Organizing a Go module`](https://go.dev/doc/modules/layout) पृष्ठ देखें। इसमें `internal` और `cmd` फ़ोल्डर[^8] नमूनें[^7] (नीचे वर्णित) और अन्य उपयोगी जानकारी शामिल है।

**यदि आप Go सीखने की कोशिश कर रहे हैं या यदि आप अपने लिए एक **अवधारणा प्रमाण[^12]** या एक साधारण परियोजना[^2] बना रहे हैं तो यह परियोजना[^2] अभिन्यास[^3] ज़रूरत से ज़्यादा है। इसके स्थान पर वास्तव में कुछ सरल से शुरू करें (एक `main.go` फ़ाइल[^21] और `go.mod` पर्याप्त से अधिक है)।** जैसे-जैसे आपकी परियोजना[^2] बढ़ती है, ध्यान रखें कि यह सुनिश्चित करना महत्वपूर्ण होगा कि आपका कोड[^13] ठीक से संरचित[^4] है अन्यथा आप बहुत सारी छिपी हुई निर्भरताओं[^14] और वैश्विक स्थिति के साथ गड़बड़ कोड[^13] पाएंगे। जब आपके पास परियोजना[^2] पर काम करने वाले अधिक लोग हों तो आपको और भी अधिक संरचना[^4] की आवश्यकता होगी। तभी संकुलों[^15]/भंडारों[^16] को प्रबंधित[^17] करने का एक सामान्य तरीका पेश करना महत्वपूर्ण है। जब आपके पास एक खुला-स्रोत[^18] परियोजना[^2] होती है या जब आप जानते हैं कि अन्य परियोजनाएं[^2] आपकी परियोजना[^2] रिपॉजिटरी[^19] से कोड[^13] आयात[^10] करती हैं, तब निजी (उर्फ `internal`) संकुल[^15] और कोड[^13] होना महत्वपूर्ण है। रिपॉजिटरी[^19] को क्लोन करें, जो आपको चाहिए उसे रखें और बाकी सब हटा दें! सिर्फ इसलिए कि यह वहाँ है इसका मतलब यह नहीं है कि आपको इसका पूरा उपयोग करना होगा। प्रत्येक परियोजनाओं[^2] में इनमें से किसी भी नमूनों[^7] का उपयोग नहीं किया जाता है। यहां तक कि `vendor` नमूनां[^7] भी सार्वभौमिक[^20] नहीं है।

Go १.१४ के साथ [`Go Modules`](https://go.dev/wiki/Modules) अंततः उत्पादन के लिए तैयार हैं। [`Go Modules`](https://blog.golang.org/using-go-modules) का उपयोग करें जब तक कि आपके पास उनका उपयोग न करने का कोई विशेष कारण न हो और यदि आप ऐसा करते हैं तो आपको $GOPATH और के बारे में चिंता करने की आवश्यकता नहीं है जहाँ आपने अपनी परियोजना[^2] रखी है। रिपॉजिटरी[^19] में मूल[^5] `go.mod` फ़ाइल[^21] मानती है कि आपकी परियोजना को GitHub पर होस्ट किया गया है, लेकिन यह कोई आवश्यकता नहीं है। अनुखंड[^22] पथ कुछ भी हो सकता है, हालांकि पहले अनुखंड[^22] पथ अंग के नाम में एक बिंदु होना चाहिए (Go का वर्तमान संस्करण अब इसे लागू नहीं करता है, लेकिन यदि आप थोड़े पुराने संस्करणों का उपयोग कर रहे हैं तो आश्चर्यचकित न हों यदि आपका निर्माण[^23] विफल हो जाए)। यदि आप चाहें तो विवाद [`३७५५४`](https://github.com/golang/go/issues/37554) और [`३२८१९`](https://github.com/golang/go/issues/32819) इसके बारे में और अधिक जानने के लिए देखें।

यह परियोजना[^2] अभिन्यास[^3] जानबूझकर सामान्य है और यह किसी विशिष्ट Go संकुल[^15] संरचना[^4] को लागू करने का प्रयास नहीं करती है।

यह एक सामुदायिक प्रयास है। यदि आपको कोई नया नमूनां[^7] दिखाई देता है या आपको लगता है कि मौजूदा नमूनों[^7] में से किसी एक को अद्यतन करने की आवश्यकता है, तो एक विवाद खोलें।

यदि आपको नामकरण, संरूपण, और शैली[^24] में मदद चाहिए तो [`gofmt`](https://golang.org/cmd/gofmt/) और [`staticcheck`](https://github.com/dominikh/go-tools/tree/master/cmd/staticcheck) चलाकर शुरुआत करें। पिछला मानक[^0] लिंटर[^25], golint, अब अप्रचलित है और इसका रखरखाव नहीं किया जा रहा है; staticcheck जैसे रखरखाव किए गए लिंटर[^25] के उपयोग की अनुशंसा[^26] की जाती है। इन Go कोड[^13] शैली[^24] दिशानिर्देशों और अनुशंसाओं[^26] को पढ़ना भी सुनिश्चित करें:

* <https://talks.golang.org/2014/names.slide>
* <https://golang.org/doc/effective_go.html#names>
* <https://blog.golang.org/package-names>
* <https://go.dev/wiki/CodeReviewComments>
* [Style guideline for Go packages](https://rakyll.org/style-packages) (rakyll/JBD)

अतिरिक्त पृष्ठभूमि जानकारी के लिए [`Go Project Layout`](https://medium.com/golang-learn/go-project-layout-e5213cdcfaa2) देखें।

संकुलों[^15] के नामकरण और आयोजन के साथ-साथ अन्य कोड[^13] संरचना[^4] अनुशंसाओं[^26] के बारे में अधिक जानकारी:

* [GopherCon EU 2018: Peter Bourgon - Best Practices for Industrial Programming](https://www.youtube.com/watch?v=PTE4VJIdHPg)
* [GopherCon Russia 2018: Ashley McNamara + Brian Ketelsen - Go best practices.](https://www.youtube.com/watch?v=MzTcsI6tn-0)
* [GopherCon 2017: Edward Muller - Go Anti-Patterns](https://www.youtube.com/watch?v=ltqV6pDKZD8)
* [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps](https://www.youtube.com/watch?v=oL6JBUk6tj0)

## Go फ़ोल्डर

### `/cmd`

इस परियोजना[^2] के लिए मुख्य अनुप्रयोग।

प्रत्येक एप्लिकेशन[^1] के लिए फ़ोल्डर[^8] का नाम उस executable के नाम से मेल खाना चाहिए जिसे आप रखना चाहते हैं (उदाहरण के लिए, `/cmd/myapp`)।

एप्लिकेशन[^1] फ़ोल्डर[^8] में बहुत सारा कोड[^13] न डालें। यदि आपको लगता है कि कोड[^13] को आयात[^10] किया जा सकता है और अन्य परियोजनाओं[^2] में उपयोग किया जा सकता है, तो इसे `/pkg` फ़ोल्डर[^8] में रहना चाहिए। यदि कोड[^13] पुन: उपयोग करने योग्य नहीं है या यदि आप नहीं चाहते कि अन्य लोग इसका पुन: उपयोग करें, तो उस कोड[^13] को `/internal` फ़ोल्डर[^8] में रखें। आप आश्चर्यचकित होंगे कि दूसरे क्या करेंगे, इसलिए अपने इरादों के बारे में स्पष्ट रहें!

एक छोटा `main` फलन[^27] होना आम बात है जो `/internal` और `/pkg` फ़ोल्डरों[^8] से कोड[^13] आयात[^10] और उपयोग करता है और कुछ नहीं।

उदाहरण के लिए [`/cmd`](cmd/README.md) फ़ोल्डर[^8] देखें।

### `/internal`

निजी एप्लिकेशन[^1] और भंडार[^16] कोड[^13]। यह वह कोड[^13] है जिसे आप नहीं चाहते कि अन्य लोग अपने एप्लिकेशन[^1] या भंडार[^16] में आयात[^10] करें। ध्यान दें कि यह अभिन्यास[^3] नमूनां[^7] Go संकलनकर्ता[^28] द्वारा ही लागू किया गया है। अधिक विवरण के लिए Go १.४ [`release notes`](https://golang.org/doc/go1.4#internalpackages) देखें। ध्यान दें कि आप शीर्ष स्तर की `internal` फ़ोल्डर[^8] तक सीमित नहीं हैं। आपकी परियोजना[^2] संरचना[^4] के किसी भी स्तर पर एक से अधिक `internal` फ़ोल्डर[^8] हो सकते है।

आप वैकल्पिक रूप से अपने साझा और गैर-साझा आंतरिक कोड[^13] को अलग करने के लिए अपने आंतरिक संकुलों[^15] में कुछ अतिरिक्त संरचना[^4] जोड़ सकते हैं। इसकी आवश्यकता नहीं है (विशेषकर छोटी परियोजनाओं[^2] के लिए), लेकिन इच्छित संकुल[^15] उपयोग को दर्शाने वाले दृश्य सुराग होना अच्छा है। आपका वास्तविक एप्लिकेशन[^1] कोड[^13] `/internal/app` फ़ोल्डर[^8] में जा सकता है (उदाहरण के लिए, `/internal/app/myapp`) और उन एप्लिकेशनों[^1] द्वारा साझा किया गया कोड[^13] `/internal/pkg` फ़ोल्डर[^8] में जा सकता है (उदाहरण के लिए, `/internal/pkg/myprivlib`).

### `/pkg`

भंडार[^16] कोड[^13] जो बाहरी एप्लिकेशनों[^1] द्वारा उपयोग करने के लिए ठीक है (उदाहरण के लिए, `/pkg/mypubliclib`)। अन्य परियोजनाएं[^2] इन भंडारों[^16] को काम करने की उम्मीद में आयात[^10] करेंगी, इसलिए यहां कुछ भी डालने से पहले दो बार सोचें :smile:। ध्यान दें कि `internal` फ़ोल्डर[^8] यह सुनिश्चित करने का एक बेहतर तरीका है कि आपके निजी संकुल[^15] आयात[^10] योग्य नहीं हैं क्योंकि यह Go द्वारा लागू किया गया है। `/pkg` फ़ोल्डर[^8] अभी भी स्पष्ट रूप से यह बताने का एक अच्छा तरीका है कि उस फ़ोल्डर[^8] का कोड[^13] दूसरों के उपयोग के लिए सुरक्षित है। Travis Jeffrey द्वारा [`I'll take pkg over internal`](https://travisjeffery.com/b/2019/11/i-ll-take-pkg-over-internal/) ब्लॉग लेख `pkg` और `internal` फ़ोल्डरों[^8] का एक अच्छा अवलोकन[^29] प्रदान करता है और कब उनका उपयोग करना उचित हो सकता है।

यह Go कोड[^13] को एक ही स्थान पर समूहित करने का एक तरीका है जब आपके मूल[^5] फ़ोल्डर[^8] में बहुत सारे गैर-Go अंग और फ़ोल्डर[^8] होते हैं जिससे विभिन्न Go उपकरण[^30] चलाना आसान हो जाता है (जैसा कि इन वार्ताओं में बताया गया है: [`Best Practices for Industrial Programming`](https://www.youtube.com/watch?v=PTE4VJIdHPg) GopherCon EU २०१८ से, [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps](https://www.youtube.com/watch?v=oL6JBUk6tj0) और [GoLab 2018 - Massimiliano Pippi - Project layout patterns in Go](https://www.youtube.com/watch?v=3gQa1LWwuzk))।

यदि आप देखना चाहते हैं कि कौनसी लोकप्रिय Go रिपॉजिटरीयाँ[^19] इस परियोजना[^2] अभिन्यास[^3] का उपयोग करती हैं तो [`/pkg`](pkg/README.md) फ़ोल्डर[^8] देखें। यह एक सामान्य अभिन्यास[^3] नमूनां[^7] है, लेकिन यह सार्वभौमिक[^20] रूप से स्वीकृत नहीं है और Go समुदाय के कुछ लोग इसकी अनुशंसा[^26] नहीं करते हैं।

यदि आपकी एप्लिकेशन[^1] परियोजना[^2] वास्तव में छोटी है और जहां अतिरिक्त स्तर का नेस्टिंग[^31] अधिक मूल्य नहीं जोड़ता है (जब तक कि आप वास्तव में नहीं चाहते :smile:) तो इसका उपयोग न करना ठीक है। इसके बारे में तब सोचें जब यह काफी बड़ी हो रहा हो और आपका मूल[^5] फ़ोल्डर[^8] काफी व्यस्त हो जाए (खासकर यदि आपके पास बहुत सारे गैर-Go एप्लिकेशन[^1] अंग हैं)।

`pkg` फ़ोल्डर[^8] की उत्पत्ति: पुराने Go स्रोत[^18] कोड[^13] द्वारा अपने संकुलों[^15] के लिए `pkg` का उपयोग किया जाता था और फिर समुदाय में विभिन्न Go परियोजनाओं[^2] ने नमूनें[^7] की प्रतिलिपि बनाना शुरू कर दिया (अधिक संदर्भ के लिए Brad Fitzpatrick का [`यह`](https://x.com/bradfitz/status/1039512487538970624) &#x1D54F; (पूर्व Twitter) पोस्ट[^32] देखें)।

### `/vendor`

एप्लिकेशन[^1] निर्भरताएं[^14] (हाथों से या आपके पसंदीदा निर्भरता[^14] प्रबंधन[^17] उपकरण[^30] जैसे नए अंतर्निहित[^33] [`Go Modules`](https://go.dev/wiki/Modules) सुविधा द्वारा प्रबंधित[^17])। `go mod vendor` निर्देश[^34] आपके लिए `/vendor` फ़ोल्डर[^8] बनाएगा। ध्यान दें कि यदि आप Go १.१४ का उपयोग नहीं कर रहे हैं, जहाँ यह पूर्व-निर्धारित[^35] रूप से चालू है, तो आपको अपने `go build` निर्देश[^34] में `-mod=vendor` सूचक[^36] जोड़ने की आवश्यकता हो सकती है।

यदि आप भंडार[^16] का निर्माण[^23] कर रहे हैं तो अपनी एप्लिकेशन[^1] निर्भरताऔं[^14] को सुपुर्द[^37] न करें।

ध्यान दें कि चूंकि [`1.13`](https://golang.org/doc/go1.13#modules) से Go ने अनुखंड[^22] प्रॉक्सी[^38] सुविधा को भी सक्षम किया है (<https://proxy.golang.org> का उपयोग करके) पूर्व-निर्धारित[^35] रूप से उनके अनुखंड[^22] प्रॉक्सी[^38] सर्वर[^39] के रूप में। इसके बारे में और अधिक पढ़ें [`यहाँ`](https://blog.golang.org/module-mirror-launch) यह देखने के लिए कि क्या यह आपकी सभी आवश्यकताओं और बाधाओं पर फिट बैठता है। यदि ऐसा होता है, तो आपको `vendor` फ़ोल्डर[^8] की बिल्कुल भी आवश्यकता नहीं होगी।

## सेवा एप्लिकेशन फ़ोल्डर

### `/api`

OpenAPI/Swagger विनिर्देशों[^40], JSON स्कीमा[^41] फ़ाइलों[^21], प्रोटोकॉल[^42] परिभाषा फ़ाइलों[^21] के लिए।

उदाहरण के लिए [`/api`](api/README.md) फ़ोल्डर[^8] देखें।

## वेब एप्लिकेशन फ़ोल्डर

### `/web`

वेब[^43] एप्लिकेशन[^1] विशिष्ट अंग: स्थिर वेब[^43] संपत्तियाँ[^61], सर्वर[^39] पक्ष टेम्पलेट[^44] और SPA (एक पृष्ठ एप्लिकेशन[^1])।

## सामान्य एप्लिकेशन फ़ोल्डर

### `/configs`

कॉन्फ़िगरेशन[^45] फ़ाइल[^21] टेम्पलेट[^44] या पूर्व-निर्धारित[^35] कॉन्फ़िगरेशन[^45]।

अपनी `confd` या `consul-template` टेम्प्लेट[^44] फ़ाइलें[^21] यहाँ रखें।

### `/init`

तंत्र[^46] प्रारंभिकरण[^47] (systemd, upstart, sysv) और प्रक्रिया[^48] प्रबंधक[^17]/पर्यवेक्षक (runit, supervisord) कॉन्फ़िगरेशन[^45]।

### `/scripts`

विभिन्न निर्माण[^23], स्थापना[^11], विश्लेषण आदि संचालन करने के लिए स्क्रिप्टें[^49]।

ये स्क्रिप्टें[^49] मूल[^5] स्तर कि Makefile को छोटा और सरल रखती हैं (उदाहरण के लिए, <https://github.com/hashicorp/terraform/blob/main/Makefile>).

उदाहरण के लिए [`/scripts`](scripts/README.md) फ़ोल्डर[^8] देखें।

### `/build`

Packaging और Continuous Integration।

अपने क्लाउड[^50] (AMI), कंटेनर[^51] (Docker), OS (deb, rpm, pkg) संकुल[^15] कॉन्फ़िगरेशनों[^45] और स्क्रिप्टों[^49] को `/build/package` फ़ोल्डर[^8] में रखें।

अपने CI (travis, circle, drone) कॉन्फ़िगरेशनों[^45] और स्क्रिप्टों[^49] को `/build/ci` फ़ोल्डर[^8] में रखें। ध्यान दें कि कुछ CI उपकरण[^30] (उदाहरण के लिए, Travis CI) अपनी कॉन्फ़िगरेशन[^45] फ़ाइलों[^21] के स्थान के बारे में बहुत चुनिंदा हैं। कॉन्फ़िगरेशन[^45] फ़ाइलों[^21] को `/build/ci` फ़ोल्डर[^8] में डालने का प्रयास करें और उन्हें उस स्थान से लिंक[^52] करें जहाँ CI उपकरण[^30] उनसे अपेक्षा करते हैं (जब संभव हो)।

### `/deployments`

IaaS, PaaS, तंत्र[^46] और कंटेनर[^51] ऑर्केस्ट्रेशन[^53] परिनियोजन[^54] कॉन्फ़िगरेशनों[^45] और टेम्पलेटों[^44] (docker-compose, kubernetes/helm, terraform)। ध्यान दें कि कुछ रिपॉजिटरीयाँ[^19] (विशेष रूप से kubernetes के साथ परिनियोजित[^54] एप्लिकेशनें[^1]) में इस फ़ोल्डर[^8] को `/deploy` कहा जाता है।

### `/test`

अतिरिक्त बाहरी परीक्षण[^55] एप्लिकेशनों[^1] और परीक्षण[^55] डेटा[^56] के लिए। बेझिझक `/test` फ़ोल्डर[^8] को अपनी इच्छानुसार संरचित[^4] करें। बड़ी परियोजनाओं[^2] के लिए डेटा[^56] उप-फ़ोल्डर[^8] का होना सार्थक है। उदाहरण के लिए, यदि आप चाहते हैं कि उस फ़ोल्डर[^8] में जो कुछ है उसे अनदेखा करें तो आपके पास `/test/data` या `/test/testdata` हो सकता है। ध्यान दें कि Go "." या "_" से शुरू होने वाले फ़ोल्डरों[^8] या फ़ाइलों[^21] को भी अनदेखा कर देगा, इसलिए आपके पास अपने परीक्षण[^55] डेटा[^56] फ़ोल्डर[^8] को नाम देने के मामले में अधिक लचीलापन है।

उदाहरणों के लिए [`/test`](test/README.md) फ़ोल्डर[^8] देखें।

## अन्य फ़ोल्डर

### `/docs`

डिज़ाइन[^57] और उपयोगकर्ता दस्तावेज़ों[^9] (आपके godoc द्वारा उत्पन्न दस्तावेज़ों[^9] के अतिरिक्त) के लिए।

उदाहरणों के लिए [`/docs`](docs/README.md) फ़ोल्डर[^8] देखें।

### `/tools`

परियोजना[^2] के लिए सहायक उपकरणों[^30] के लिए। ध्यान दें कि ये उपकरण[^30] `/pkg` और `/internal` फ़ोल्डरों[^8] से कोड[^13] आयात[^10] कर सकते हैं।

उदाहरणों के लिए [`/tools`](tools/README.md) फ़ोल्डर[^8] देखें।

### `/examples`

आपकी एप्लिकेशनों[^1] और/या सार्वजनिक[^58] भंडारों[^16] के लिए उदाहरणों के लिए।

उदाहरणों के लिए [`/examples`](examples/README.md) फ़ोल्डर[^8] देखें।

### `/third_party`

बाहरी सहायक उपकरणों[^30], फोर्क[^59] किया हुए कोड[^13] और अन्य तृतीय पक्ष उपयोगिताऔं (उदाहरण के लिए, Swagger UI) के लिए।

### `/githooks`

Git हुकों[^60] के लिए।

### `/assets`

अन्य संपत्तियाँ[^61] जैसे चित्र, प्रतीक-चिन्ह[^62] इत्यादि के लिए जो परियोजना[^2] से संबंधित हैं।

### `/website`

यदि आप GitHub Pages का उपयोग नहीं कर रहे हैं तो यह आपकी परियोजना[^2] की वेबसाइट[^63] डेटा[^56] डालने का स्थान है।

उदाहरणों के लिए [`/website`](website/README.md) फ़ोल्डर[^8] देखें।

## फ़ोल्डर जो आपके पास नहीं होना चाहिए

### `/src`

कुछ Go परियोजनाओं[^2] में एक `src` फ़ोल्डर[^8] होता है, लेकिन यह आमतौर पर तब होता है जब डेवलपर[^6] Java दुनिया से आते हैं जहाँ यह एक सामान्य नमूनां[^7] है। यदि आप अपनी मदद कर सकते हैं तो इस Java नमूनें[^7] को न अपनाने का प्रयास करें। आप वास्तव में नहीं चाहते कि आपका Go कोड[^13] या Go परियोजना[^2] Java जैसे दिखें। :smile:

परियोजना[^2] स्तर के `/src` फ़ोल्डर[^8] को उस `/src` फ़ोल्डर[^8] के साथ भ्रमित न करें जिसका उपयोग Go अपने कार्यक्षेत्रों[^64] के लिए करता है जैसा कि [`How to Write Go Code`](https://golang.org/doc/code.html) में वर्णित है। `$GOPATH` पर्यावरण चर[^65] आपके (वर्तमान) कार्यक्षेत्र[^64] को इंगित करता है (डिफ़ॉल्ट रूप से यह गैर-Windows तंत्र[^46] पर `$HOME/go` को इंगित करता है)। इस कार्यक्षेत्र[^64] में शीर्ष स्तर `/pkg`, `/bin` और `/src` फ़ोल्डरें[^8] शामिल हैं। आपकी वास्तविक परियोजना[^2] `/src` के अंतर्गत एक उप-फ़ोल्डर[^8] बनकर समाप्त होता है, इसलिए यदि आपकी परियोजना[^2] में `/src` फ़ोल्डर[^8] है तो परियोजना[^2] पथ इस तरह दिखेगा: `/some/path/to/workspace/src/your_project/src/your_code.go`. ध्यान दें कि Go १.११ के साथ आपकी परियोजना[^2] को आपके `$GOPATH` के बाहर रखना संभव है, लेकिन फिर भी इसका मतलब यह नहीं है कि इस अभिन्यास[^3] नमूनें[^7] का उपयोग करना एक अच्छा विचार है।

## बैज

* [Go Report Card](https://goreportcard.com/) - यह आपके कोड[^13] को `gofmt`, `go vet`, `gocyclo`, `golint`, `ineffassign`, `license` और `misspell` के साथ स्कैन करेगा। `github.com/golang-standards/project-layout` को अपनी परियोजना[^2] संदर्भ से बदलें।

  [![Go Report Card](https://goreportcard.com/badge/github.com/golang-standards/project-layout?style=flat-square)](https://goreportcard.com/report/github.com/golang-standards/project-layout)

* ~~[GoDoc](http://godoc.org) - यह आपके GoDoc जनित दस्तावेज़[^9] का ऑनलाइन संस्करण प्रदान करेगा। अपनी परियोजना[^2] को इंगित करने के लिए लिंक[^52] बदलें।~~

  [![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/golang-standards/project-layout)

* [pkg.go.dev](https://pkg.go.dev) - pkg.go.dev Go खोज और दस्तावेज़ों[^9] के लिए एक नया ठिकाना है। आप [बैज निर्माण[^23] उपकरण[^30]](https://pkg.go.dev/badge) का उपयोग करके एक बैज बना सकते हैं।

  [![PkgGoDev](https://pkg.go.dev/badge/github.com/golang-standards/project-layout)](https://pkg.go.dev/github.com/golang-standards/project-layout)

* प्रकाशन - यह आपकी परियोजना[^2] के लिए नवीनतम प्रकाशन अंक दिखाएगा। अपनी परियोजना[^2] को इंगित करने के लिए GitHub लिंक[^52] बदलें।

  [![Release](https://img.shields.io/github/release/golang-standards/project-layout.svg?style=flat-square)](https://github.com/golang-standards/project-layout/releases/latest)

## टिप्पणी

नमूनें[^7]/पुन: उपयोगी कॉन्फ़िगरेशनें[^45], स्क्रिप्टें[^49] और कोड[^13] के साथ एक अधिक विचारशील परियोजना[^2] टेम्पलेट[^44] कार्य प्रगति पर है।

## शब्द सूची

नीचे दिए गए तिरछे शब्द आगत शब्द हैं।

[^0]: मानक - standard
[^1]: *एप/एप्लिकेशन* - app/application
[^2]: परियोजना - project
[^3]: अभिन्यास - layout
[^4]: संरचना - structure
[^5]: मूल - core/root
[^6]: *डेव/डेवलपर* - dev/developer
[^7]: नमूनां - pattern
[^8]: *फ़ोल्डर* - folder
[^9]: दस्तावेज़ - document
[^10]: आयात - import
[^11]: स्थापन - install
[^12]: अवधारणा प्रमाण - proof of concept
[^13]: *कोड* - code
[^14]: निर्भरता - dependency
[^15]: संकुल - package
[^16]: भंडार - library
[^17]: प्रबंध - manage
[^18]: स्रोत - source
[^19]: *रिपॉजिटरी* - repository
[^20]: सार्वभौमिक - universal
[^21]: *फ़ाइल* - file
[^22]: अनुखंड - module
[^23]: निर्माण - build
[^24]: शैली - style
[^25]: *लिंट* - lint
[^26]: अनुशंसा - recommend
[^27]: फलन - function
[^28]: संकलनकर्ता - compiler
[^29]: अवलोकन - overview
[^30]: उपकरण - tool
[^31]: *नेस्टिंग* - nesting
[^32]: *पोस्ट* - post
[^33]: अंतर्निहित - built-in
[^34]: निर्देश - command
[^35]: पूर्व-निर्धारित - default
[^36]: सूचक - flag
[^37]: सुपुर्द - commit
[^38]: *प्रॉक्सी* - proxy
[^39]: *सर्वर* - server
[^40]: विनिर्देश - specification
[^41]: *स्कीमा* - schema
[^42]: *प्रोटोकॉल* - protocol
[^43]: वेब - web
[^44]: टेम्पलेट - template
[^45]: *कॉन्फ़िग/कॉन्फ़िगर* - config/configure
[^46]: तंत्र - system
[^47]: प्रारंभिकरण - init/initialization
[^48]: प्रक्रिया - process
[^49]: *स्क्रिप्ट* - script
[^50]: *क्लाउड* - cloud
[^51]: *कंटेनर* - container
[^52]: *लिंक* - link
[^53]: *ऑर्केस्ट्रेशन* - orchestration
[^54]: परिनियोजन - deployment
[^55]: परीक्षण - testing
[^56]: *डेटा* - data
[^57]: *डिज़ाइन* - design
[^58]: सार्वजनिक - public
[^59]: *फोर्क* - fork
[^60]: *हुक* - hook
[^61]: संपत्ति - asset
[^62]: प्रतीक-चिन्ह - logo
[^63]: *वेबसाइट* - website
[^64]: कार्यक्षेत्र - workspace
[^65]: चर - variable