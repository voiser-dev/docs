Speech to Text
===================================

You can use the APIs on this page to convert your audio files to text. The conversion process consists of two stages:

    1. Creating a project (`Create API`_)
    2. Query the result and get the text (`Result API`_)
    3. (Optional) Translate the transcribed output into different languages. (`Translate API`_)


.. _Create API:

Create API
----------

The api you will use to convert your audio file to text.

.. http:post:: https://api.voiser.net/transcription/v1/

**Request Parameters**

    - **userCode -** Your Voiser user code.
    - **projectName -** The name you want to give your project.
    - **fileUrl -** The url of the audio file to be converted to text or the youtube video url.
    - **language -** Language code to be used. (`STT Languages`_)
    - **punctuation -** Can be used to set punctuation marks. (`Punctutation Options`_)
    - **profanityFilter -** You can hide bad words with the profanity filter. (`Profanity Options`_)

**Response Parameters**

    - **status -** If it returns 1, the record has been created, if it returns 0, a problem has occurred.
    - **message -** Informative message showing the result of your action.
    - **projectCode -** If your project has been successfully created, you can request the `Result API`_ using this project code.



**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'userCode' => 'YOUR_USER_CODE',
            'projectName' => 'Test Project',
            'fileUrl' => 'https://www.youtube.com/watch?v=0yoaMzhErnA&ab_channel=Voiser',
            'language' => 'en-US',
            'punctuation' => 'DictatedAndAutomatic',
            'profanityFilter' => 'Masked'
        );

        $ch = curl_init('https://api.voiser.net/transcription/v1/');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'userCode': 'YOUR_USER_CODE',
            'projectName': 'Test Project',
            'fileUrl': 'https://www.youtube.com/watch?v=0yoaMzhErnA&ab_channel=Voiser',
            'language': 'en-US',
            'punctuation': 'DictatedAndAutomatic',
            'profanityFilter': 'Masked'
        }
        response = requests.post('https://api.voiser.net/transcription/v1/', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
       "status": "1",
       "message": "Your decryption request has been successfully saved.",
       "projectCode": "ABCDEFGH"
    }



.. _Result API:

Result API
----------

Result API allows you to query the status of the project you have created and, if completed, returns the download urls of the text files.

.. http:post:: https://api.voiser.net/transcription/v1/result

**Request Parameters**

    - **userCode -** Your Voiser user code.
    - **projectCode -** The code of the project you want to query.

**Response Parameters**

    - **status -** If it returns 1, the record has been created, if it returns 0, a problem has occurred.
    - **message -** Informative message showing the result of your action.
    - **result -** It returns urls where you can download txt, srt, xlsx and docx file types.


**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'userCode' => 'YOUR_USER_CODE',
            'projectCode' => 'ABCDEFGH'
        );

        $ch = curl_init('https://api.voiser.net/transcription/v1/result');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'userCode': 'YOUR_USER_CODE',
            'projectCode': 'ABCDEFGH'
        }
        response = requests.post('https://api.voiser.net/transcription/v1/result', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
       "status": "1",
       "message": "Transcription completed successfully",
       "result": {
            "txt": "TXT_FILE_URL",
            "srt": "SRT_FILE_URL",
            "docx": "DOCX_FILE_URL",
            "xlsx": "XLSX_FILE_URL"
       }
    }



.. _Translate API:

Translate API
----------

Result API allows you to query the status of the project you have created and, if completed, returns the download urls of the text files.

.. http:post:: https://api.voiser.net/transcription/v1/translate

**Request Parameters**

    - **userCode -** Your Voiser user code.
    - **projectCode -** The code of the project you want to query.
    - **langCode -** Translation language code. (`Translate Languages`_)

**Response Parameters**

    - **status -** If it returns 1, the record has been created, if it returns 0, a problem has occurred.
    - **message -** Informative message showing the result of your action.
    - **result -** It returns translated transcription rows and their duration.


