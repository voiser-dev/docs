Text to Speech
===================================

You can use the `Create API`_ to convert the text you have to audio.

.. note::

   You can voice a maximum of 30,000 characters at once.


.. _Create API:

Create API
----------

You can create a project and download your file by giving the text you want to convert to audio to this API.

.. http:post:: https://api.voiser.net/v2/limitless/

**Request Parameters**

    - **authCode -** Your Voiser user code.
    - **articleText -** The text you want to convert to audio.
    - **configVoice -** Voice name. (`All Voices`_)
    - **configLang -** Language code to be used. (`All Languages`_)
    - **configPitch -** Pitch (Should be 0 for normal reading, Min. -4.00, Max. +4.00)
    - **configSpeed -** Reading speed (Should be 1 for normal reading, Min. 0.3, Max. 4.0)

**Response Parameters**

    - **status -** If it returns *success*, the record has been created, if it returns *error*, a problem has occurred.
    - **processTime -** Audio generation processing time.
    - **barkod -** Audio barcode.
    - **counter -** Word limit remaining in your account.
    - **fileUrl -** The url of the audio file.
    - **createTime -** Date and time the sound was created.



**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'authCode' => 'YOUR_USER_CODE',
            'articleText' => 'Hello World!',
            'configVoice' => 'Aria',
            'configLang' => 'en-US',
            'configPitch' => '1.0',
            'configSpeed' => '1.0'
        );

        $ch = curl_init('https://api.voiser.net/v2/limitless/');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'authCode': 'YOUR_USER_CODE',
            'articleText': 'Hello World!',
            'configVoice': 'Jenny Multilingual',
            'configLang': 'en-US',
            'configPitch': '1.0',
            'configSpeed': '1.0'
        }
        response = requests.post('https://api.voiser.net/v2/limitless/', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
        "status": "success",
        "processTime": 2.55,
        "barkod": "ABCD",
        "counter": 79972,
        "fileUrl": "AUDIO_FILE_URL",
        "durationSeconds": 573,
        "durationFormat": "00:00:03",
        "createTime": "2022-10-01 10:40:53"
    }


.. _All Languages:

Languages
---------
======================================== ============
Language                                 Code
======================================== ============
Multilingual                             multilingual
Afrikaans (South Africa)                 af-ZA
Albanian (Albania)                       sq-AL
Amharic (Ethiopia)                       am-ET
Arabic (Algeria)                         ar-DZ
Arabic (Bahrain)                         ar-BH
Arabic (Egypt)                           ar-EG
Arabic (Iraq)                            ar-IQ
Arabic (Jordan)                          ar-JO
Arabic (Kuwait)                          ar-KW
Arabic (Lebanon)                         ar-LB
Arabic (Libya)                           ar-LY
Arabic (Morocco)                         ar-MA
Arabic (Oman)                            ar-OM
Arabic (Qatar)                           ar-QA
Arabic (Saudi Arabia)                    ar-SA
Arabic (Syria)                           ar-SY
Arabic (Tunisia)                         ar-TN
Arabic (United Arab Emirates)            ar-AE
Arabic (Yemen)                           ar-YE
Azerbaijani (Azerbaijan)                 az-AZ
Bengali (Bangladesh)                     bn-BD
Bengali (India)                          bn-IN
Bosnian (Bosnia and Herzegovina)         bs-BA
Bulgarian                                bg-BG
Burmese (Myanmar)                        my-MM
Catalan (Spanish)                        ca-ES
Chinese (Cantoneo)                       zh-HK
Chinese (Mandarin)                       zh-CN
Chinese (Mandarin, Simplified, Liaoning) zh-CN-LN
Chinese (Mandarin, Simplified, Sichuan)  zh-CN-SC
Croatian                                 hr-HR
Czech                                    cs-CZ
Danish                                   da-DK
Dutch (Belgium)                          nl-BE
Dutch (Netherlands)                      nl-NL
English (American)                       en-US
English (Australia)                      en-AU
English (British)                        en-GB
English (Canada)                         en-CA
English (Hongkong)                       en-HK
English (India)                          en-IN
English (Ireland)                        en-IE
English (Kenya)                          en-KE
English (New Zealand)                    en-NZ
English (Nigeria)                        en-NG
English (Philippines)                    en-PH
English (Singapore)                      en-SG
English (South Africa)                   en-ZA
English (Tanzania)                       en-TZ
Estonian (Estonia)                       et-EE
Filipino                                 fil-PH
Finnish (Finland)                        fi-FI
French (Belgium)                         fr-BE
French (Canada)                          fr-CA
French (France)                          fr-FR
French (Switzerland)                     fr-CH
Galician (Spain)                         gl-ES
Georgian (Georgia)                       ka-GE
German (Austria)                         de-AT
German (Germany)                         de-DE
German (Switzerland)                     de-CH
Greek                                    el-GR
Gujarati (India)                         gu-IN
Hebrew (Israel)                          he-IL
Hindi                                    hi-IN
Hungarian                                hu-HU
Icelandic (Iceland)                      is-IS
Indonesian                               id-ID
Irish (Ireland)                          ga-IE
Italian                                  it-IT
Japanese                                 ja-JP
Javanese (Indonesia)                     jv-ID
Kannada (India)                          kn-IN
Kazakh (Kazakhstan)                      kk-KZ
Khmer (Cambodia)                         km-KH
Korean                                   ko-KR
Lao (Laos)                               lo-LA
Latvian (Latvia)                         lv-LV
Lithuanian (Lithuania)                   lt-LT
Macedonian (Republic of North Macedonia) mk-MK
Malay (Malaysia)                         ms-MY
Malayalam (India)                        ml-IN
Maltese (Malta)                          mt-MT
Marathi (India)                          mr-IN
Mongolian (Mongolia)                     mn-MN
Nepali (Nepal)                           ne-NP
Norwegian                                nb-NO
Pashto (Afghanistan)                     ps-AF
Persian (Iran)                           fa-IR
Polish (Poland)                          pl-PL
Portuguese                               pt-PT
Portuguese (Brazil)                      pt-BR
Romanian (Romania)                       ro-RO
Russian                                  ru-RU
Serbian (Serbia, Cyrillic)               sr-RS
Sinhala (Sri Lanka)                      si-LK
Slovak (Slovakia)                        sk-SK
Slovenian                                sl-SI
Somali (Somalia)                         so-SO
Spanish (Argentina)                      es-AR
Spanish (Bolivia)                        es-BO
Spanish (Chile)                          es-CL
Spanish (Colombia)                       es-CO
Spanish (Costa Rica)                     es-CR
Spanish (Cuba)                           es-CU
Spanish (Dominican Republic)             es-DO
Spanish (Ecuador)                        es-EC
Spanish (El Salvador)                    es-SV
Spanish (Equatorial Guinea)              es-GQ
Spanish (Guatemala)                      es-GT
Spanish (Honduras)                       es-HN
Spanish (Mexico)                         es-MX
Spanish (Nicaragua)                      es-NI
Spanish (Panama)                         es-PA
Spanish (Paraguay)                       es-PY
Spanish (Peru)                           es-PE
Spanish (Puerto Rico)                    es-PR
Spanish (Spain)                          es-ES
Spanish (United States)                  es-US
Spanish (Uruguay)                        es-UY
Spanish (Venezuela)                      es-VE
Sundanese (Indonesia)                    su-ID
Swahili (Kenya)                          sw-KE
Swahili (Tanzania)                       sw-TZ
Swedish                                  sv-SE
Taiwan                                   zh-TW
Tamil (India)                            ta-IN
Tamil (Malaysia)                         ta-MY
Tamil (Singapore)                        ta-SG
Tamil (Sri Lanka)                        ta-LK
Telugu (India)                           te-IN
Thai (Thailand)                          th-TH
Turkish                                  tr-TR
Ukrainian                                uk-UA
Urdu (India)                             ur-IN
Urdu (Pakistan)                          ur-PK
Uzbek (Uzbekistan)                       uz-UZ
Vietnamese                               vi-VN
Welsh (United Kingdom)                   cy-GB
Zulu (South Africa)                      zu-ZA
======================================== ==========

.. _All Voices:

Voices
------------
================== =======================================================
Voice Name         Language
================== =======================================================
Ada                Multilingual
Adam               Multilingual
Alessio            Multilingual
Alex               Multilingual
Amanda             Multilingual
Andrew             Multilingual
Arabella           Multilingual
Ava                Multilingual
Brandon            Multilingual
Brian              Multilingual
Caroline           Multilingual
Derek              Multilingual
Dustin             Multilingual
Florian            Multilingual
Giuseppe           Multilingual
Hyunsu             Multilingual
Isabella           Multilingual
Isidora            Multilingual
James              Multilingual
Lena               Multilingual
Lewis              Multilingual
Lily               Multilingual
Lola               Multilingual
Lucien             Multilingual
Macerio            Multilingual
Marcello           Multilingual
Masaru             Multilingual
Mia                Multilingual
Nancy              Multilingual
Ollie              Multilingual
Phoebe             Multilingual
Remy               Multilingual
Ryan               Multilingual
Samuel             Multilingual
Seraphina          Multilingual
Serena             Multilingual
Steffan            Multilingual
Thalita            Multilingual
Tristan            Multilingual
Vivienne           Multilingual
Xiaochen           Multilingual
Xiaoxiao           Multilingual
Xiaoyu             Multilingual
Ximena             Multilingual
Yunfan             Multilingual
Yunxiao            Multilingual
Yunyi              Multilingual
Jenny Multilingual English (American)
Giorgi             ka-GE                                    
Abeo               en-NG                                    
YunxiSichuan       zh-CN-SC                                 
Abbi               English (British)                        
Bella              English (British)                        
Hollie             English (British)                        
Maisie             English (British)                        
Mia                English (British)                        
Olivia             English (British)                        
Alfie              English (British)                        
Elliot             English (British)                        
Ethan              English (British)                        
Noah               English (British)                        
Oliver             English (British)                        
Thomas             English (British)                        
Libby              English (British)                        
Sonia              English (British)                        
Ryan               English (British)                        
Jane               English (American)                       
Nancy              English (American)                       
Davis              English (American)                       
Jason              English (American)                       
Tony               English (American)                       
Aria               English (American)                       
Jenny              English (American)                       
Guy                English (American)                       
Joseph             English (American)                       
Amber              English (American)                       
Ashley             English (American)                       
Cora               English (American)                       
Elizabeth          English (American)                       
Michelle           English (American)                       
Monica             English (American)                       
Sara               English (American)                       
Brandon            English (American)                       
Christopher        English (American)                       
Eric               English (American)                       
Jacob              English (American)                       
Ana [Kid]          English (American)                       
Natasha            English (Australia)                      
William            English (Australia)                      
Meryem             Turkish                                  
İbrahim            Turkish                                  
خدیجه              Arabic (Saudi Arabia)                    
عمر                Arabic (Saudi Arabia)                    
Amala              German (Germany)                         
Elke               German (Germany)                         
Gisela [Kid]       German (Germany)                         
Klarissa           German (Germany)                         
Louisa             German (Germany)                         
Maja               German (Germany)                         
Tanja              German (Germany)                         
Bernd              German (Germany)                         
Christoph          German (Germany)                         
Kasper             German (Germany)                         
Killian            German (Germany)                         
Klaus              German (Germany)                         
Ralf               German (Germany)                         
Katja              German (Germany)                         
Conrad             German (Germany)                         
Fabiola            Italian                                  
Fiamma             Italian                                  
Imelda             Italian                                  
Irma               Italian                                  
Palmira            Italian                                  
Pierina            Italian                                  
Benigno            Italian                                  
Calimero           Italian                                  
Cataldo            Italian                                  
Gianni             Italian                                  
Lisandro           Italian                                  
Rinaldo            Italian                                  
Elsa               Italian                                  
Isabella           Italian                                  
Diego              Italian                                  
Elvira             Spanish (Spain)                          
Alvaro             Spanish (Spain)                          
Dariya             Russian                                  
Svetlana           Russian                                  
Dmitry             Russian                                  
Xiaochen           Chinese (Mandarin)                       
Xiaoqiu            Chinese (Mandarin)                       
Xiaoshuang         Chinese (Mandarin)                       
Xiaoyan            Chinese (Mandarin)                       
Xiaohan            Chinese (Mandarin)                       
Xiaomo             Chinese (Mandarin)                       
Xiaorui            Chinese (Mandarin)                       
Xiaoxuan           Chinese (Mandarin)                       
Yunxi              Chinese (Mandarin)                       
Yunyang            Chinese (Mandarin)                       
Yunfeng            Chinese (Mandarin)                       
Yunhao             Chinese (Mandarin)                       
Yunjian            Chinese (Mandarin)                       
Xiaoxiao           Chinese (Mandarin)                       
Xiaoyou            Chinese (Mandarin)                       
Yunye              Chinese (Mandarin)                       
HsiaoChen          Taiwan                                   
HsiaoYu            Taiwan                                   
YunJhe             Taiwan                                   
Vlasta             Czech                                    
Antonin            Czech                                    
Christel           Danish                                   
Jeppe              Danish                                   
Liam               Danish                                   
Gadis              Indonesian                               
Ardi               Indonesian                               
Hillevi            Swedish                                  
Sofie              Swedish                                  
Mattias            Swedish                                  
Swara              Hindi                                    
Madhur             Hindi                                    
Colette            Dutch (Netherlands)                      
Fenna              Dutch (Netherlands)                      
Maarten            Dutch (Netherlands)                      
Blessica           Filipino                                 
Angelo             Filipino                                 
Noora              Finnish (Finland)                        
Selma              Finnish (Finland)                        
Harri              Finnish (Finland)                        
Nanami             Japanese                                 
Keita              Japanese                                 
SunHi              Korean                                   
InJoon             Korean                                   
Noemi              Hungarian                                
Tamas              Hungarian                                
Iselin             Norwegian                                
Pernille           Norwegian                                
Finn               Norwegian                                
Polina             Ukrainian                                
Ostap              Ukrainian                                
Agnieszka          Polish (Poland)                          
Zofia              Polish (Poland)                          
Marek              Polish (Poland)                          
Fernanda           Portuguese                               
Raquel             Portuguese                               
Duarte             Portuguese                               
Viktoria           Slovak (Slovakia)                        
Lukas              Slovak (Slovakia)                        
HoaiMy             Vietnamese                               
NamMinh            Vietnamese                               
Athina             Greek                                    
Nestoras           Greek                                    
Brigitte           French (France)                          
Celeste            French (France)                          
Coralie            French (France)                          
Eloise [Kid]       French (France)                          
Jacqueline         French (France)                          
Josephine          French (France)                          
Yvette             French (France)                          
Alain              French (France)                          
Claude             French (France)                          
Jerome             French (France)                          
Maurice            French (France)                          
Yves               French (France)                          
Denise             French (France)                          
Henri              French (France)                          
سماء               Arabic (Egypt)                           
يوسف               Arabic (Egypt)                           
Kalina             Bulgarian                                
Borislav           Bulgarian                                
Alba               Catalan (Spanish)                        
Joana              Catalan (Spanish)                        
Enric              Catalan (Spanish)                        
HiuGaai            Chinese (Cantoneo)                       
HiuMaan            Chinese (Cantoneo)                       
WanLung            Chinese (Cantoneo)                       
Gabrijela          Croatian                                 
Srecko             Croatian                                 
Clara              English (Canada)                         
Neerja             English (India)                          
Prabhat            English (India)                          
Emily              English (Ireland)                        
Connor             English (Ireland)                        
Antoine            French (Canada)                          
Sylvie             French (Canada)                          
Jean               French (Canada)                          
Ariane             French (Switzerland)                     
Fabrice            French (Switzerland)                     
Ingrid             German (Austria)                         
Jonas              German (Austria)                         
Leni               German (Switzerland)                     
Jan                German (Switzerland)                     
Hila               Hebrew (Israel)                          
Avri               Hebrew (Israel)                          
Yasmin             Malay (Malaysia)                         
Osman              Malay (Malaysia)                         
Brenda             Portuguese (Brazil)                      
Elza               Portuguese (Brazil)                      
Giovanna           Portuguese (Brazil)                      
Leila              Portuguese (Brazil)                      
Leticia            Portuguese (Brazil)                      
Manuela            Portuguese (Brazil)                      
Yara               Portuguese (Brazil)                      
Donato             Portuguese (Brazil)                      
Fabio              Portuguese (Brazil)                      
Humberto           Portuguese (Brazil)                      
Julio              Portuguese (Brazil)                      
Nicolau            Portuguese (Brazil)                      
Valerio            Portuguese (Brazil)                      
Francisca          Portuguese (Brazil)                      
Antonio            Portuguese (Brazil)                      
Alina              Romanian (Romania)                       
Emil               Romanian (Romania)                       
Petra              Slovenian                                
Rok                Slovenian                                
Beatriz            Spanish (Mexico)                         
Candela            Spanish (Mexico)                         
Carlota            Spanish (Mexico)                         
Larissa            Spanish (Mexico)                         
Marina             Spanish (Mexico)                         
Nuria              Spanish (Mexico)                         
Renata             Spanish (Mexico)                         
Cecilio            Spanish (Mexico)                         
Gerardo            Spanish (Mexico)                         
Liberto            Spanish (Mexico)                         
Luciano            Spanish (Mexico)                         
Pelayo             Spanish (Mexico)                         
Yago               Spanish (Mexico)                         
Dalia              Spanish (Mexico)                         
Jorge              Spanish (Mexico)                         
Achara             Thai (Thailand)                          
Premwadee          Thai (Thailand)                          
Niwat              Thai (Thailand)                          
Pallavi            Tamil (India)                            
Valluvar           Tamil (India)                            
Shruti             Telugu (India)                           
Mohan              Telugu (India)                           
Dena               Dutch (Belgium)                          
Arnaud             Dutch (Belgium)                          
Yan                English (Hongkong)                       
Sam                English (Hongkong)                       
Molly              English (New Zealand)                    
Mitchell           English (New Zealand)                    
Rosa               English (Philippines)                    
James              English (Philippines)                    
Luna               English (Singapore)                      
Wayne              English (Singapore)                      
Leah               English (South Africa)                   
Luke               English (South Africa)                   
Anu                Estonian (Estonia)                       
Kert               Estonian (Estonia)                       
Charline           French (Belgium)                         
Gerard             French (Belgium)                         
Dhwani             Gujarati (India)                         
Niranjan           Gujarati (India)                         
Orla               Irish (Ireland)                          
Colm               Irish (Ireland)                          
Everita            Latvian (Latvia)                         
Nils               Latvian (Latvia)                         
Ona                Lithuanian (Lithuania)                   
Leonas             Lithuanian (Lithuania)                   
Grace              Maltese (Malta)                          
Aarohi             Marathi (India)                          
Manohar            Marathi (India)                          
Elena              Spanish (Argentina)                      
Tomas              Spanish (Argentina)                      
Salome             Spanish (Colombia)                       
Gonzalo            Spanish (Colombia)                       
Paloma             Spanish (United States)                  
Alonso             Spanish (United States)                  
Zuri               Swahili (Kenya)                          
Rafiki             Swahili (Kenya)                          
Uzma               Urdu (Pakistan)                          
Asad               Urdu (Pakistan)                          
Nia                Welsh (United Kingdom)                   
Aled               Welsh (United Kingdom)                   
Tanishaa           Bengali (India)                          
Bashkar            Bengali (India)                          
Sapna              Kannada (India)                          
Gagan              Kannada (India)                          
Sobhana            Malayalam (India)                        
Midhun             Malayalam (India)                        
Laila              Arabic (Bahrain)                         
Ali                Arabic (Bahrain)                         
Rana               Arabic (Iraq)                            
Bassel             Arabic (Iraq)                            
Sana               Arabic (Jordan)                          
Taim               Arabic (Jordan)                          
Noura              Arabic (Kuwait)                          
Fahed              Arabic (Kuwait)                          
Iman               Arabic (Libya)                           
Omar               Arabic (Libya)                           
Mouna              Arabic (Morocco)                         
Jamal              Arabic (Morocco)                         
Amal               Arabic (Qatar)                           
Moaz               Arabic (Qatar)                           
Amany              Arabic (Syria)                           
Laith              Arabic (Syria)                           
Reem               Arabic (Tunisia)                         
Hedi               Arabic (Tunisia)                         
Fatima             Arabic (United Arab Emirates)            
Hamdan             Arabic (United Arab Emirates)            
Maryam             Arabic (Yemen)                           
Saleh              Arabic (Yemen)                           
Nabanita           Bengali (Bangladesh)                     
Pradeep            Bengali (Bangladesh)                     
Nilar              Burmese (Myanmar)                        
Thiha              Burmese (Myanmar)                        
Asilia             English (Kenya)                          
Chilemba           English (Kenya)                          
Ezinne             English (Nigeria)                        
Imani              English (Tanzania)                       
Elimu              English (Tanzania)                       
Sabela             Galician (Spain)                         
Roi                Galician (Spain)                         
Siti               Javanese (Indonesia)                     
Dimas              Javanese (Indonesia)                     
Sreymom            Khmer (Cambodia)                         
Piseth             Khmer (Cambodia)                         
Dilara             Persian (Iran)                           
Farid              Persian (Iran)                           
Ubax               Somali (Somalia)                         
Muuse              Somali (Somalia)                         
Sofia              Spanish (Bolivia)                        
Marcelo            Spanish (Bolivia)                        
Catalina           Spanish (Chile)                          
Lorenzo            Spanish (Chile)                          
Maria              Spanish (Costa Rica)                     
Juan               Spanish (Costa Rica)                     
Belkys             Spanish (Cuba)                           
Manuel             Spanish (Cuba)                           
Ramona             Spanish (Dominican Republic)             
Emilio             Spanish (Dominican Republic)             
Andrea             Spanish (Ecuador)                        
Luis               Spanish (Ecuador)                        
Lorena             Spanish (El Salvador)                    
Rodrigo            Spanish (El Salvador)                    
Teresa             Spanish (Equatorial Guinea)              
Javier             Spanish (Equatorial Guinea)              
Marta              Spanish (Guatemala)                      
Andres             Spanish (Guatemala)                      
Karla              Spanish (Honduras)                       
Carlos             Spanish (Honduras)                       
Yolanda            Spanish (Nicaragua)                      
Federico           Spanish (Nicaragua)                      
Margarita          Spanish (Panama)                         
Roberto            Spanish (Panama)                         
Tania              Spanish (Paraguay)                       
Mario              Spanish (Paraguay)                       
Camila             Spanish (Peru)                           
Alex               Spanish (Peru)                           
Karina             Spanish (Puerto Rico)                    
Victor             Spanish (Puerto Rico)                    
Valentina          Spanish (Uruguay)                        
Mateo              Spanish (Uruguay)                        
Paola              Spanish (Venezuela)                      
Sebastian          Spanish (Venezuela)                      
Tuti               Sundanese (Indonesia)                    
Jajang             Sundanese (Indonesia)                    
Rehema             Swahili (Tanzania)                       
Daudi              Swahili (Tanzania)                       
Venba              Tamil (Singapore)                        
Anbu               Tamil (Singapore)                        
Saranya            Tamil (Sri Lanka)                        
Kumar              Tamil (Sri Lanka)                        
Gul                Urdu (India)                             
Salman             Urdu (India)                             
Madina             Uzbek (Uzbekistan)                       
Sardor             Uzbek (Uzbekistan)                       
Thando             Zulu (South Africa)                      
Themba             Zulu (South Africa)                      
Anila              Albanian (Albania)                       
Ilir               Albanian (Albania)                       
Layla              Arabic (Lebanon)                         
Rami               Arabic (Lebanon)                         
Aysha              Arabic (Oman)                            
Abdullah           Arabic (Oman)                            
Babek              Azerbaijani (Azerbaijan)                 
Banu               Azerbaijani (Azerbaijan)                 
Adri               Afrikaans (South Africa)                 
Willem             Afrikaans (South Africa)                 
Vesna              Bosnian (Bosnia and Herzegovina)         
Goran              Bosnian (Bosnia and Herzegovina)         
Eka                Georgian (Georgia)                       
Gudrun             Icelandic (Iceland)                      
Gunnar             Icelandic (Iceland)                      
Mekdes             Amharic (Ethiopia)                       
Ameha              Amharic (Ethiopia)                       
Aigul              Kazakh (Kazakhstan)                      
Daulet             Kazakh (Kazakhstan)                      
Keomany            Lao (Laos)                               
Chanthavong        Lao (Laos)                               
Marija             Macedonian (Republic of North Macedonia) 
Aleksandar         Macedonian (Republic of North Macedonia) 
Amina              Arabic (Algeria)                         
Ismael             Arabic (Algeria)                         
Yesui              Mongolian (Mongolia)                     
Bataa              Mongolian (Mongolia)                     
Hemkala            Nepali (Nepal)                           
Sagar              Nepali (Nepal)                           
Latifa             Pashto (Afghanistan)                     
GulNawaz           Pashto (Afghanistan)                     
Sophie             Serbian (Serbia, Cyrillic)               
Nicholas           Serbian (Serbia, Cyrillic)               
Thilini            Sinhala (Sri Lanka)                      
Sameera            Sinhala (Sri Lanka)                      
Kani               Tamil (Malaysia)                         
Surya              Tamil (Malaysia)                         
Xiaobei            Chinese (Mandarin, Simplified, Liaoning) 
================== =======================================================