**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'userCode' => 'YOUR_USER_CODE',
            'projectCode' => 'ABCDEFGH',
            'langCode' => 'tr'
        );

        $ch = curl_init('https://api.voiser.net/transcription/v1/translate');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'userCode': 'YOUR_USER_CODE',
            'projectCode': 'ABCDEFGH',
            'langCode' => 'tr'
        }
        response = requests.post('https://api.voiser.net/transcription/v1/translate', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
       "status": "1",
       "message": "Transcript translate completed successfully",
       "result": [
            {
                "text": "Hey there, I'm Yasaman from Voicer.",
                "textTranslated": "Merhaba, ben Voiser'dan Yasaman.",
                "timeStart": "0.56",
                "timeEnd": 2.44
            },
            {
                "text": "Let me show you how.",
                "textTranslated": "Size nasıl olduğunu göstereyim.",
                "timeStart": "2.52",
                "timeEnd": 3.6
            },
            {
                "text": "Use our AL voice solutions and level up your content with a text to speech, natural voices, transcribe voice recordings and even create your own unique voice with upcoming voice cloning.",
                "textTranslated": "AL ses çözümlerimizi kullanın ve metninizi konuşmaya, doğal seslerle yükseltin, ses kayıtlarını yazıya dökün ve hatta yakında çıkacak olan ses klonlama ile kendi benzersiz sesinizi yaratın.",
                "timeStart": "3.60",
                "timeEnd": 14.12
            },
            {
                "text": "And there is more.",
                "textTranslated": "Dahası da var.",
                "timeStart": "14.56",
                "timeEnd": 15.56
            }
       ]
    }


.. _STT Languages:

STT Languages
-------------
=================================== =======
Language                            Code
=================================== =======
Afrikaans (South Africa)            af-ZA
Albanian (Albania)                  sq-AL
Amharic (Ethiopia)                  am-ET
Arabic (Algeria)                    ar-DZ
Arabic (Bahrain), (Modern Standard) ar-BH
Arabic (Egypt)                      ar-EG
Arabic (Iraq)                       ar-IQ
Arabic (Israel)                     ar-IL
Arabic (Jordan)                     ar-JO
Arabic (Kuwait)                     ar-KW
Arabic (Lebanon)                    ar-LB
Arabic (Libya)                      ar-LY
Arabic (Morocco)                    ar-MA
Arabic (Oman)                       ar-OM
Arabic (Palestinian)                ar-PS
Arabic (Qatar)                      ar-QA
Arabic (Saudi Arabia)               ar-SA
Arabic (Syria)                      ar-SY
Arabic (Tunisia)                    ar-TN
Arabic (United Arab Emirates)       ar-AE
Arabic (Yemen)                      ar-YE
Armenian (Armenia)                  hy-AM
Azerbaijani (Azerbaijan)            az-AZ
Basque (Spain)                      eu-ES
Bengali (India)                     bn-IN
Bulgarian (Bulgaria)                bg-BG
Burmese (Myanmar)                   my-MM
Catalan (Spain)                     ca-ES
Chinese (Cantonese, Traditional)    zh-HK
Chinese (Mandarin, Simplified)      zh-CN
Chinese (Taiwanese Mandarin)        zh-TW
Croatian (Croatia)                  hr-HR
Czech (Czech Republic)              cs-CZ
Czech (Czech)                       cs-CZ
Danish (Denmark)                    da-DK
Dutch (Belgium)                     nl-BE
Dutch (Netherlands)                 nl-NL
English (Australia)                 en-AU
English (Canada)                    en-CA
English (Ghana)                     en-GH
English (Hong Kong)                 en-HK
English (India)                     en-IN
English (Ireland)                   en-IE
English (Kenya)                     en-KE
English (New Zealand)               en-NZ
English (Nigeria)                   en-NG
English (Philippines)               en-PH
English (Singapore)                 en-SG
English (South Africa)              en-ZA
English (Tanzania)                  en-TZ
English (United Kingdom)            en-GB
English (United States)             en-US
Estonian(Estonia)                   et-EE
Filipino (Philippines)              fil-PH
Finnish (Finland)                   fi-FI
French (Belgium)                    fr-BE
French (Canada)                     fr-CA
French (France)                     fr-FR
French (Switzerland)                fr-CH
Galician (Spain)                    gl-ES
Georgian (Georgia)                  ka-GE
German (Austria)                    de-AT
German (Germany)                    de-DE
German (Switzerland)                de-CH
Greek (Greece)                      el-GR
Gujarati (Indian)                   gu-IN
Hebrew (Israel)                     he-IL
Hindi (India)                       hi-IN
Hungarian (Hungary)                 hu-HU
Icelandic (Iceland)                 is-IS
Indonesian (Indonesia)              id-ID
Irish (Ireland)                     ga-IE
Irish(Ireland)                      ga-IE
Italian (Italy)                     it-IT
Italian (Switzerland)               it-CH
Japanese (Japan)                    ja-JP
Javanese (Indonesia)                jv-ID
Kannada (India)                     kn-IN
Kazakh (Kazakhstan)                 kk-KZ
Khmer (Cambodia)                    km-KH
Korean (Korea)                      ko-KR
Lao (Laos)                          lo-LA
Latvian (Latvia)                    lv-LV
Lithuanian (Lithuania)              lt-LT
Macedonian (North Macedonia)        mk-MK
Malay (Malaysia)                    ms-MY
Maltese (Malta)                     mt-MT
Marathi (India)                     mr-IN
Mongolian (Mongolia)                mn-MN
Nepali (Nepal)                      ne-NP
Norwegian (Bokmål, Norway)          nb-NO
Persian (Iran)                      fa-IR
Polish (Poland)                     pl-PL
Portuguese (Brazil)                 pt-BR
Portuguese (Portugal)               pt-PT
Romanian (Romania)                  ro-RO
Russian (Russia)                    ru-RU
Serbian (Serbia)                    sr-RS
Sinhala (Sri Lanka)                 si-LK
Slovak (Slovakia)                   sk-SK
Slovenian (Slovenia)                sl-SI
Spanish (Argentina)                 es-AR
Spanish (Bolivia)                   es-BO
Spanish (Chile)                     es-CL
Spanish (Colombia)                  es-CO
Spanish (Costa Rica)                es-CR
Spanish (Cuba)                      es-CU
Spanish (Dominican Republic)        es-DO
Spanish (Ecuador)                   es-EC
Spanish (El Salvador)               es-SV
Spanish (Equatorial Guinea)         es-GQ
Spanish (Guatemala)                 es-GT
Spanish (Honduras)                  es-HN
Spanish (Mexico)                    es-MX
Spanish (Nicaragua)                 es-NI
Spanish (Panama)                    es-PA
Spanish (Paraguay)                  es-PY
Spanish (Peru)                      es-PE
Spanish (Puerto Rico)               es-PR
Spanish (Spain)                     es-ES
Spanish (Uruguay)                   es-UY
Spanish (USA)                       es-US
Spanish (Venezuela)                 es-VE
Swahili (Kenya)                     sw-KE
Swahili (Tanzania)                  sw-TZ
Swedish (Sweden)                    sv-SE
Tamil (India)                       ta-IN
Telugu (India)                      te-IN
Thai (Thailand)                     th-TH
Turkish (Turkey)                    tr-TR
Ukrainian (Ukraine)                 uk-UA
Uzbek (Uzbekistan)                  uz-UZ
Vietnamese (Vietnam)                vi-VN
Zulu (South Africa)                 zu-ZA
=================================== =======

.. _Punctutation Options:

Punctutation
------------
============================== =======================================
Option                         Description
============================== =======================================
DictatedAndAutomatic (Default) Automatically detects punctuation marks
None                           Does not use punctuation marks
Dictated                       Uses punctuation marks
============================== =======================================

.. _Profanity Options:

Profanity
---------

============================== =======================================
Option                         Description
============================== =======================================
Masked (Default)               Slang hides words
None                           Slang does not hide words
============================== =======================================

.. _Translate Languages:

Translate Languages
-------------------
=================================== =======
Language                            Code
=================================== =======
Afrikaans	                        af
Amharic	                            am
Arabic	                            ar
Assamese	                        as
Azerbaijani	                        az
Bashkir	                            ba
Bulgarian	                        bg
Bangla	                            bn
Tibetan	                            bo
Bosnian	                            bs
Catalan	                            ca
Czech	                            cs
Welsh	                            cy
Danish	                            da
German	                            de
Lower Sorbian	                    dsb
Divehi	                            dv
Greek	                            el
English	                            en
Spanish	                            es
Estonian	                        et
Basque	                            eu
Persian	                            fa
Finnish	                            fi
Filipino	                        fil
Fijian	                            fj
Faroese	                            fo
French	                            fr
French (Canada)	                    fr-CA
Irish	                            ga
Galician	                        gl
Konkani	                            gom
Gujarati	                        gu
Hausa	                            ha
Hebrew	                            he
Hindi	                            hi
Croatian	                        hr
Upper Sorbian	                    hsb
Haitian Creole	                    ht
Hungarian	                        hu
Armenian	                        hy
Indonesian	                        id
Igbo	                            ig
Inuinnaqtun	                        ikt
Icelandic	                        is
Italian	                            it
Inuktitut	                        iu
Inuktitut (Latin)	                iu-Latn
Japanese	                        ja
Georgian	                        ka
Kazakh	                            kk
Khmer	                            km
Kurdish (Northern)	                kmr
Kannada	                            kn
Korean	                            ko
Kurdish (Central)	                ku
Kyrgyz	                            ky
Lingala	                            ln
Lao	                                lo
Lithuanian	                        lt
Ganda	                            lug
Latvian	                            lv
Chinese (Literary)	                lzh
Maithili	                        mai
Malagasy	                        mg
Māori	                            mi
Macedonian	                        mk
Malayalam	                        ml
Mongolian (Cyrillic)	            mn-Cyrl
Mongolian (Traditional)	            mn-Mong
Marathi	                            mr
Malay	                            ms
Maltese	                            mt
Hmong Daw	                        mww
Myanmar (Burmese)	                my
Norwegian	                        nb
Nepali	                            ne
Dutch	                            nl
Sesotho sa Leboa	                nso
Nyanja	                            nya
Odia	                            or
Querétaro Otomi	                    otq
Punjabi	                            pa
Polish	                            pl
Dari	                            prs
Pashto	                            ps
Portuguese (Brazil)	                pt
Portuguese (Portugal)	            pt-PT
Romanian	                        ro
Russian	                            ru
Rundi	                            run
Kinyarwanda	                        rw
Sindhi	                            sd
Sinhala	                            si
Slovak	                            sk
Slovenian	                        sl
Samoan	                            sm
Shona	                            sn
Somali	                            so
Albanian	                        sq
Serbian (Cyrillic)	                sr-Cyrl
Serbian (Latin)	                    sr-Latn
Sesotho	                            st
Swedish	                            sv
Swahili	                            sw
Tamil	                            ta
Telugu	                            te
Thai	                            th
Tigrinya	                        ti
Turkmen	                            tk
Klingon (Latin)	                    tlh-Latn
Klingon (pIqaD)	                    tlh-Piqd
Setswana	                        tn
Tongan	                            to
Turkish	                            tr
Tatar	                            tt
Tahitian	                        ty
Uyghur	                            ug
Ukrainian	                        uk
Urdu	                            ur
Uzbek (Latin)	                    uz
Vietnamese	                        vi
Xhosa	                            xh
Yoruba	                            yo
Yucatec Maya	                    yua
Cantonese (Traditional)	            yue
Chinese Simplified	                zh-Hans
Chinese Traditional	                zh-Hant
Zulu	                            zu
=================================== =======